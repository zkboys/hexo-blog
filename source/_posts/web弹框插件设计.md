---
title: web弹框插件设计
date: 2016-05-31 19:26:47
category: [实现方案]
tags: [弹框]
---
*弹框一般项目都会用到，项目中的所有弹框要做到统一，需要对弹框组件做单独的整理维护*

一般弹框分为：
> alert、confirm、promp、toast这么几种

设计一个通用的modal，其他（任何弹框、滑出形式组件）的组件基于modal实现，统一底层的实现，便于后期统一维护和修改，统一控制，这一点很重要。其实是使用了**外观模式**。根据参数个数判断参数的作用，实现类似重载功能，下面是简单的实现原理：
*具体参考framework7源码modals.js*
```javascript
app.modal = function(options){
    ……
}
alert = function (text, title, callbackOk) {
    if (typeof title === 'function') {
        callbackOk = arguments[1];
        title = undefined;
    }
    return app.modal(options);
};
confirm = function (text, title, callbackOk, callbackCancel) {
    if (typeof title === 'function') {
        callbackCancel = arguments[2];
        callbackOk = arguments[1];
        title = undefined;
    }
    return app.modal(options);
};
prompt = function (text, title, callbackOk, callbackCancel,callbackOpened) {
    if (typeof title === 'function') {
        callbackCancel = arguments[2];
        callbackOk = arguments[1];
        callbackOpened = arguments[3];
        title = undefined;
    }
    return  app.modal(options);
};
```
如下是基于F7改造的一个jQuery插件（样式使用的还是F7的样式）
```javascript
/*========================================================
 * 弹出框
 * =======================================================*/
// TODO F7有些方法没实现,暂时不需要
;
(function ($, window, document, undefined) {
    var modalStack = [];
    var _modalTemplateTempDiv = document.createElement('div');

    function modal(params) {
        params = params || {};
        var modalHTML = '';
        var buttonsHTML = '';
        if (params.buttons && params.buttons.length > 0) {
            for (var i = 0; i < params.buttons.length; i++) {
                buttonsHTML += '<span class="modal-button' + (params.buttons[i].bold ? ' modal-button-bold' : '') + '">' + params.buttons[i].text + '</span>';
            }
        }
        var titleHTML = params.title ? '<div class="modal-title">' + params.title + '</div>' : '';
        var textHTML = params.text ? '<div class="modal-text">' + params.text + '</div>' : '';
        var afterTextHTML = params.afterText ? params.afterText : '';
        var noButtons = !params.buttons || params.buttons.length === 0 ? 'modal-no-buttons' : '';
        var verticalButtons = params.verticalButtons ? 'modal-buttons-vertical' : '';
        modalHTML = '<div class="modal ' + noButtons + ' ' + (params.cssClass || '') + '"><div class="modal-inner">' + (titleHTML + textHTML + afterTextHTML) + '</div><div class="modal-buttons ' + verticalButtons + '">' + buttonsHTML + '</div></div>';


        _modalTemplateTempDiv.innerHTML = modalHTML;

        var modal = $(_modalTemplateTempDiv).children();

        $('body').append(modal[0]);

        // Add events on buttons
        modal.find('.modal-button').each(function (index, el) {
            $(el).on('click', function (e) {
                if (params.buttons[index].close !== false) closeModal(modal);
                if (params.buttons[index].onClick) params.buttons[index].onClick(modal, e);
                if (params.onClick) params.onClick(modal, index);
            });
        });
        openModal(modal);
        return modal;
    }

    function openModal(modal) {
        modal = $(modal);
        var isModal = modal.hasClass('modal');
        if ($('.modal.modal-in:not(.modal-out)').length && isModal) {
            modalStack.push(function () {
                openModal(modal);
            });
            return;
        }
        // do nothing if this modal already shown
        if (true === modal.data('f7-modal-shown')) {
            return;
        }
        modal.data('f7-modal-shown', true);
        modal.trigger('close', function () {
            modal.removeData('f7-modal-shown');
        });
        if (isModal) {
            modal.show();
            modal.css({
                marginTop: -Math.round(modal.outerHeight() / 2) + 'px'
            });
        }

        if ($('.modal-overlay').length === 0) {
            $('body').append('<div class="modal-overlay"></div>');
        }
        var overlay = $('.modal-overlay');
        //Make sure that styles are applied, trigger relayout;
        var clientLeft = modal[0].clientLeft;//这个不能删,删了actions动画没了.
        // Trugger open event
        modal.trigger('open');
        // Classes for transition in
        overlay.addClass('modal-overlay-visible');
        modal.removeClass('modal-out').addClass('modal-in').transitionEnd(function (e) {
            if (modal.hasClass('modal-out')) modal.trigger('closed');
            else modal.trigger('opened');
        });
        return true;
    }

    function closeModal(modal) {
        modal = $(modal || '.modal-in');
        if (typeof modal !== 'undefined' && modal.length === 0) {
            return;
        }
        var isModal = modal.hasClass('modal');
        var overlay = $('.modal-overlay');
        if (overlay && overlay.length > 0) {
            overlay.removeClass('modal-overlay-visible');
        }
        modal.trigger('close');
        modal.removeClass('modal-in').addClass('modal-out').transitionEnd(function (e) {
            if (modal.hasClass('modal-out')) modal.trigger('closed');
            else modal.trigger('opened');
            modal.remove();
        });
        if (isModal) {
            modalStackClearQueue();
        }
        return true;
    }

    function modalStackClearQueue() {
        if (modalStack.length) {
            (modalStack.shift())();
        }
    }

    var modalTitle = '提示';
    var modalButtonOk = '确定';
    var modalButtonCancel = '取消';
    var modalPreloaderTitle = '加载中';
    $.extend({
        alert: function (text, title, callbackOk) {
            if (typeof title === 'function') {
                callbackOk = arguments[1];
                title = undefined;
            }
            return modal({
                text: text || '',
                title: typeof title === 'undefined' ? modalTitle : title,
                buttons: [
                    {text: modalButtonOk, bold: true, onClick: callbackOk}
                ]
            });
        },
        confirm: function (text, title, callbackOk, callbackCancel) {
            if (typeof title === 'function') {
                callbackCancel = arguments[2];
                callbackOk = arguments[1];
                title = undefined;
            }
            return modal({
                text: text || '',
                title: typeof title === 'undefined' ? modalTitle : title,
                buttons: [
                    {text: modalButtonCancel, onClick: callbackCancel},
                    {text: modalButtonOk, bold: true, onClick: callbackOk}
                ]
            });
        },
        showPreloader: function (title) {
            return modal({
                title: title || modalPreloaderTitle,
                text: '<div class="preloader"></div>',
                cssClass: 'modal-preloader'
            });
        },
        hidePreloader: function () {
            closeModal('.modal.modal-in');
        },
        showIndicator: function () {
            //$('body').append('<div class="preloader-indicator-overlay"></div><div class="preloader-indicator-modal"><span class="preloader preloader-white"></span></div>');
            //去掉全屏透明遮盖层
            $('body').append('<div class="preloader-indicator-modal"><span class="preloader preloader-white"></span></div>');
        },
        hideIndicator: function () {
            $('.preloader-indicator-overlay, .preloader-indicator-modal').remove();
        },
        toast: function (text, closeCallBack) {
            var m = modal({
                title: '',
                text: text
            });
            if (closeCallBack) {
                m.on("close", closeCallBack);
            }
            setTimeout(function () {
                closeModal();
            }, 1500);
            return modal
        },
        actions: function (params) {
            var modal, groupSelector, buttonSelector;

            params = params || [];

            if (params.length > 0 && !$.isArray(params[0])) {
                params = [params];
            }
            var modalHTML;

            var buttonsHTML = '';
            for (var i = 0; i < params.length; i++) {
                for (var j = 0; j < params[i].length; j++) {
                    if (j === 0) buttonsHTML += '<div class="actions-modal-group">';
                    var button = params[i][j];
                    var buttonClass = button.label ? 'actions-modal-label' : 'actions-modal-button';
                    if (button.bold) buttonClass += ' actions-modal-button-bold';
                    if (button.color) buttonClass += ' color-' + button.color;
                    if (button.bg) buttonClass += ' bg-' + button.bg;
                    if (button.disabled) buttonClass += ' disabled';
                    buttonsHTML += '<div class="' + buttonClass + '">' + button.text + '</div>';
                    if (j === params[i].length - 1) buttonsHTML += '</div>';
                }
            }
            modalHTML = '<div class="actions-modal">' + buttonsHTML + '</div>';
            _modalTemplateTempDiv.innerHTML = modalHTML;
            modal = $(_modalTemplateTempDiv).children();
            $('body').append(modal[0]);
            groupSelector = '.actions-modal-group';
            buttonSelector = '.actions-modal-button';

            var groups = modal.find(groupSelector);
            groups.each(function (index, el) {
                var groupIndex = index;
                $(el).children().each(function (index, el) {
                    var buttonIndex = index;
                    var buttonParams = params[groupIndex][buttonIndex];
                    var clickTarget;
                    if ($(el).is(buttonSelector)) clickTarget = $(el);
                    if ($(el).find(buttonSelector).length > 0) clickTarget = $(el).find(buttonSelector);

                    if (clickTarget) {
                        clickTarget.on('click', function (e) {
                            if (buttonParams.close !== false) closeModal(modal);
                            if (buttonParams.onClick) buttonParams.onClick(modal, e);
                        });
                    }
                });
            });
            openModal(modal);
            return modal;
        },
        closeModal: closeModal
    });
})(jQuery, window, document);
```
