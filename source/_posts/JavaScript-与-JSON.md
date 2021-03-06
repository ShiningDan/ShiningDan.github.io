﻿---
title: JavaScript 与 JSON
date: 2017-04-08 12:28:09
categories: coding
tags:
  - JavaScript
---

JSON和JavaScript确实存在渊源，可以说这种数据格式是从JavaScript对象中演变出来的，它是JavaScript的一个子集。JSON本身的意思就是JavaScript对象表示法（JavaScript Object Notation），它用严格的JavaScript对象表示法来表示结构化的数据。

**并不是只有 JavaScript 才能使用 JSON，JSON 只是一种数据格式。**

JSON 的语法可以表示下面三种类型的值：

* **简单值**：在 JSON 中，简单只可以是 **字符串、数值、布尔值、null**。JSON 不支持 `undefined` 和 函数。**JSON**中字符串必须使用双引号，单引号会导致语法错误。
* **对象**：对象是一种复杂的数据类型，表示的是一组无序的键值对，键值对中的值可以是简单值，也可以是复杂的数据类型。
* **数组**：数组是一种复杂的数据类型，表示一组有序的简单值，或者对象，或者数组列表。

<!--more-->

**JSON 中所有的属性都需要加上引号！**但是 JavaScript 在定义对象字面量的时候不需要加引号：

```
let person = {
    name: "Z",
    age: 20,
}
```

转化为 JSON 就是：

```
{
    "name": "Z",
    "age": 20   //  末尾不能有分号
}
```

### JSON 的解析和序列化

可以使用 `JSON` 来将一个 JavaScript 对象解析成 String 类型的数据结构，也可以将 JSON 数据结构解析成 JavaScript 对象。

在 ECMAScript 5 中定义了全局对象 `JSON`（注意：`JSON` 是一个对象，而不是类），在 JavaScript 中也没有 JSON 这个数据类型。`JSON` 里面有两个方法：

1. `JSON.parse(str)`： 将一个 String 类型的 JSON 数据结构解析为 JavaScript 对象
2. `JSON.stringify(obj)`：将一个JavaScript 对象序列化为 JSON 数据结构。



#### JSON.parse(str)

```
JSON.parse(text[, reviver])
```

`text`: The string to parse as JSON. See the JSON object for a description of JSON syntax.
`reviver`: Optional, If a function, prescribes how the value originally produced by parsing is transformed, before being returned.


##### Return value

The Object corresponding to the given JSON text.

##### Exceptions

Throws a SyntaxError exception if the string to parse is not valid JSON.

##### Examples

例子如下：

```
JSON.parse('{}');              // {}
JSON.parse('true');            // true
JSON.parse('"foo"');           // "foo"
JSON.parse('[1, 5, "false"]'); // [1, 5, "false"]
JSON.parse('null');            // null
```

针对 reviver，也就是对每一个属性进行处理的例子：

```
JSON.parse('{"p": 5}', (key, value) =>
  typeof value === 'number'
    ? value * 2 // return value * 2 for numbers
    : value     // return everything else unchanged
);
```

```
JSON.parse('{"1": 1, "2": 2, "3": {"4": 4, "5": {"6": 6}}}', (key, value) => {
  console.log(key); // log the current property name, the last is "".
  return value;     // return the unchanged property value.
});
```

#### JSON.stringify(obj)

```
JSON.stringify(value[, replacer[, space]])
```

`value`: The value to convert to a JSON string. // value 指的就是需要转换成字符串的 JavaScript 对象

`replacer`: Optional, A function that alters the behavior of the stringification process, or an array of String and Number objects that serve as a whitelist for selecting/filtering the properties of the value object to be included in the JSON string. If this value is null or not provided, all properties of the object are included in the resulting JSON string.  // 第二个参数是一个函数，表示在 JavaScript 对象转换为字符串的时候，针对每一个属性的处理方法，也就是一个过滤器，或者传入一个数组，只有数组中的属性才会被转换成字符串。

`space`: Optional, A String or Number object that's used to insert white space into the output JSON string for readability purposes. If this is a Number, it indicates the number of space characters to use as white space; this number is capped at 10 (if it is greater, the value is just 10). Values less than 1 indicate that no space should be used. If this is a String, the string (or the first 10 characters of the string, if it's longer than that) is used as white space. If this parameter is not provided (or is null), no white space is used. // 第三个参数指定在输出的字符串中是否要保留缩进，以及如何保留缩进。如果参数是一个数值，则表示每个缩进的空格数，空格数量不能超过10。如果这个参数是一个字符串，则这个字符串就作为缩进进行输出。如果这个参数不赋值，则不会输出空格。

**注意，如果传入的对象就是简单值，则 `JSON.stringify()` 返回的值也是字符串化的简单值。由于 JSON 中没有 `undefined` 和 `function`，如果传入的对象属性中如果包含这两个种类型，则序列化的时候会跳过该属性。**

```
JSON.stringify({});                  // '{}'
JSON.stringify(true);                // 'true'
JSON.stringify('foo');               // '"foo"'
JSON.stringify([1, 'false', false]); // '[1,"false",false]'
JSON.stringify({ x: 5 });            // '{"x":5}'

JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)) 
// '"2006-01-02T15:04:05.000Z"'

JSON.stringify({ x: 5, y: 6 });
// '{"x":5,"y":6}' or '{"y":6,"x":5}'
JSON.stringify([new Number(1), new String('false'), new Boolean(false)]);
// '[1,"false",false]'

JSON.stringify({ x: [10, undefined, function(){}, Symbol('')] }); 
// '{"x":[10,null,null,null]}' 
 
// Symbols:
JSON.stringify({ x: undefined, y: Object, z: Symbol('') });
// '{}'
JSON.stringify({ [Symbol('foo')]: 'foo' });
// '{}'
JSON.stringify({ [Symbol.for('foo')]: 'foo' }, [Symbol.for('foo')]);
// '{}'
JSON.stringify({ [Symbol.for('foo')]: 'foo' }, function(k, v) {
  if (typeof k === 'symbol') {
    return 'a symbol';
  }
});
// '{}'

// Non-enumerable properties:
JSON.stringify( Object.create(null, { x: { value: 'x', enumerable: false }, y: { value: 'y', enumerable: true } }) );
// '{"y":"y"}'
```

#### toJSON 方法

```
let book = {
    name: "JS You Don't Know",
    year: 2012,
    toJSON: function() {
        return this.name;
    }
}
```

可以在 JavaScript 对象中定义 `toJSON()` 方法，表示这个对象应该怎么被序列化。当调用 `JSON.stringify()` 方法的时候，按照下面的顺序进行序列化：

1. 如果有 `toJSON()` 方法，并且返回有效值，则调用该方法，否则返回对象本身。
2. 如果提供第二个参数，则应用这个函数过滤器，传入过滤器的参数的值是(1)返回的值
3. 对 (2) 返回的值进行序列化
4. 如果提供了第三个参数，则执行对应的格式化










