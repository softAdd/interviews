## \_\_proto\_\_ и prototype - свойства объектов. На основе: [IT-KAMASUTRA](https://youtu.be/b55hiUlhAzI?list=WL)

```js
// a - ссылается на объект { value: 18 }
let a = { value: 18 }
// b.age - ссылается на тот же объект
let b = {
  age: a
}
// c - ссылается на тот же объект
let c = a
// Итого:
// a === b.age
// a === c
```

**\_\_proto\_\_**

Есть у всех (практически, за редким исключением) объектов.<br>
\_\_proto\_\_ - ПОЧТИ ВСЕГДА объект.
```js
let man = {} // man.__proto__
let users = [] // users.__proto__
let age = 18 // age.__proto__ - у примитивов тоже есть __proto__
let str = 'str' // age.__proto__
// функции, стрелочные функции, классы и т.д. - все имеют свойство __proto__
```

Одинаковые по "типу" объекты имеют равное свойство прото:
```js
let man = {}
let man_2 = {}
// man !== man_2
// man.__proto__ === man_2.__proto__
let users = []
let cars = []
// users.__proto__ === cars.__proto__
let str_1 = 'строка 1'
let str_2 = 'строка 2'
// str_1.__proto__ === str_2.__proto__
// это касается остальных типов данных
```

Любой объект в JS создается с помощью класса/функции конструктора (с помощью new, явно или нет).
```js
let promise = new Promise(() => {}) // new Promise(...)
let man = {} // new Object(...)
let users = [] // new Array(...)
let age = 18 // new Number(...)
let str = 'строка' // new String(...)
let func = () => {} // new Function(...)
// и т.д.
```

Итого:
1. У любого объекта есть свойство \_\_proto\_\_.
2. Чтобы определить прото, нужно знать с помощью какой функции-конструктора (класса) создан объект. То есть, если объекты созданы одной и той же функцией, то их прото также одно.

**prototype**

Прототип - по сути независимый объект.<br>
Классы и функции (стрелочные функции не содержат прототипы) содержат в себе prototype. Каждый prototype - независимый объект: Object.prototype !== Promise.prototype.

**proto и prototype**

proto - у любого объекта, prototype - у класса или функции.<br>
proto любого объекта ссылается на prototype класса (функции-конструктора), с помощью которой этот объект был создан.
```js
new Promise(() => {}).__proto__ === Promise.prototype
{}.__proto__ === Object.prototype
[].__proto__ === Array.prototype
18.__proto__ === Number.prototype
'str'.__proto__ === String.prototype
true.__proto__ === Boolean.prototype
// Прототип класса - функция
class Example {}
Example.__proto__ === Function.prototype
// прототип нового объекта класса Example - Example.prototype
new Example.__proto__ === Example.prototype
```

**Зачем они нужны**

```js
// можно создать множество объектов с помощью функции
function Samurai(name) {
  this.name = name;
}
// все они будут содержать в себе свойство name
let samurai_1 = new Samurai('samurai_1');
...
let samurai_199911 = new Samurai('samurai_199911');
// но если понадобится метод, например, для вывода имени - то необязательно его хранить в каждом объекте
// можно записать его внутрь прототипа функции, куда будет обращаться каждый из объектов, в случае необходимости
Samurai.prototype.sayName = function() {
  alert(this.name);
}
```

**Современный синстаксис**

```js
class Samurai {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    alert(this.name);
  }
}
```

**Итого**

1. proto - у любого объекта, prototype - у функций, созданных с помощью ключевого слова function и классов.
2. proto - ссылка на прототип функции-конструктора, с помощью которой он создан.
3. prototype - независимый объект.