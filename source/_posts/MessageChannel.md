---
title: DeepClone
date: 2023-01-04 12:12:03
comments: true
tags:
  - 深拷贝
---

### MessageChannel

使用 [MessageChannel](https://developer.mozilla.org/zh-CN/docs/Web/API/MessageChannel) 深拷贝，但无法复制 function

```javascript
function deeepClone(obj) {
  return new Promise((resolve) => {
    const { port1, port2 } = new MessageChannel();
    port1.postMessage(obj1);
    port2.onmessage = (msg) => {
      resolve(msg.data);
    };
  });
}
const obj1 = {
  a: 1,
  b: 2,
  c: 5,
};
obj1.c = obj1;
const obj2 = deeepClone(obj1);
console.log(obj2.then((o) => console.log(o)));
```

### WeakMap

```javascript
function deepClone(source, hash = new WeakMap()) {
  const _deepClone = (source) => {
    if (typeof source !== "object" || source == null) return source;

    if (hash.has(source)) {
      return hash.get(source);
    }

    const result = Array.isArray(source) ? [] : {};
    hash.set(source, result);
    for (const item in source) {
      result[item] = _deepClone(source[item]);
    }
    return result;
  };
  return _deepClone(source);
}
```
