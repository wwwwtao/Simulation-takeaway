<!--
作者：布衣 1983
链接：https://juejin.cn/post/7221813031813054501
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
-->

## Blob API

Blob API 用于处理二进制数据，可以方便地将数据转换为 Blob 对象或从 Blob 对象读取数据。

```js
// 创建一个Blob对象
const myBlob = new Blob(["Hello, world!"], { type: "text/plain" });

// 读取Blob对象的数据
const reader = new FileReader();
reader.addEventListener("loadend", () => {
  console.log(reader.result);
});
reader.readAsText(myBlob);
```

使用场景：在 Web 应用中，可能需要上传或下载二进制文件，使用 Blob API 可以方便地处理这些数据。

<!-- Blob 对象主要的作用应该不是文件上传，而是文件预览，文件上传的核心应该是 FormData，如果一定要说文件上传那应该是大文件分片上传才会用到，一般文件上传都用不上这个。 -->

## WeakSet

WeakSet 类似于 Set，但可以存储弱引用的对象。这意味着，如果没有其他引用指向一个对象，那么这个对象可以被垃圾回收器回收，而不需要手动从 WeakSet 中删除。

```js
const myWeakSet = new WeakSet();
const obj1 = {};
const obj2 = {};

myWeakSet.add(obj1);
myWeakSet.add(obj2);

console.log(myWeakSet.has(obj1)); // true

obj1 = null;

console.log(myWeakSet.has(obj1)); // false

```

使用场景：在某些情况下，可能需要存储一些临时的对象，但又不希望这些对象占用太多的内存。使用 WeakSet 可以方便地管理这些对象。

<!-- WeakSet 存的是弱引用，也并不是什么需要临时存储的对象，减少内存占用，而是方便管理一些不重要的数据，这些存储的数据会随着原始数据销毁而被清除掉，而不会因为原始数据被引用而导致该数据无法进行垃圾回收。和 WeakSet 同期的还有 WeakMap -->

## Web Workers

Web Workers 可以用于在后台线程中执行 JavaScript 代码，可以用于提高性能或实现复杂的计算。

```js
// main.js
const myWorker = new Worker("worker.js");

myWorker.postMessage("Hello, worker!");

myWorker.onmessage = (event) => {
  console.log(`Message received from worker: ${event.data}`);
};

// worker.js
onmessage = (event) => {
  console.log(`Message received in worker: ${event.data}`);
  postMessage("Hello, main!");
};
```

使用场景：在 Web 应用中，可能需要处理大量计算密集型任务或执行长时间运行的操作，使用 Web Workers 可以提高性能或避免阻塞用户界面。

## TextEncoder 和 TextDecoder

TextEncoder 和 TextDecoder 用于处理字符串和字节序列之间的转换。它们可以方便地将字符串编码为字节序列或将字节序列解码为字符串。

```js
const encoder = new TextEncoder();
const decoder = new TextDecoder();

const myString = "Hello, world!";
const myBuffer = encoder.encode(myString);

console.log(myBuffer); // Uint8Array(13) [72, 101, 108, 108, 111, 44, 32, 119, 111, 114, 108, 100, 33]

const decodedString = decoder.decode(myBuffer);

console.log(decodedString); // "Hello, world!"

```

使用场景：在 Web 应用中，可能需要将字符串转换为二进制数据，或将二进制数据转换为字符串。使用 TextEncoder 和 TextDecoder 可以方便地进行这些转换。

## Object.entries() 和 Object.values()

Object.entries() 用于获取对象的可枚举属性和值的数组，Object.values() 用于获取对象的可枚举属性值的数组。

```js
const myObject = {
  name: "John",
  age: 30,
};

console.log(Object.entries(myObject)); // [["name", "John"], ["age", 30]]
console.log(Object.values(myObject)); // ["John", 30]

```

使用场景：在某些情况下，可能需要获取对象的可枚举属性或属性值。使用 Object.entries() 和 Object.values() 可以方便地实现这些功能。

## IntersectionObserver

IntersectionObserver 可以用于检测元素是否进入视口，可以用于实现无限滚动、懒加载等功能。

```js
const myObserver = new IntersectionObserver((entries, observer) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      console.log(`${entry.target.id} is now visible`);
      observer.unobserve(entry.target);
    }
  });
});

const myElement = document.getElementById("myElement");
myObserver.observe(myElement);

```

使用场景：在 Web 应用中，可能需要实现无限滚动、懒加载等功能，使用 IntersectionObserver 可以方便地实现这些功能。

## Symbol

Symbol 可以用于创建唯一标识符，可以用于定义对象的私有属性或方法。

```js
const mySymbol = Symbol("mySymbol");

const myObject = {
  [mySymbol]: "This is a private property",
  publicProperty: "This is a public property",
};

console.log(myObject[mySymbol]); // "This is a private property"
console.log(myObject.publicProperty); // "This is a public property"

```

使用场景：在某些情况下，可能需要定义对象的私有属性或方法，使用 Symbol 可以方便地实现这些功能。

## Proxy API

Proxy API 可以用于创建代理对象，可以拦截对象属性的读取、赋值等操作。这个功能可以用于实现元编程、数据劫持等功能。

```js
const myObject = {
  name: "John",
  age: 30,
};

const myProxy = new Proxy(myObject, {
  get(target, property) {
    console.log(`Getting property ${property}`);
    return target[property];
  },
  set(target, property, value) {
    console.log(`Setting property ${property} to ${value}`);
    target[property] = value;
  },
});

console.log(myProxy.name); // "John"

myProxy.age = 31; // Setting property age to 31

```

使用场景：在某些情况下，可能需要拦截对象属性的读取、赋值等操作，以实现更高级的功能。使用 Proxy API 可以方便地实现这些功能。

## Reflect API

Reflect API 可以用于实现元编程，例如动态调用对象的方法或构造函数。

```js
class MyClass {
  constructor(value) {
    this.value = value;
  }

  getValue() {
    return this.value;
  }
}

const myObject = Reflect.construct(MyClass, ["Hello, world!"]);
const myMethod = Reflect.get(myObject, "getValue");
const myValue = myMethod.call(myObject);

console.log(myValue); // "Hello, world!"
```

使用场景：在某些情况下，可能需要动态调用对象的方法或构造函数，使用 Reflect API 可以方便地实现这些功能。

## Generator API

Generator API 可以用于生成迭代器，可以用于实现异步操作或惰性计算。

```js
function* myGenerator() {
  yield "Hello";
  yield "world";
  yield "!";
}

const myIterator = myGenerator();

console.log(myIterator.next().value); // "Hello"
console.log(myIterator.next().value); // "world"
console.log(myIterator.next().value); // "!"
```

使用场景：在某些情况下，可能需要实现异步操作或惰性计算，使用 Generator API 可以方便地实现这些功能。

## AudioContext

AudioContext 可以用于处理音频，可以用于实现音频播放、音效处理等功能。

```js
const audioContext = new AudioContext();

fetch("https://example.com/audio.mp3")
  .then((response) => response.arrayBuffer())
  .then((arrayBuffer) => audioContext.decodeAudioData(arrayBuffer))
  .then((audioBuffer) => {
    const source = audioContext.createBufferSource();
    source.buffer = audioBuffer;
    source.connect(audioContext.destination);
    source.start();
  });
```

使用场景：在 Web 应用中，可能需要实现音频播放、音效处理等功能，使用 AudioContext 可以方便地实现这些功能。
