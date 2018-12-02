# proposal-class-modifiers
An ES proposal to add class-level inheritance modifiers.

## Motivation
The latest proposals for ES include data properties for `class`. If this encourages an increase in developers from class-based languages adopting ES for various uses, they will also want to be able to control the inheritability of the classes they write.

## Goal
The idea is to add `abstract` and `final` as `class` modifiers. These prefixes will prevent instantiation and inheritance respectively. They are mutually exclusive as the only type of class that is usefully neither instantiable nor inheritable is one with only static data and methods.

## Behavior

* `abstract` - causes `Reflect.construct` and `new` to throw an exception if `target.prototype === newTarget.prototype`.
* `final` - causes a derived `class` definition to throw an exception if it extends the target `class`.

### Examples
```js
abstract class Base {
    constructor() {
        console.log("abstract class 'Base' was instantiated!");
    }
}

new Base(); //throws exception

final class Derived extends Base {
    constructor() {
        constructor.log("final class 'Derived' was instantiated!");
    }
}

new Derived(); //Prints both console.log messages

class C extends Derived {}; //throws exception

abstract final class D {}; //throws exception
```
