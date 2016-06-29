---
title: js构造树状数据结构
date: 2016-06-29 20:49:58
category: [前端, JS]
tags: [js]
---
菜单，组织结构等场景经常会用到树状结构的数据，树状结构数据可以后端构造，也可以前端构造，如下是js方式构造数据，需要扁平数据结构为
```js
[
  {key: 1, parentKey: 0, text: '一级'},
  {key: 2, parentKey: 1, text: '二级2'},
  {key: 3, parentKey: 1, text: '二级3'},
  ...
]
```
key， parentKey， text 函数中会用到，如果后端给出的不是这三个字段，可以适当改造如下方法，或者做映射。
```js
/**
 * 检测某个节点是否有parent节点
 * @param rows 所有节点
 * @param row 需要判断得节点
 * @returns {boolean}
 */
export function hasParent(rows, row) {
    let parentKey = row.parentKey;
    for (let i = 0; i < rows.length; i++) {
        if (rows[i].key === parentKey) return true;
    }
    return false;
}

/**
 * js构造树方法。
 * @param rows 具有key，parentKey关系的扁平数据结构，标题字段为text
 * @param parentNode 开始节点
 * @returns {array}
 */
export function convertToTree(rows, parentNode) {
    // 这个函数会被多次调用，对rows做深拷贝，否则会产生副作用。
    rows = rows.map((row) => {
        return assign({}, row);
    });
    parentNode = assign({}, parentNode);

    let nodes = [];
    if (parentNode) {
        nodes.push(parentNode);
    } else {
        // 获取所有的顶级节点
        for (let i = 0; i < rows.length; i++) {
            let row = rows[i];
            if (!hasParent(rows, row.parentKey)) {
                nodes.push(row);
            }
        }
    }

    // 存放要处理的节点
    let toDo = nodes.map((v) => v);

    while (toDo.length) {
        // 处理一个，头部弹出一个。
        let node = toDo.shift();
        // 获取子节点。
        for (let i = 0; i < rows.length; i++) {
            let row = rows[i];
            if (row.parentKey === node.key) {
                let child = row;
                let parentKeys = [node.key];
                if (node.parentKeys) {
                    parentKeys = node.parentKeys.concat(node.key);
                }
                child.parentKeys = parentKeys;
                let parentText = [node.text];
                if (node.parentText) {
                    parentText = node.parentText.concat(node.text);
                }
                child.parentText = parentText;

                if (node.children) {
                    node.children.push(child);
                } else {
                    node.children = [child];
                }
                // child加入toDo，继续处理
                toDo.push(child);
            }
        }
    }
    if (parentNode) {
        return nodes[0].children;
    }
    return nodes;
}

```
