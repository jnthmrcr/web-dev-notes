# Property Methods
Objects can have a special type of property, called a method.

Methods are properties that are functions. This adds different behavior to an object.
```javascript
let duck = {
  name: "Aflac",
  numLegs: 2,
  sayName: function() {return "The name of this duck is " + duck.name + ".";}
};
duck.sayName();
```

# this
`this` refers to the object that the method is associated with
```javascript
let duck = {
  name: "Aflac",
  numLegs: 2,
  sayName: function() {return "The name of this duck is " + this.name + ".";}
};
```

# constructors
Constructors are functions that create new objects. They define properties and behaviors that will belong to the new object. Think of them as a blueprint for the creation of new objects.
```javascript
function Bird() {
  this.name = "Albert";
  this.color = "blue";
  this.numLegs = 2;
}
```
- Constructors are defined with a capitalized name to distinguish them from other functions that are not constructors.
- Constructors use the keyword this to set properties of the object they will create. Inside the constructor, this refers to the new object it will create.
- Constructors define properties and behaviors instead of returning a value as other functions might.

# new
```javascript
function Bird() {
  this.name = "Albert";
  this.color  = "blue";
  this.numLegs = 2;
}
let blueBird = new Bird();
```

Notice that the `new` operator is used when calling a constructor. This tells JavaScript to create a new instance of Bird called blueBird

can pass in arguments to constructors 
```javascript
function Bird(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}
```
# instanceof
`instanceof` allows you to compare an object to a constructor, returning true or false based on whether or not that object was created with the constructor.
```javascript
let Bird = function(name, color) {
  this.name = name;
  this.color = color;
  this.numLegs = 2;
}

let crow = new Bird("Alexis", "black");

crow instanceof Bird; // true

let canary = {
  name: "Mildred",
  color: "Yellow",
  numLegs: 2
};

canary instanceof Bird; // false
```

# Own Properties
in the previous example, `name` and `numLegs` are called own properties, because they are defined directly on the instance object. That means `crow` has its own separate copy of these properties. In fact every instance of `Bird` will have its own copy of these properties.
```javascript
let ownProps = [];
for (let property in duck) {
  if(duck.hasOwnProperty(property)) {
    ownProps.push(property);
  }
}
console.log(ownProps); // ["name", "numLegs"]
```

# Prototype Properties
Properties in the `prototype` are shared among ALL instances of an object.
```javascript
Bird.prototype.numLegs = 2;
console.log(duck.numLegs); // 2
console.log(canary.numLegs); // 2
```
all instances automatically have the properties on the `prototype`, think of a `prototype` as a "recipe" for creating objects. Note that the `prototype` for `duck` and `canary` is part of the `Bird` constructor as `Bird.prototype`. Nearly every object in JavaScript has a `prototype` property which is part of the constructor function that created it.
> ffs its `static` fields with extra steps. i think???

Own properties are defined directly on the object instance itself. And `prototype` properties are defined on the `prototype`
``` javascript
function Dog(name) {
  this.name = name;
}
Dog.prototype.numLegs = 4;

let beagle = new Dog("Snoopy");

let ownProps = [];
let prototypeProps = [];

for (let prop in beagle) {
  if (beagle.hasOwnProperty(prop)){
    ownProps.push(prop);
  } else {
    prototypeProps.push(prop);
  }
}

console.log(ownProps); // 'name'
console.log(prototypeProps); // 'numLegs'
```

adding more than a few properties is a pain... A more efficient way is to set the `prototype` to a new object that already contains the properties. This way, the properties are added all at once:

```javascript
Bird.prototype = {
  numLegs: 2, 
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```

## Constructor Property
```javascript
let duck = new Bird();
let beagle = new Dog();

console.log(duck.constructor === Bird); // true
console.log(beagle.constructor === Dog); // true
```
Note that the `constructor` property is a reference to the constructor function that created the instance. The advantage of the `constructor` property is that it's possible to check for this property to find out what kind of object it is.

Since the `constructor` property can be overwritten it’s generally better to use the `instanceof` method to check the type of an object.

manually setting the prototype erases the constructor property. To fix this, whenever a prototype is manually set to a new object, remember to define the constructor property:
```javascript
Bird.prototype = {
  constructor: Bird,
  numLegs: 2,
  eat: function() {
    console.log("nom nom nom");
  },
  describe: function() {
    console.log("My name is " + this.name); 
  }
};
```

## isPrototypeOf()
an object inherits its `prototype` directly from the constructor function that created it. 
```javascript
function Bird(name) {
  this.name = name;
}
let duck = new Bird("Donald");
Bird.prototype.isPrototypeOf(duck); // true
```

All objects in JavaScript (with a few exceptions) have a `prototype`. Also, an object’s `prototype` itself is an object. Because a `prototype` is an object, a `prototype` can have its own `prototype`!

> shut the fuck up. please. just. shut the fuck up

> i dont understand this and its making me mad, im just copying whats written here
```javascript
Object.prototype.isPrototypeOf(Bird.prototype);
```
How is this useful? You may recall the `hasOwnProperty` method from a previous challenge:
```javascript
let duck = new Bird("Donald");
duck.hasOwnProperty("name");
```
The `hasOwnProperty` method is defined in `Object.prototype`, which can be accessed by `Bird.prototype`, which can then be accessed by duck. This is an example of the prototype chain. In this prototype chain, `Bird` is the supertype for `duck`, while `duck` is the subtype. `Object` is a supertype for both `Bird` and `duck`. `Object` is a supertype for all objects in JavaScript. Therefore, any object can use the `hasOwnProperty` method.
```javascript
function Dog(name) {
  this.name = name;
}
let beagle = new Dog("Snoopy");
Dog.prototype.isPrototypeOf(beagle);  // yields true
Object.prototype.isPrototypeOf(Dog.prototype); // true
```
> dont like this, should use actual classes with static fields. fuck.

# Don't Repeat Yourself (DRY) or what you need to repeat when the interviewer asks "so do you know what object oriented is?"
dont do this:
```javascript
Bird.prototype = {
  constructor: Bird,
  describe: function() {
    console.log("My name is " + this.name);
  }
};

Dog.prototype = {
  constructor: Dog,
  describe: function() {
    console.log("My name is " + this.name);
  }
};
```
instead create a supertype that contains the common method
```javascript
function Animal() { };

Animal.prototype = {
  constructor: Animal, 
  describe: function() {
    console.log("My name is " + this.name);
  }
};

Bird.prototype = {
  constructor: Bird
};

Dog.prototype = {
  constructor: Dog
};
```
frankly im more inclined to enable this type of stuff via interfaces but who knows if javascript likes that
> wait, where is it defined that dog and bird are subtypes of animal? what???

# inheritance
> wait. wtf. just. why not mention this with DRY
```javascript
function Animal() { }

Animal.prototype = {
  constructor: Animal,
  eat: function() {
    console.log("nom nom nom");
  }
};

let duck = Object.create(Animal.prototype);
let beagle = Object.create(Animal.prototype);
// use Object.create not new Animal();

function Dog() { }

Dog.prototype = Object.create(Animal.prototype);
let beagle = new Dog(); // beagle inherits all of Animal's properties, including the eat method.
```
When an object inherits its prototype from another object, it also inherits the supertype's constructor property.
```javascript
function Animal() { }
function Bird() { }
function Dog() { }

Bird.prototype = Object.create(Animal.prototype);
Dog.prototype = Object.create(Animal.prototype);
// manually change constructors
Bird.prototype.constructor = Bird;
Dog.prototype.constructor = Dog;

let duck = new Bird(); // Bird not Animal
let beagle = new Dog(); // Dog not Animal
```