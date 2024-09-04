```js
class Cat extends Animal {
  constructor(options) {
    super(options);
    this.color = "Black";
  }

  voice() {
    console.log('I am Cat!');
  }

  get ageInfo() {
    return this.age * 7;
  }

  set ageInfo(newAge) {
	  this.age = newAge;
  }
}

const cat = new Cat({
	name: 'Cat',
	age: 7,
	hasTail: true,
	color: 'Black'
})

cat.ageInfo(); // 49 (7*7=49)
cat.ageInfo = 8;
cat.ageInfo(); // 56 (7*8=49)
```