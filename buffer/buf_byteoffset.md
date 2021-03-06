
* {integer} 创建 `Buffer` 对象时基于的底层 `ArrayBuffer` 对象的 `byteOffset`。

当 `Buffer.from(ArrayBuffer, byteOffset, length)` 设置了 `byteOffset` 或创建一个小于 `Buffer.poolSize` 的 buffer 时，底层的 `ArrayBuffer` 的偏移量并不是从 0 开始。

当直接使用 `buf.buffer` 访问底层的 `ArrayBuffer` 时，`ArrayBuffer` 的第一个字节可能并不指向 `buf` 对象。

所有使用 `Buffer` 对象创建 `TypedArray` 对象时，需要正确地指定 `byteOffset`。

```js
// 创建一个小于 `Buffer.poolSize` 的 buffer。
const nodeBuffer = new Buffer.from([0, 1, 2, 3, 4, 5, 6, 7, 8, 9]);

// 当将 Node.js Buffer 赋值给一个 Int8 的 TypedArray 时，记得使用 byteOffset。
new Int8Array(nodeBuffer.buffer, nodeBuffer.byteOffset, nodeBuffer.length);
```

