### javascript中Iterable，Iterator三者的区别与联系  
#### Iterable(可迭代对象)  
Iterable是指有`[Symbol.iterator]`属性的对象，这个属性`obj[Symbol.iterator]`就是Iterator(迭代器)。也可以说该对象实现了`Symbol.itrator`方法。  
可迭代对象可以被`for ...of`循环遍历，我们最常进行迭代操作的可迭代对象就是Array，其实还有其他的可迭代对象，例如string,Set,Map,函数的arguments对象和NodeList对象等，这些对象都默认有`Symbol.iterator`属性。  

#### Iterator(迭代器)
Iterator必须有`next()`方法，他每次返回一个`{done: boolean, value:any}`对象，这里的`done: true`表明迭代结束，否则value就是下一个要迭代的值。  


#### 手写一个Iterator 
```
let range = {
    form: 1,
    to: 5
};

// for(let num of range)   num = 1,2,3,4,5
```
```
let range = {
  from: 1,
  to: 5,

  [Symbol.iterator]() {
    this.current = this.from;
    return this;
  },

  next() {
    if (this.current <= this.to) {
      return { done: false, value: this.current++ };
    } else {
      return { done: true };
    }
  }
};

for (let num of range) {
  alert(num); // 1, 然后是 2, 3, 4, 5
}
