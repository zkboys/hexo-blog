---
title: js滚动动画
date: 2016-11-17 17:10:27
category: [前端, JS]
tags: [js]
---
js原生函数，滚动动画
```js
/**
 * 滚动动画函数
 * @param el 元素对象或者元素id
 * @param targetPosition 滚动条目标位置
 * @param duringTime 持续时间 默认300
 * @param onComplete 滚动完成触发
 */
export function scrollAnimate({el, targetPosition, duringTime = 300, onComplete}) {
    if (typeof el === 'string') {
        el = document.getElementById(el);
    }

    if (!targetPosition) return;

    const startTime = (new Date()).getTime();

    function animate() {
        const nowTime = (new Date()).getTime();
        const elapsed = nowTime - startTime;
        const fraction = elapsed / duringTime;
        const position = targetPosition - el.scrollTop;
        if (fraction < 1) {
            el.scrollTop += fraction * position * Math.sin(Math.PI / 2);
            setTimeout(animate, Math.min(25, duringTime - elapsed));
        } else {
            el.scrollTop = targetPosition;
            if (onComplete) {
                onComplete();
            }
        }
    }

    animate();
}

```
