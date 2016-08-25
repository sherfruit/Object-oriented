# 面向对象与高级

## 第一天

### 1.1复习

#### argument

```javascript
function count(a,b){
  console.log(arguments[0]+arguments[1]);
}
count(10,20)
```
> arguments是一个代表实参的对象，可以通过下标的方式来获取不同的实参，通过length属性获取实参的个数；因为arguments对象的使用方式很像数组，所以这种对象我们称之为伪数组。

#### throw

> 手动抛出错误，需要注意，一旦错误抛出，代码就停止运行了。

```javascript
 function fn(a) {
            console.log(a * 10);
            if (arguments.length !== 1) {
                // 错误抛出
                throw '请按照我的规则调用！';
            }
        }
```

#### debugger

> debugger相当于通过代码的方式添加调试断点。



### 1.2面向对象

> 什么是面向对象？
>
> 面向对象就是利用对象来解决问题，通常我们都是先找内置的对象解决问题，内置的解决不了，我们就得自己创建对象，然后利用这个对象解决问题。

### 1.3创建对象的方法

> 接来下，将一一例句对象的创建的方式，首先假如在**javascript**没有对对象进行支持的情况下创建对象，我们则需要这样做：

```javascript
 // 描述一条犬对象
        var name = '阿拉斯加';
        var age = 2;
        var color = '黑白相间';
        function eat() {
            console.log('各种吃！');
        }
        function run() {
            console.log('跑');
        }

        // 如果描述二条犬对象
        var name = '阿拉斯加';
        var age = 2;
        var color = '黑白相间';
        function eat() {
            console.log('各种吃！');
        }
        function run() {
            console.log('跑');
        }

        var name2 = '中华田园犬';
        var age2 = 10;
        var color2 = '土色';
        function eat2() {
            console.log('各种吃！');
        }
        function run2() {
            console.log('很能跑');
        }
```

> 书写过程很繁琐。

- 使用new Object的方式创建对象

```javascript
var aLaSiJia = new Object();
        aLaSiJia.name = '阿拉斯加';
        aLaSiJia.age = 2;
        aLaSiJia.color = '黑白相间';
        aLaSiJia.eat = function () {
            console.log('各种吃！');
        };
        aLaSiJia.run = function () {
            console.log('跑');
        };

        var zhonghuaTianyuanQuan = new Object();
        zhonghuaTianyuanQuan.name = '中华田园犬';
        zhonghuaTianyuanQuan.age = 10;
        zhonghuaTianyuanQuan.color = '土色';
        zhonghuaTianyuanQuan.eat = function () {
            console.log('各种吃！');
        };
        zhonghuaTianyuanQuan.run = function () {
            console.log('很能跑');
        };
```

> 过程依旧比较繁琐，因此可以使用字面量的方式创建对象，例如：

```javascript
 var aLaSiJia = {
            name : '阿拉斯加',
            age : 2,
            color : '黑白相间',
            eat : function () {
                console.log('各种吃！');
            },
            run : function () {
                console.log('跑');
            }
        };

        var zhonghuaTianyuanQuan = {
            name : '中华田园犬',
            age : 10,
            color : '土色',
            eat : function () {
                console.log('各种吃！');
            },
            run : function () {
                console.log('很能跑');
            }
        };
```

> 可以进一步封装成函数进行优化：

```javascript
 function getDog(name, age, color) {
            var dog = new Object();
            dog.name = name;
            dog.age = age;
            dog.color = color;
            dog.eat = function () {
                console.log('吃');
            };
            dog.run = function () {
                console.log('跑');
            };
            return dog;
        }

        var aLaSiJia = getDog('阿拉斯加', 2, '黑白相间');
        var zhonghuaTianyuanQuan = getDog('中华田园犬', 5, '土色');
        var aShiQi = getDog('哈士奇', 3, '黑白相间');
```

> 这样我们在需要创建新的对象，就不必每次都书写一次代码，直接可以调用函数。但是依旧不是最简洁的方式，因此最后我们可以通过构造函数的方式来创建对象。

- #### 什么是构造函数？

> 用来配合new创建对象的函数，我们给这种函数起了一个名字进行区分，这个名字就是构造函数，如果一个函数只当做构造函数使用，一般我们会把这个函数的名字首字母大写。*Object、Array、Date、Number、String*都是内置的构造函数，*Math*除外。



> 使用构造函数的方式创建对象：

```javascript
function Dog(name, age, color) {
            this.name = name;
            this.age = age;
            this.color = color;
            this.eat = function () {
                console.log('吃');
            };
            this.run = function () {
                console.log('跑');
            };
        }

        var aLaSiJia = new Dog('阿拉斯加', 2, '黑白相间');
        var zhonghuaTianyuanQuan = new Dog('中华田园犬', 5, '土色');
        var aShiQi = new Dog('哈士奇', 3, '黑白相间');
        aShiQi = 2;
```

> 因此在创建对象的时候更多是通过**new**的方式来创建对象。



## 1.4 类

- 什么是类？

> ES6之前没有类这个概念，这个概念来自于其他主流的面向对象编程语言。而在js当中，我们把构造函数看作是类。



> 类是对某一些具有相同特征或特性的对象的抽象描述，可以把类想象成是一个模板(模具)，通过这个模版可以创建N多个具体的对象。



### 1.5实例

- 实例的概念

  > 通过构造函数创建出来的对象，就叫这个构造函数的实例。


- 实例的类型

  > 和构造函数的名字有关；
  >
  > 一个实例他的具体类型，就是创建这个实例的构造函数的名字。

```javascript
 function Person() {

        }
        // xiaohong是Person类型的对象
        var xiaohong = new Person();

        // arr是Array类型的对象
        var arr = new Array();

        // date是Date类型的对象
        var date = new Date();
```

- 构造函数创建对象存在的问题，例如以下代码：

```javascript
 function Animal(name, age) {
            this.name = name;
            this.age = age;
            this.run = function () {
                console.log('都会动');
            }
        }

        var songShu = new Animal('松鼠', 3);
        var kaoLa = new Animal('考拉', 5);
        console.log(songShu.run == kaoLa.run);
```

> 每调用一次函数都会在内存中开辟一个新的空间，其中this.run=function(){console.log('都会动')}，是每一个对象都存在的属性方法，那么能不能把这个方法只创建一次，就可以让每一个构建出来的对象都拥有这个方法呢？



### 1.6原型

- 原型的概念：原型是函数的一个自带属性prototype，这个属性的值指向一个对象（因为存的是对象的指针）。
- 原型的作用：通过构造函数创建的对象，这个对象可以使用原型上的属性与方法；也就说原型可以让实例共享他的属性与方法。

```javascript
 // Person类
        function Person(name) {
            this.name = name;
            /*this.eat = function () {
                console.log('必须吃！！！');
            };*/
        }

        // 把eat方法加到Person的原型上
        Person.prototype.eat = function () {
            console.log('必须吃！！！');
        };

        // 创建两个实例
        var honghong = new Person('红红');
        var jiajia = new Person('佳佳');

        // 两个实例，都可以访问Person原型上的eat方法
        honghong.eat();
        jiajia.eat();
        console.log(honghong.eat == jiajia.eat);//true
```

> 通过将方法存入到prototype指向的对象上，可以让通过构建函数创建出来的对象都能继承这个方法。示意图如下：

 ![03原型(对应代码15)](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.29\资料\03原型(对应代码15).png)

#### __proto__

>这是一个属性，所有的对象都有这个属性，这个属性我们也叫他原型。

```javascript
function Dog(age) {
            this.age = age;
        }

        Dog.prototype.run = function () {
            console.log('可以跑');
        };

		var shaMo = new Dog(5);
		console.log(shaMo.__proto__); //{}
        console.log(shaMo.__proto__ == Dog.prototype); //true

		shaMo.run();
        console.log(shaMo.toString());
```

> 构造函数创建对象的四个步骤：

1. 自动创建出一个新对象
2. 初始化这个对象：给这个对象添加了一个__proto__ = 构造函数.prototype
3. 通过这个新对象调用构造函数
4. 返回新对象的地址

- __proto__ 是一个非标准的属性，不要在日常开发中使用。

> 对象属性的查找规则： 如果访问一个对象的属性，先会在自身上查找，如果没有，则根据__proto__对应的原型对象上去找，如果还没有找到，再根据这个对象的__proto__去找，一直找到Object.prototype。

- 原型的称呼问题：

> prototype这个属性，我们称之为原型属性，或者显式原型。
>
> __proto__这个属性，我们称之为原型对象，或者隐式原型。



> prototype只有函数拥有这个属性，__proto__所有对象都有这个属性，因为function本身就是函数，又是对象，所以他既有prototype，又有__proto__!



#### prototype和__proto__：

> 他们是两个不同的属性。



> 其中prototype是函数的属性，这个属性指向原型；
>
> 函数中prototype属性作用：将来的实例的__proto__属性会根据构造函数的prototype属性来定义。
>
> __proto__是对象的属性，这个属性也指向原型；
>
> 对象中__proto__属性作用：对象可以访问__proto__属性所指向的那个原型对象中的属性与方法。

- 思考1：

```javascript
 function A(){

    }
    function B(){

    }
    B.prototype.val=2;

    // a对象不能使用B类显式原型上的属性！
    // 因为a.__proto__ 没有指向 B.prototype。
    var a = new A;
    console.log(a.val);

    //所以要指向B
    var a = new B;
    console.log(a.val);
```

- 思考2：

```javascript
    function Dog(name){
        this.name=name;
    }
    Dog.prototype.MAX_AGE=24;

    var saMo=new Dog('萨摩');
    var zangao=new Dog('藏獒');

    saMo.MAX_AGE=20; //只是给自身添加了一个MAX_AGE属性
    console.log(zangao.MAX_AGE);//24
    console.log(saMo.MAX_AGE);//20

    Dog.prototype.MAX_AGE = 10; //修改要通过prototype来修改
    console.log(zangao.MAX_AGE);//10
    console.log(saMo.MAX_AGE);//20
```

 ![04对象属性修改(对应代码19)](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.29\资料\04对象属性修改(对应代码19).png)

- 对象属性的查找：

  > 先找自身，找不到就根据自身的__proto__属性去找，以此类推，一直找到Object.prototype。


- 对象属性的修改：

  > 如果修改一个对象的属性，那么只能修改自己的，不会影响其他对象。



#### constructor

> 所有的原生的原型，都有这个属性。这个属性的值存的是构造函数的地址(指针)。因为构造函数.prototype的值，可以被我们修改，修改之后，就不是原生原型了。

```javascript
        function Dog() {

        }
        // 构造函数.prototype可以被修改
        console.log(Dog.prototype);//object {}
        Dog.prototype = [];
        console.log(Dog.prototype); //[]
```

- constructor的作用

```javascript
function Dog() {

        }
        Dog.prototype.run = function () {
            console.log('跑');
        };

        var dog = new Dog();
        dog.run();

        // 可以获取对象的具体类型
        console.log(dog.constructor.name);

        // 动态修改原型的属性，尽量不要这么干，最好一次性在最初就定义好
        Dog.prototype.run = function () {
            console.log('飞起来跑');
        };
        dog.run();
```

 ![05constructor](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.29\资料\05constructor.png)

- 原型的补充

```javascript
 function Dog() {

            // 为了防止这段代码在创建对象时多次执行，
            // 所以加一个判断，提升性能优化内存
            if (!Dog.prototype.run) {
                Dog.prototype.run = function () {
                    console.log('跑');
                };
                Dog.prototype.eat = function () {
                    console.log('吃');
                };
            }
        }

        var dog = new Dog();
        dog.run();

        var dog2 = new Dog();
        dog2.eat();
```

- 继承

  > 一个对象可以使用本不属于自己的属性，那么就说这个对象继承了这些属性。主流的面向对象编程语言他们的继承是类与类之间的继承;在ES6之前，js的继承是对象与对象之间的继承。

```javascript
function Dog() {}
        Dog.prototype.MAX_AGE = 25;

        // 因为dog可以访问自身__proto__属性指向的对象的属性，
        // 我们就说dog继承自它的隐式原型。
        var dog = new Dog();
		console.log(dog.MAX_AGE);

        // 在js中，有一些其他继承方式，
        // 这些方式实际上只是一些编程技巧，
        // 这些编程技巧同样完成了继承定义的功能。
```



## 第二天

### 2.1   继承方式1

### 默认的原型继承：

```javascript
function Dog(name) {
            this.name = name;
        }

        Dog.prototype.run = function () {
            console.log(this.name + ' 跑');
        };

        // aFuAiGB 继承 Dog.prototype 指向的原型
        // aFuAiGB 继承 aFuAiGB.__proto__指向的原型(自己的隐式原型)
        // 通常我们说 对象 继承自 自己原型对象(隐式原型)
        var aFuAiGB = new Dog('阿富汗贵宾犬');
```

 ![02继承方式1的结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.31\资料\02继承方式1的结构.png)

### 2.2   继承方式2

#### 原型覆写：

```javascript
       function Animal(age) {
            this.age = age;
        }

        // 这是添加给类自己的属性，实例无法使用
        Animal.value = 10;

        // 对构造函数的原型属性进行覆写
        Animal.prototype = {
            // 这种方式，构造函数的原型上的constructor属性会丢失，
            // 最好自己手动补一下，不补也无大碍。
            constructor: Animal,
            eat: function () {
                if (this.age < 3) {
                    console.log('饭量比较小');
                }else {
                    console.log('饭量比较大');
                }
            },
            run: function () {
                if (this.age < 3) {
                    console.log('奔跳跑');
                }else {
                    console.log('正常奔跑');
                }
            }
        };

        var shuLan = new Animal(5);
        shuLan.eat();
        shuLan.run();
        console.log(shuLan.constructor);
        // undefined，无法访问类上的属性，
        // 只能访问自己的，或者继承的
        console.log(shuLan.value);
```

> 在覆写原型时，不要使用已经存在的对象

 ![03继承方式2的结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.31\资料\03继承方式2的结构.png)

### 2.3   继承方式3

### copy继承：

```javascript
// 实现copy继承，需要下面这个函数来完成
        function extend(obj1, obj2) {

            // 把obj2对象里的所有属性复制到obj1上
            for (var key in obj2) {
                obj1[key] = obj2[key];
            }
        }

        var o = {
            val : 10,
            age : 5
        };

        var obj = {
            color : 'red'
        };

        // 把o对象里面的属性复制到obj上
        extend(obj, o);
        console.log(obj.color);

        // copy之后，obj可以使用age属性了
        console.log(obj.age);
```

 ![04继承方式3的结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.31\资料\04继承方式3的结构.png)



### 2.4   继承方式4

#### copy加原型继承（extend）：

```javascript
var obj = {
            eat: function () {
                console.log('饭量比较小');
            },
            run: function () {
                console.log('正常奔跑');
            }
        };

        function Animal(age) {
            this.age = age;
        }

        // 把obj对象上的属性复制到Animal.prototype上
        extend(Animal.prototype, obj);

        Animal.prototype.run = function () {
            if (this.age < 3) {
                console.log('奔跳跑');
            }else {
                console.log('飞跑');
            }
        };

        var shuLan = new Animal(5);
        shuLan.run();
        obj.run();

```

 ![05继承方式4的结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.31\资料\05继承方式4的结构.png)

### 2.5   继承方式5

#### Object.create:

> 这个方法是一个内置的工厂函数。
>
> 语法：Object.create(传入要继承的对象);
>
>  return：返回一个新对象，新对象继承你传入的对象。

```javascript
var $ = {
            id : function (id) {
                return document.getElementById(id);
            },
            name : function (name) {
                return document.getElementsByTagName(name);
            }
        };

        // ES5才有了这个方法，所以IE8之前不支持
        // obj继承$(即obj.__proto__ == $)
        var obj = Object.create($);
        console.log(obj.id);
```

 ![06继承方式5的结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.31\资料\06继承方式5的结构.png)

### 2.6   继承方式6

### Object.create加原型的组合继承：

```javascript
       var $ = {
            id : function (id) {
                return document.getElementById(id);
            },
            name : function (name) {
                return document.getElementsByTagName(name);
            }
        };

        function Student(name) {
            this.name = name;
        }

        // 建议采用这种方式
        /*extend(Student.prototype, $);*/

        // 继承方式6的关键代码
        Student.prototype = Object.create($);

        // liXiaoLong继承Object.create创建的对象，
        // Object.create创建的对象继承$,
        // 也就是说liXiaoLong间接继承了$。
        var liXiaoLong = new Student('黎小龙');
        console.log(liXiaoLong.name);
        // 可以访问$对象上定义的id方法
        console.log(liXiaoLong.id);
```

 ![07继承方式6的结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\7.31\资料\07继承方式6的结构.png)

### 2.7   继承方式7

#### 原型组合式继承：

```javascript
function Person() {

        }

        Person.prototype.run = function () {
            console.log('跑');
        };

        function Student(name) {
            this.name = name;
        }

        // 建议这么做
        /*extend(Student.prototype, Person.prototype);*/

        /*Student.prototype = Object.create(Person.prototype);*/

        // 继承方式7的关键代码，原理类似与继承方式6
        Student.prototype = new Person();

        var liXiaoLong = new Student('黎小龙');
        // 可以访问Person上的run方法了
        liXiaoLong.run();
```



## 第三天

### 3.1   原型对象

```javascript
 		function Person() {}
        function Student() {}
```



>Person.prototype 自身是一个对象，它也有__proto__属性。
>
>也就是说它也有自己继承的对象，那么继承谁呢？通过观察，发现它继承的对象上有一个constructor属性，而拥有constructor属性的对象，都是原生的原型对象，而constructor属性标识了这个原型对象诞生于谁，也就是可以通过construcotor来确定一个原型对象的身份。
>
>结论：构造函数的原型，都继承Object.prototype。

 ![01重新画实例的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\01重新画实例的继承结构.png)



>通过访问Object.prototype，发现结果是null，说明Object.prototype是继承结构的终点，既然是终点，那么所有的对象都继承它。

```javascript
function Person() {}
        function Student() {}
        var xiaomei = new Person();
        var xiaofang = new Student();

        // 所有对象拥有的方法，可以添加到Object.prototype上。
        // 让代码稍微严谨一些
        if (!Object.prototype.itcast) {
            Object.prototype.itcast = '星期五';
        }
        console.log(xiaomei.itcast);
        console.log(xiaofang.itcast);
```

### 3.2   原型链：

>从对象开始，到Object.prototype结束，中间由__proto__连接起来的一系列对象，形象的称之为原型链。

- 研究原型链结构的方案：
  1. 先通过__proto__属性获取到对象继承的那个对象;
  2. 再通过查看继承对象的constructor属性，来确认该继承对象的出身。

#### 3.2.1字面对象的原型链

```javascript
 var obj = {};
        // 上面的写法相当于是 var obj = new Object();
        // 原型链结构 obj ==> Object.prototype ==> null

        /*
        * 通过观察发现，obj继承的对象是Object.prototype
```

 ![02字面量对象的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\02字面量对象的继承结构.png)

#### 3.2.2   数组原型链

```javascript
// 字面量数组形式
        var arr = [1,2,3,4];
        // 上面的写法相当于是 var arr = new Array();
        // arr的原型链：arr ==> Array.prototype ==> Object.prototype ==> null

        // 使用的是Array.prototype上定义的toString
        console.log(arr.toString());
```

 ![03字面量数组的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\03字面量数组的继承结构.png)

>对象的继承规律：

1. 对象的直接的继承关系，和该对象的类型有关;	

2. 构造函数.prototype.__proto__都是Object.prototype。

   ​

#### 3.2.3   复杂类型对象继承结构

```javascript
var reg = /abc/;
        // reg原型链： reg ==> RegExp.prototype ==> Object.prototype == null

        var date = new Date();
        // date原型链： date ==> Date.prototype ==> Object.prototype == null

        var strObj = new String();
        // strObj原型链： strObj ==> String.prototype ==> Object.prototype == null

        // Math 自己不是一个构造函数，自己本身就是一个对象
        // Math原型链： Math ==> Object.prototype == null

        // Date原型链： Date ==> Function.prototype ==> Object.prototype == null
```

 ![04Date实例的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\04Date实例的继承结构.png)

- 思考：

  ```javascript
   function Person() {}
          var xiaomei = new Person();

          function Student() {}
          Student.prototype = new Person();
          var xiaofang = new Student();
  ```

   ![05子类实例间接继承父类原型的结构图](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\05子类实例间接继承父类原型的结构图.png)

  ​

#### 3.2.4   函数原型链

>函数也是对象，因为函数式键值对的集合。

```javascript
function fn() {}
        fn.value = 10;
        console.log(fn.value);
```

> 因此：

```javascript
function fn() {}
        // fn原型链： fn ==> Function.prototype ==> Object.prototype ==> null

        // 函数也可以访问 Object.prototype 上的属性
        Object.prototype.it = 'IT';
        console.log(fn.it);

        // 因为Function.prototype上定义了一个toString方法，
        // 所以当函数使用toString时，优先访问到了Function.prototype上的toString
        console.log(fn.toString());
```

 ![06函数的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\06函数的继承结构.png)

- 函数加实例的原型链

  ```javascript
  // 画图练习，注：
          // 现在已经知道Person有两个和原型相关的属性了，
          // 都要画。
          function Person() {}
          var xiaomei = new Person();
  ```

   ![07函数加实例的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\07函数加实例的继承结构.png)

  ​

#### 3.2.5   Function的原型链

>通过之前的学习，已经知道函数继承Function.prototype;既然Function自己也是函数，那么继承谁呢？ 仍然是Function.prototype。

 仍然是Function.prototype。

```javascript
Function.__proto__  === Function.prototype
```

 ![08Function的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\08Function的继承结构.png)



>Object继承谁呢？
>
>Object也是函数，所以也继承Function.prototype。

 ![09Object的继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\09Object的继承结构.png)



>内置的String、Number、Boolean、Error、Function、Object、Date、Array、RegExp的几个构造函数自身的原型结构一样：

1. Function原型链 : Function ==> Function.prototype ==> Object.prototype == null
2. Object原型链 : Object ==> Function.prototype ==> Object.prototype == null
3. Date原型链 : Date ==> Function.prototype ==> Object.prototype == null
4. String原型链 : String ==> Function.prototype ==> Object.prototype == null
5. Array原型链 : Array ==> Function.prototype ==> Object.prototype == null

> 内置的9大构造函数的实例，的继承结构很相像。

- new String原型链 ：new String ==> String.prototype ==> Object.prototype == null
- new Date原型链 ：new Date ==> Date.prototype ==> Object.prototype == null

 ![10整合原型链](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\10整合原型链.png)

	>精简版继承结构

 ![11精简版继承结构](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.1\资料\11精简版继承结构.png)





### 3.3   instanseof

> instanceof运算符的运算规则和原型链有关：
>
> 语法：对象 instanceof 构造函数
>
> 判断左边对象的原型链结构中，有没有右边构造函数的显式原型

```javascript
 function Person() {}
        var xiaomei = new Person();

        // xiaomei即是Person类型的对象，又是Object类型的对象
        console.log(xiaomei instanceof Person);
        console.log(xiaomei instanceof Object);
        // xiaomei不是Function类型的对象
        console.log(xiaomei instanceof Function);

        // Person即是Function类型的对象，又是Object类型的对象
        console.log(Person instanceof Function);
        console.log(Person instanceof Object);
```



```javascript
function Person() {}
    var xiaomei = new Person();

    // 覆写Person的prototype属性
    Person.prototype = {
        run : function () {
            console.log('跑');
        },
        MAX_AGE : 200
    };

    var xiaofang = new Person();


    console.log(xiaofang instanceof Person); // true
    console.log(xiaomei instanceof Person); // false
```

```javascript
 function Person() {}
        var xiaomei = new Person();

        // 覆写Person的prototype属性
        Person.prototype = {
            run : function () {
                console.log('跑');
            },
            MAX_AGE : 200
        };

        console.log(xiaomei instanceof Person);//false
```



## 第四天

### 4.1	hasOwnProperty

>判断一个属性是不是自己的。
>
>语法：obj.hasOwnProperty(属性名);

```javascript
var myObj = {
            val : 1
        };

        Object.prototype.itcast = '星期五';

        console.log(myObj.hasOwnProperty('val')); // 是自己的属性，所以结果为true
        console.log(myObj.hasOwnProperty('itcast'));  // 继承的属性，所以结果为false
```



> 另外可以在使用extend的时候（将obj2的属性copy到obj1），运用hasOwnProperty去绑判定是否是obj2本身所拥有的属性，是的话就copy，如是继承过来的属性就不copy从而到达过滤的效果。

```javascript
// 实现copy继承的函数
        function extend(o, o2) {

            // 可以遍历出o2对象中我们自己添加的属性，
            // 以及o2继承的对象中，我们自己添加的属性
            for (var key in o2) {

                // 只把o2自己的属性copy到o上
                if (o2.hasOwnProperty(key)) {
                    o[key] = o2[key];
                }
            }

            return o;
        }

        var myObj = {
            val : 1
        };
        Object.prototype.itcast = '传智播客';
        // 打印出来的对象，没有itcast属性，因为被过滤掉了
        console.log(extend({}, myObj));
```

- 思考：

  ```javascript
   var arr = [];
          console.log(arr.hasOwnProperty('push')); // false
          console.log(Array.hasOwnProperty('push')); // false
          console.log(Array.prototype.hasOwnProperty('push')); // true

          console.log(Object.prototype.hasOwnProperty('hasOwnProperty')); // true
  ```

  > 数组的内置方法都是定义到Array.prototype上的，Object.prototype作为最高的，有hasOwnProperty这个属性。



### 4.2   propertyIsEnumerable

> 判断一个属性是不是可枚举的(内置属性不可枚举)；同时也判断属性是不是自己的(两个条件都是true才为true)；所以propertyIsEnumerable是hasOwnProperty的加强版本。
>
> 语法：obj.propertyIsEnumerable(属性名);

```javascript
 Object.prototype.itcast = '成长可期';
        console.log(Object.prototype.propertyIsEnumerable('hasOwnProperty')); // false
        console.log(Object.prototype.propertyIsEnumerable('itcast')); // true

        console.log(Object.prototype.hasOwnProperty('itcast')); // true
        console.log(Object.prototype.hasOwnProperty('hasOwnProperty')); // true
```



### 4.3   isPrototypeOf

>是不是另一个对象的原型对象。判断一个对象在不在另一个对象的原型链中。
>
>语法: obj.isPrototypeOf(obj);

```javascript
// 因为Object的原型链中存在Object.prototype和Function.prototype，所以为true
        console.log(Object.prototype.isPrototypeOf(Object));
        console.log(Function.prototype.isPrototypeOf(Object));
```

- isPrototypeOf与instanceof的区别
- prototype  原型属性，显式原型
- __proto__  原型对象，隐式原型
- 对象的原型对象，还有另外一种含义，指这个对象所有继承的对象。

  >isPrototypeOf 和 instanceof 公共点：
  >
  >都会判断一个对象，在不在另一个对象的原型链上。


>isPrototypeOf 和 instanceof 不同点：
>
>对象 instanceof 构造函数
>
>判断构造函数的原型属性，是不是左边对象的原型对象。
>
>判断构造函数的显式属性，是不是左边对象继承的对象。
>
>对象.isPrototypeOf(对象);
>
>判断左边对象，是不是参数对象继承的对象。

### 4.4   toLocaleString

>把对象转换为字符串，但是该方法会按照不同的对象类型转换;
>
>语法：obj.toLocaleString();
>
>返回值：字符串

```javascript
var date = new Date();
        console.log(date.toLocaleString());

        // 相当于是date调用了Object.prototype上的toLocaleString方法
        console.log(Object.prototype.toLocaleString.call(date));
        console.log(date.toString());
```





### 4.5 valueOf

>返回对象自身。
>
>语法：obj.valueOf()

```javascript
var obj = {
            val : 2
        };
        console.log(obj.valueOf()); //Object {val: 2}
```





### 4.6 toString

>返回一个类似与这样的字符串'[object 类名]'；该方法可以用来判断内置的10种对象的子类型。
>
>语法：obj.toString();



```javascript
  var date = new Date();
        var obj = {};
        var arr = [];
        var reg = /abc/;
        var fn = function () {};
        var str = new String();
        var num = new Number();
        var boo = new Boolean();
        var err = new Error();
        // 还有Math

        // 相当于是date调用Object.prototype上的toString方法
        console.log(({}).toString.call(date)); //[object Date]
        console.log(({}).toString.call(obj)); //[object Object]
        console.log(({}).toString.call(arr)); //[object Array]
        console.log(({}).toString.call(reg)); //[object RegExp]
        console.log(({}).toString.call(fn)); //[object Function]
        console.log(({}).toString.call(str)); //[object String]
        console.log(({}).toString.call(num)); //[object Number]
        console.log(({}).toString.call(boo)); //[object Boolean]
        console.log(({}).toString.call(err)); //[object Error]
        console.log(({}).toString.call(Math)); //[object Math]

        // 其他类型的对象，统一返回'[object Object]'
        function Person() {}
        console.log(({}).toString.call(new Person()));
        console.log(({}).toString.call(Person.prototype));
```

>判断数据类型一般使用typeof,但是它有缺陷，无法判断对象的具体类型，可以通过toString解决，最后还有null可以通过全等判断解决。

```javascript
  function getType(date) {
            var typeStr = typeof date;

            // number 、 string 、 boolean、 undefined
            if (typeStr === 'number' ||
                    typeStr === 'string' ||
                    typeStr === 'boolean' ||
                    typeStr === 'undefined') {
                return typeStr;
            }

            // function
            if (typeStr === 'function') {
                return 'Function';
            }

            // null
            if (date === null) {
                return 'null';
            }

            // object
            typeStr = ({}).toString.call(date);
            // 截取类名
            typeStr = typeStr.slice(8, -1);
            return typeStr;
        }
```





### 4.7   实例成员

>这个单词，是从类的角度来说的，在类中给实例添加的属性和方法，就叫实例成员。



> 什么是成员：就是对象上属性和方法的统称。

```javascript
// Person
        function Person(name, age) {
            // 在类的构造函数中，通常会有一些代码，用来给将来的实例添加属性。
            // 怎么添加了，通过this。

            // 给实例添加的name属性，就叫实例成员。
            this.name = name;
            this.age = age;

            // 这不是实例成员，因为val不是添加给实例的。
            var val = 1;
        }

        // 这上面添加的run方法，虽然不是直接添加给实例的，
        // 但是我们的本意是让实例来使用，所以也可以看作是实例成员。
        Person.prototype.run = function () {
            console.log('跑');
        };

```



### 4.8   静态成员(类成员)

> 添加到类自己的属性和方法，就叫静态成员或类成员。
>
> 需要注意，实例无法使用类成员。

```javascript
 // Dog类
        function Dog(name) {

            // 这是实例成员
            this.name = name;
        }

        // 这是静态成员或类成员
        Dog.MAX_AGE = 20;

        var dog = new Dog('泰迪');
        console.log(dog.name);  // '泰迪'
        console.log(dog.MAX_AGE); // undefined
```

- 什么情况下会把一些属性和方法定义为静态成员呢？

  > 属性：和类相关的属性，可以考虑添加类上。
  >
  > 方法：如果一个方法具有通用性，同时和实例无关，那么这个方法可以考虑添加到类上。



```javascript
// 构造函数
        function Jq(name) {
            this.name = name;
        }

        // 这个extend和实例有关，无法添加到类上，让其他地方使用。
        Jq.prototype.extend = function (o) {
            for (var key in o) {
                this[key] = o[key];
            }
        };

        var $ = new Jq('Jquery');
        $.extend({val : 1});
```

- 静态方法使用extend

```javascript
function Jq(name) {
            this.name = name;
        }

        // 给实例提供的extend方法
        Jq.prototype.extend = function () {

            // 这里的this，指实例，
            // 因为添加到原型上的方法，要为了让实例使用
            Jq.extend(this, arguments[0]);
        };

        // 这是暴漏给外面的extend方法
        Jq.extend = function (o, o2) {
            for (var key in o2) {
                o[key] = o2[key];
            }
        };

        var shiLi$ = new Jq('Jquery');

        // 静态方法具有通用性。
        // Jq上的extend方法可以服务与代码的其他地方，不再局限于Jq的实例了。
        var obj = {val:1};
        var o = {};
        Jq.extend(o, obj);
```



### 4.9  函数的几个属性

```javascript
 function count(a,b,c,d,e,f) {
            console.log(count.length);  // 形参的个数为6
            console.log(arguments.length); // 实参的个数为2
            console.log(arguments[0] + arguments[1]); //3
        }
        count(1,2)
        
        
 function add(a,b) {
            if (add.length !== arguments.length) {
                throw '参数个数不一致！';
            }
            console.log(a + b);
        }
		add(1);
```

1. name 函数的名字
2. prototype 函数的显式原型或者说是原型属性
3. __proto__ 函数的隐式原型或者说是原型对象
4. arguments  作为属性基本上要被废掉了，在函数内直接使用arguments即可
5. length 代表形参的个数
6. caller 调用该函数的函数

#### 4.9.1  caller

```javascript
function fn() {

            // 看看哪个函数调用的我
            console.log(fn.caller);
        }

        function fn2() {
            fn();
        }

        fn2();
        fn();
```

#### 4.9.2   in 运算符

>可以判断一个对象可不可以使用某个属性。
>
>语法：属性名  in  对象

```javascript
 var arr = [];
        Object.prototype.itcast = 'it';
        console.log('push' in arr); //true
        console.log('itcast' in arr); //true
```



#### 4.9.3   delete

> 删除对象的一个属性
>
> 语法：delete 属性
>
> 返回值：是否删除成功

```javascript
 var obj = {
            val : 2
        };

        delete obj.val;
        // obj里的val属性就没了
        console.log(obj);
```

> delete可以删除部分window中属性，比如 delete window.alert。
>
> delete可以删除全局下的变量，但是只能删除没有通过var关键字声明的全局变量。

```javascript
var a = 1;
        b = 2;

        delete a;  // 删除失败
        delete b;  // 删除成功
```



#### 4.9.4   Function

> 语法：new Function(arg1, arg2, arg3, arg4..., body);
>
> 所有的参数，都要求是字符串类型。
>
> 前面可以定义任意多个形参，最后一个参数代表函数的代码体。

```javascript
var fn2 = new Function('alert(2)');
        fn2();

        var fn3 = new Function('a', 'b', 'alert(a+b)');
        fn3(20,50);

        var str = 'var a = 1; console.log(a * 100);';
        var fn4 = new Function(str);
		fn4();
```



#### 4.9.5   eval

> eval(字符串代码),把字符串作为代码执行

```javascript
var str = 'var a = 1; console.log(a * 100);';
        eval(str);
```

- eval的使用方法：

  ```javascript
  <script id="tem" type="template">
          var a = 1;
          var b = 2;
          console.log(a + b);
      </script>

      <script>
          var temStr = document.getElementById('tem').innerHTML;
          eval(temStr);
      </script>
  ```



#### 4.9.6   总结构造函数的相关概念

````javascript
 // 这是构造函数，用来创建对象的
        // 这也是类，用来创建对象的
        // 这个函数和普通函数无异
        function Person(name, age) {

            // 这是实例成员，因为是添加给实例的属性
            this.name = name;
            this.age = age;
        }

        // 这也是实例成员，因为这是给实例使用的
        Person.prototype.run = function () {
            console.log('不同的年龄有不同奔跑方式');
        };
        /*
        * Person.prototype的作用：
        * 让实例继承它。
        *
        * 为什么要继承呢？
        * 为了共享Person.prototype上面的成员，这样可以节省内存。
        * */

        /*
        * Person.__proto__的作用：
        * 就是Person可以共享的对象，
        * 也就是让Person可以使用Function.prototype上定义的成员。
        * */

        /*
        * prototype和__proto__的微妙关系
        * 让实例的__proto__依据构造函数的prototype来初始化。
        * */
        var xiaomei = new Person('美', 16);
````



## 第五天

### 5.1   属性和方法

```javascript
 var obj = {
            // 这是属性
            a : 1,
            // 这是属性
            b : 2,
            // 这是属性、这也是方法
            fn : function () {}
        };

        // 如果对象的某个属性值，是一个函数，那么我们称这个函数为方法。
        // 所以，属性包含方法
```



### 5.2   预解析

> 在代码正式大规模解析之前，先解析一小部分代码。

- 声明的变量（变量声明提升）

  > 去找使用var声明的变量，但是var语句可能含有赋值表达式，只有声明的变量会被预解析，赋值表达式不会.

- 声明的函数（函数声明提升）

  > 只有声明式定义的函数才会预解析，被提升，表达式定义的函数不会。

**注意：预解析完成之后，会逐行正式解析(之前未预解析)过的代码。**



#### 5.2.1   预解析的第一部分：变量声明提升

> 预解析的特点是，可以在变量声明的前面使用这个变量。

- 变量声明提升注意点：

>声明变量时，可以给这个变量赋值，但是只有声明的变量会被预解析，而赋值表达式不会

```javascript
 // a存不存在，就看使用a报不报错，
        // 如果报错，说明没有a，不抱错，说明有
        console.log(a);
        var a = 1;
        console.log(a);

        /*
        * 上面的代码相当于这样：
        * var a;
        * console.log(a);
        * a = 1;
        * console.log(a);
        * */
```

#### 5.2.2   预解析的第二部分：函数声明提升

> 预解析的特点是，可以在函数声明的前面可以使用这个函数。

- 变量声明提升注意点：

  > 可以在函数声明的前面使用这个函数

  ```javascript
  		fn();
  		function fn(){
    			console.log(1);
  		}
  		fn();
  ```


- 函数表达式不会被预解析：

```javascript
 var f = function () {
            console.log(2);
        };
        f();
```

```javascript
(function fn() {
            console.log('自调函数也是函数表达式，不会预解析');
        })();
```

##### 	5.2.21   函数声明式

	>函数声明式的特点：

1. 必须以function关键字开头定义
2. 必须要有函数名
3. 要么定义在全局，要么直接嵌套在另一个函数中

```javascript
       // 函数声明式1(全局作用域下定义的)
        function fn() {}
```

```javascript

        (function fn() {

            // 函数声明式2(函数内定义的，并且没有其他嵌套规则，只直接嵌套在函数中)
            function fn2() {}
        }());
```

##### 	5.2.22   函数表达式

> 函数表达式的特点：

1. 开头一定不是以function关键字定义的
2. 函数名可有可无
3. 一定嵌套在其他代码块或语句或表达式

```javascript
        // 表达式1
        var fn = function f() {};

        // 表达式2
        (function pp() {})();

        // 表达式3
        alert(function fn() {});

        // 案例说这也是表达式,但是这种是特殊情况，浏览器会特殊对待
        if (true) {
            function fn() {}
        }
```

- 测试函数表达式中函数名是否会预解析

```javascript
		// 函数名不会预解析
        console.log(fn);
        var a = function fn() {
            console.log(1);
        }

        // 函数名不会预解析
       console.log(fn);
        var a = function fn() {
            console.log(1);
        }

        // 函数名不会预解析
        console.log(fn);
        Object.create(function fn() {});
		
		//都会报错：
		//VM84:1 Uncaught ReferenceError: fn is not defined(…)
```



#### 5.2.3   预解析规则

##### 5.2.31    变量重名

>如果存在两个重名的变量声明，会报错，只保留一个，可以理解为后面的被忽略了。

```javascript
 		console.log(a);
        var a = 1;
        var a = 2;
        console.log(a);
       
		/*
        *  var a;
        *  var a;  // 忽略，没必要在解析一个同名的变量了
        *  console.log(a);  //undefined
        *  a = 1;
        *  a = 2;
        *  console.log(a);  //2
        * */
```

##### 5.2.32    函数重名

> 如果存在两个重名的函数声明，不会报错，只保留后面声明的那个函数。(类似css规则，如果权重一样，后面的优先。)

```javascript
        fn();
        function fn() {
            console.log(100);  //忽略
        }
        function fn() {
            console.log(800);  //800;
        }
```

##### 5.2.33    变量与函数重名

> 如果存在变量声明和函数声明重名的情况，那么也不会报错，会保留函数。

```javascript
 		// 打印函数
        console.log(a);

        function a() {
            console.log(1);
        }
        var a = 1;

        // 打印1，因为赋值语句是在预解析之后执行的
        console.log(a);

		/*
		*   function a() {
        *    console.log(1);
        *   }
        *   var a  忽略
		*	console.log(a);
		*	a=1;
		*	console.log(a);
		**/
		
```

##### 5.2.34   类型声明函数写在代码块中

> 类似于函数声明式写在（非函数的代码块）中,这种情况，函数名会被预解析，函数体不会。

```javascript

        // 不会报错，是undefined，相当于预解析了函数名
        console.log(fn);
        if (true) {
            function fn() {}
        }
        // 打印函数
        console.log(fn);
		 /*
        * var fn;
        * console.log(fn);
        * 因为if判断结果是true，所以运行了 function fn() {}
        * console.log(fn);
        * */
```

```javascript
		// 不会报错，是undefined，相当于预解析了函数名
        console.log(fnn);
        {
            function fnn() {}
        }
```



#### 5.2.4   函数内页存在预解析

> 函数调用的售后，里面也存在预解析，预解析的规则和在全局下的预解析一样

```javascript
 function fn() {
            console.log(a);
            console.log(b);
            fn();

            var a = 1;
            var b = 2;
            function fn() {
                console.log(1);
            }

            console.log(a);
            console.log(b);
            fn();
        }

        /*
        * 全局下的预解析：
        * 预解析了函数fn
        * */

        fn();
        /*
        * fn调用时的预解析：
        * var a;
        * var b;
        * function fn(){ console.log(1); }
        * 开始正常执行：
        * console.log(a)
        * console.log(b)
        * fn()
        * a = 1;
        * b = 2;
        * console.log(a)
        * console.log(b)
        * fn()
        * */
```



### 5.3   作用域

>作用域说的就是变量的有效范围。
>
>如何检测一个变量的有效范围：在某个范围内，使用这个变量，不报错，说明这个范围下该变量存在。

#### 5.3.1   全局变量

>在代码的任何地方都可以访问的变量，就叫全局变量。
>
>如何定义一个全局变量：在函数外声明一个变量(var a = 1)，或者直接写一个变量(b = 2)。

```javascript
		var a = 1;
        if (true) {
            console.log(a);
        }
        (function fn() {
            console.log(a);
        }());
```

#### 5.3.2   局部变量

>只在部分代码中，可以访问的变量，就叫局部变量。局部变量只能在定义该变量的作用域以及子作用域中使用。
>
>如何定义一个局部变量：在函数内声明变量(var a = 1)，就是定义了一个局部变量。

```javascript
		 (function fn() {
            var a = 1;
            if (true) {
                console.log(a);
            }
            (function () {
                console.log(a);
            }());
        }());

        console.log(a);
```

#### 5.3.3  函数作用域

> 只有函数可以产生新的作用域，这种作用域规则，就叫函数作用域。

```javascript
function fn() {
            var a = 1;
        }
        console.log(b); // 可以访问，因为ES6之前只有函数可以产生新作用域。
        if (true) {
            var b = 1;
        }
```

- 块级作用域

  > 只要是代码块就可以产生新的作用域，这种作用域规则，就叫块级作用域。

```javascript
		// console.log(c);  // 不可以访问，因为let定义的变量拥有块级作用域。
        if (true) {
            // es6，新增的一种定义变量的方式，这种方式定义的变量拥有块级作用域。
            let c = 2;
        }
        console.log(c);  // 不可以访问，因为let定义的变量拥有块级作用域。
```

- 变量的声明周期

  >一个变量从定义开始，到消亡结束，中间存活的周期就叫变量的生命周期。

  1. 全局变量的生命周期：

     > 从变量定义开始，到页面被卸载时结束，中间存活的周期。生命周期太长，所以少用全局变量；同时全局变量用多了容易冲突。只要页面不卸载，就不消亡。

  2. 局部变量的生命周期：

     > 从变量定义开始，到函数执行完毕结束(这是一般情况，还存在二般情况)，中间存活的周期。

     ````javascript
     function fn() {
                 // 函数调用时产生，调用结束时消亡
                 var a = 2;
                 console.log(b);
             }

             // 调用两次fn，fn内产生的局部变量的a，不是同一个
             fn();
             fn();
     ````

 ![01函数调用多次产生多个作用域](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.4\资料\01函数调用多次产生多个作用域.png)



#### 5.3.4  词法作用域(静态作用域)

>在函数内，访问一个变量，先在函数内找(形参、局部变量)，如果找不到就去定义该函数的作用域中去找，以此类推，直到全局作用域。

**词法作用域的关键在：变量的查找与函数调用无关，和函数的定义有关。**

```javascript
function fn(b) {
            var a = 1;

            console.log(a);
            console.log(b);

            // 去定义fn的作用域中去找，
            // 找到了全局作用域，
            // 而全局作用域没有val，
            // 所以报错
            console.log(val);
        }

        (function () {
            var val = 2;
            fn(3);
        }());
```

- 函数作用域和块级作用域说的是，什么会产生新的作用域。

- 词法作用域说的是，变量的查找规则。

  > 在js中，采用的是函数作用域加词法作用域，不过在ES6的规则中，也采纳了块级作用域。

- 动态作用域(在其他编程语言)：

  > 在函数内，访问一个变量，先在函数内找(形参、局部变量)，如果找不到就去调用该函数的作用域中去找，以此类推，直到全局作用域。
  >
  > **动态作用域的关键在：变量的查找与函数调用有关，和函数的定义无关。**

#### 5.3.5   作用域链

>任何一个作用域，都可以访问上级作用域中的变量，那么从一个作用域开始，到全局作用域结束，以及中间所有的作用域串联起来形成作用域链。

```javascript
var a = 1;
        (function fn() {
            var b = 2;

            (function () {
                console.log(a);
            }());
        }());
```

 ![02作用域链](F:\传智播客前端\上课笔记\就业班\面向对象和框架\8.4\资料\02作用域链.png)

#### 5.3.6   自调函数的传参

```javascript
       // 自调函数也可以传参
        (function (a) {
            // 打印100
            console.log(a);
        }(100));

        // 如果一个函数有形参，该函数被调用时，
        // 会先给形参赋值。
        function fn(a) {
            console.log(a);
            var a = 21;
            console.log(a);
            /*
            * var a = 2;
            * var a // 忽略
            * console.log(a);
            * a = 21;
            * console.log(a);
            * */
        }

        fn(2);
```



## 第六天

### 6.1   闭包

- 广义闭包：

  > 闭包就是可以访问外界作用域中的变量的函数(在js中是函数，在ES6中代码块也可以)。

```javascript
  	    var a = 1;
        function fn() {  //广义中，函数就是闭包
            console.log(a);
        }
```

- 狭义闭包：

  >闭包就是可以访问外部局部变量的函数(如果存在快级作用域，闭包也可以是代码块)

```javascript
		// 从狭义上来说，这不是闭包
        function fn () {
            // 从狭义上来说，这是闭包
            function fn() {
            }
        }
```

#### 6.1.1   闭包的作用

> 可以访问非自己作用域的变量。

```javascript
// 广义闭包从闭包的角度上来说，没有任何使用价值
        var a = 1;
        function fn() {
            console.log(a);
        }
        console.log(a);

        // 狭义闭包就有价值了,因为它能访问的变量，不是任何地方都能访问的。
        function f() {
            var val = 2;

            function fn() {
                console.log(val);
            }
        }
        console.log(val);
```

#### 6.1.2   闭包的价值利用

````javascript
        (function () {
            var v = 1;
            function fn() {
                console.log(v);
            }
        }());

        // 全局下无法使用局部变量v
         console.log(v);
````

> 闭包可以解决的问题：在全局下通过闭包操作局部变量。
>
> 想：能不能在全局作用域下，通过闭包fn，来操作局部变量v呢？

```javascript
		//fn指的是fn1函数
      var fn = function(){
      var num=100;
      function fn1(){
          console.log(num);
      }
        fn1();
        return fn1; //将闭包暴露在全局
    }()
    console.log(fn);
```

```javascript
	//fn2指的是fn3函数
       var fn2=function(){
       var v=20;
       function fn3(){
           console.log(++v);
       }
        return fn3;
    }()

    fn2(); //通过调用返回出来的函数，就是fn3函数，可以对变量v进行操作。
    fn2(); // 特点，因为闭包fn3的存在，造成自调函数作用域中的变量v被保留了下来，无法释放。

	fn2=null;
	 // 把fn2改为null，那么自调函数作用域中的fn就无法使用了，
     // 就意味着没有函数依赖我，我就被回收了。
	
```

##### 6.1.21   闭包实现计数器

```javascript
	        var counter = (function () {
            var total = 0;  // 计数

            // 每次加1
            function add() {
                //total = total + 1;
                // 等价与上面的代码
                ++total;
            }

            // 看看数计到多少了
            function getTotal() {
                console.log(total);
            }

            // 返回一个对象，把闭包暴露到全局
            return {
                add: add,
                getTotal: getTotal
            };
        }());

        counter.add();
        counter.add();
        counter.getTotal();
```

#### 6.1.3   闭包实现缓存

- 全局的情况下实现缓存：

```javascript
 /*
        * 实现一个缓存
        * */
        var cache = {};
        // 给缓存中，存数据
        function setCache(key, value) {
            cache[key] = value;
        }
        // 在缓存中，取数据
        function getCache(key) {
            return cache[key];
        }

        // 正常缓存操作
        setCache('val', 10);
        console.log(getCache('val'));

        // 但是外界可以对cache随意的进行(不正常)的操作，
        // 比如删除一个属性，那么下次我获取缓存的数据时，就丢失了。
        delete cache.val;
        console.log(getCache('val'));

```

> 因为外界可以随意的对cache进行增删查改，所以我们要用闭包的特性改造上面的代码。

```javascript
		function getCache() {
            var cache = {};
            return {
                // 给缓存中，存数据
                setCache: function (key, value) {
                    cache[key] = value;
                },

                // 在缓存中，取数据
                getCache: function (key) {
                    return cache[key];
                }
            }
        }

        /*
        * getCache每调用一次，就会产生一个作用域，
        * 每个作用域中都会独自维护属于自己的cache对象。
        * */
        var cacheObj = getCache();
        cacheObj.setCache('v', 1);
        console.log(cacheObj.getCache('v'));

        var cacheObj2 = getCache();
        console.log(cacheObj2.getCache('v'));
```

> 接下来继续对上面代码进行改造升级：

```javascript
		function getCache(){
  		var cache={};
        return function (key,value){
  				if(arguments.length==2){   // 如果传2参数，就认为对方要存数据
  					cache[key]=value;
				}else if(arguments.length==1){  // 如果传1参数，就认为对方要取数据
  					return cache[key];
				}
			}  
		}
		var cacheFn = getCache();
		cacheFn('val',10);
		console.log(cacheFn('val'));
```

> 通过运用到实际案例中，对以上代码再改造：

```javascript
		  /*
        * 要求给缓存加一个限制，最多存3个key。
        * */

        function getCache() {
            var cache = {};

            // 记录存了多少key
            cache.total = 0;
            cache.MaxTotal = 3;

            return function (key, value) {

                // 如果传2参数，就认为对方要存数据
                if (arguments.length == 2) {

                    // 缓存数量没有达到最大值，才能进行存储
                    if (cache.total < cache.MaxTotal || cache.hasOwnProperty(key)) {

                        // 如果之前没有这个key，才能加加
                        if (!cache.hasOwnProperty(key)) {
                            cache.total++;
                        }
                        cache[key] = value;
                    }
                }

                // 如果传1参数，就认为对方要取数据
                else if (arguments.length == 1) {
                    return cache[key];
                }
            };
        }

        var cacheFn = getCache();
        cacheFn('nba', '美国');
        cacheFn('nba', '美利坚合众国');
        cacheFn('cba', '中国');
        cacheFn('cba', '中华人民共和国');
        cacheFn('tba', '牛国');
        cacheFn('aba', '天国');
        cacheFn('tba', '牛不落帝国');
        console.log(cacheFn('nba'));
        console.log(cacheFn('cba'));
        console.log(cacheFn('tba'));
        console.log(cacheFn('aba'));
```

#### 6.1.4   闭包练习

```javascript
		 /*
     * 需求，有一个Person类，
     * 要求创建一个Person实例，
     * 我们就要记录一下，
     * 最终可以通过记录获取总人数。
     * */

    //记录总人数
    var personCount=0;
   //person类
   function Person(name){
       //实例成员
       this.name=name;
        // 每创建一个人，就让总人数++
        personCount++;
    }

    var xiaomei = new Person('小美');
    var xiaofang = new Person('小芳');
    var xiaojiaojiao = new Person('小娇娇');
    var xiaojiangjiang = new Person('小江江');
    console.log(personCount);
```

> 练习：把上面的代码进行改造，让外界无法随意修改personCount值。

```javascript
	function getPerson(){
  	var personCount=0;
    function Person(name){
  		this.name=name;
      	personCount++;
	}  
    function getPersonCount (){
  		return personCount;
	}  
    return {
  		Person:Person,
      	getPersonCount:getPersonCount
	}  
}
		var PersonObj = getPerson();
        var xiaomei = new PersonObj.Person();
        console.log(PersonObj.getPersonCount());

```

因为getPersonCount与Persons是密切相关的，可以将其作为后者的静态成员添加到类当中：

```javascript
var Person = function getPerson() {
            // 记录总人数
            var personCount = 0; // 私有变量：只能在类中使用的变量叫私有变量。

            // Person类
            function Person(name) {

                // 实例成员
                this.name = name;

                // 每创建一个人，就让总人数++
                personCount++;
            }

            // 静态成员，记录总人数
            Person.getPersonCount = function () {
                return personCount;
            };

            return Person;
        }();

        var xiaomei = new Person();
        var xiaofang = new Person();
        console.log(Person.getPersonCount());
```

#### 6.1.5  闭包保存状态

>一个变量，在存储不同的值的时候，每一个值，都认为是这个变量的一个状态.

```javascript
		  // 循环的时候，马上使用变量i
        for (var i = 0; i < 5; i++) {
            console.log(i); //打印出来的是0，1，2，3，4
      
        // 或一会再使用变量i
        for (var i = 0; i < 5; i++) {

            function fn() {
                console.log(i); //打印出来的是5，5，5，5，5，因为循环是瞬间完成的
            }
            setTimeout(fn, 300);

            // 这里的代码和上面等价
            setTimeout(function () {
                console.log(i); //打印出来的是5，5，5，5，5，因为循环是瞬间完成的
            }, 300);
        }

```

>想在300毫秒后，执行的回调函数，分别打印0、1、2、3、4,可以通过闭包来实现

```javascript
		for (var i = 0; i < 5; i++) {
            (function (i) { //闭包保存传进来的每一个i
                setTimeout(function () {
                    console.log(i);
                }, 1000);
            }(i));
        }
```

> 也可以用另外的写法：

```javascript
		function getfn(i){ //闭包保存传进来的每一个i
  		return function(){
  			console.log(i);
			}
		}
		for(var i=0;i<5;i++){
            // 这里给setTimeout传入的第一个参数，
            // 是getFn函数的调用结果。
  			setTimeout(getfn(i),1000)
		}
```

- 应用例子：

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Title</title>
  </head>
  <style>
      li {
          margin-top: 5px;
          height: 20px;
          background-color: red;
      }
  </style>
  <body>
      <ul>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
          <li></li>
      </ul>
      <script>
          /*
          * 需要，点击不同的li，打印对应的角标值
          * */

          // 这种做法，可取
         /* var lis = document.getElementsByTagName('li');
          for (var i = 0; i < lis.length; i++) {
              lis[i].index = i;
              lis[i].onclick = function () {
                  console.log(this.index);
              }
          }*/

          // 这种做法，没有上的好
          var lis = document.getElementsByTagName('li');
          for (var i = 0; i < lis.length; i++) {
              (function (i) {
                  lis[i].onclick = function () {
                      console.log(i);
                  }
              }(i));
          }
      </script>
  </body>
  </html>
  ```



## 第七天  

### 7.1   同步异步

> 同步：

```javascript
		var a = 1;
        function fn() {
            console.log(1);
        }
        // 调用fn，fn马上执行，这就是同步
        // 同步和代码的执行以及调用顺序是保持一致的
        fn();
        function fn2(cak) {
            cak();
        }

        // 调用fn2，传入fn，然后fn2里面马上调用fn，
        // 所以这里传入的回调函数是同步执行的。
        fn2(fn);
```

> 异步：
>
> 异步执行的代码，调用顺序以及时间不能把控.
>
> 1. 传入定时器的回调函数是异步执行的
> 2. 所有事件触发的回调函数(事件触发函数)是异步执行的

```javascript
		// 这个事件触发函数，什么时候执行，不能确定，这就是异步的。
        window.onload = function () {
            console.log(1);
        };
        // 传入给定时器的回调函数，不是马上执行，这也是异步的。
        setTimeout(function () {
            console.log(1);
        }, 500);
```

> 同步和异步执行对比：

```javascript
		for (var i = 0; i < 3; i++) {
            // log函数是同步执行的
            console.log(i);

            // 传入fn2的回调函数，是同步执行的，
            // 所以每一次循环，回调都会马上执行。
            fn2(fn);

            // 传入定时器的回调函数，是异步执行的，
            // 只有循环结束后，回调才会执行(具体是不是循环结束后，马上执行？不一定)。
            setTimeout(function () {
                console.log(i);
            }, 500);

            // 自调函数是同步执行的，
            // 也就是说每一次循环，自调函数都是执行一次，
            // 每次执行时，for循环中的i都不同
            (function (i) {
                setTimeout(function () {
                    console.log(i);
                }, 500);
            }(i));
        }
```

### 7.2   函数调用的四种方式

#### 	7.2.1   函数调用模式

```javascript
		// 函数调用模式  ==> 函数名()  ==> this指向window
        /*function fn() {
            console.log(this);  // this指向window
        }
        fn();*/
        /*-------------------------------------*/
        var obj = {
            fn : function () {
                console.log(this);
            }
        };
        var fn = obj.fn;
        fn();   // this指向window，因为是函数名直接调用
```

#### 	7.2.2   方法调用模式

```javascript
		// 方法调用模式  ==> 对象.函数名()  ==> this指向对应的对象
        /*var obj = {
            fn : function () {
                console.log(this);
            }
        };
        obj.fn();  // 方法调用，this指向对象obj*/

        /*------------------------------------------------------*/
        function fn() {
            console.log(this);
        }
        var o = {};
        o.fn = fn;
        o.fn();  // 方法调用，this指向对象o
```

#### 	7.2.3   构造函数调用模式

```javascript
		// 构造函数调用模式  ==> new 函数名()  ==> this指向new新创建出的实例

    /*    function Person(name) {
            this.name = name;
            console.log(this);
        }
        var xiaomei = new Person('小美');
        var xiaofang = new Person('小芳');*/

        /*------------------------------------------------*/
        var obj = {
            fn: function (age) {
                this.age = age;
                console.log(this);
            }
        };
        var o = new obj.fn(16); // 构造函数调用模式，this指向实例
```

#### 	7.2.4   间接调用模式

```javascript
		
        function fn() {
            console.log(this);
        }

        // 通过函数.call(),在call中会再次调用fn，并改变fn的this指向。
        fn.call([]);
        fn.call({});
        fn.apply(/abc/);

        // 下面了解即可
        fn.apply(); // 指向全局
        fn.apply(null); // 指向全局
        fn.apply(undefined); // 指向全局

        fn.call(1);  // 指向数字1的包装对象
        fn.call('string'); // 指向字符串'string'的包装对象
```

>call、apply这两函数是定义在Function.prototype上的，说明所有的函数都可以使用这两个方法。

**call和apply的共同作用是：改变函数调用时的this指向。**

##### 	7.2.41   call与apply的借用原理

```javascript
		// 给数组扩展一个方法，该方法遍历数组中的元素
        Array.prototype.forArr = function () {
            console.log(this);  // 哪个数组调用我，this就指向那个数组
            for (var i = 0, len = this.length; i < len; i++) {
                console.log(this[i]);
            }
        };

       /* var arr = [1,2,3,4];
        arr.forArr();*/

        // 定义一个伪数组对象
        var argus = {
            0: 10,
            1: 20,
            2: 30,
            a: 2,
            b: 3,
            length: 3
        };
        // 通过call借用数组原型上的forArr方法，来遍历伪数组
        // 通过call或者apply借用的方法，里面一定是和this相关的操作，否则没有什么意义。
        Array.prototype.forArr.call(argus);
```

- 实践：

  ```javascript
  		 var argus = {
              0: 10,
              1: 20,
              2: 30,
              a: 2,
              b: 3,
              length: 3
          };

          // 通过数组的push方法，给伪数组添加值
          Array.prototype.push.call(argus, 5);
          console.log(argus);

          // 通过数组的pop方法，删除伪数组的最后一个值
          Array.prototype.pop.call(argus);
          console.log(argus);
  ```

  ##### 7.2.42   call和apply具体语法

  > call


  > 语法：函数名.call(this指向, arg1, arg2, arg3...);
  >
  > 上面的做法，传参相等于：函数名(arg1, arg2, arg3...)
  >
  >  注意，传给call的第一个参数，用来设置函数调用时的this指向，并不会作为参数传给函数.

```javascript
		function fn() {
            console.log(arguments);
        }

        // 把1和2传给fn了
        fn.call([1], 1, 2);

```

- apply

  > 语法：函数名.apply(this指向, [arg1, arg2, arg3...]);
  >
  > 上面的做法，传参相等于：函数名(arg1, arg2, arg3...)
  >
  > 注意，传给apply的第一个参数，用来设置函数调用时的this指向，并不会作为参数传给函数.另外，传给apply的第二个数组参数，apply会自动铺开传给函数。

```javascript
		function fn() {
            console.log(arguments);
        }

        // 把数组铺开传给fn，相当于传了5和9
        fn.apply({}, [5, 9]);
```

##### 7.2.43  call和apply传this指向问题

```javascript
		var obj = {
            fn : function () {

                // 这里的this指向obj，
                // 所以这句代码的含义调用fn2函数，
                // 并指定fn2函数中的this指向obj
                fn2.call(this);

                // 上面的代码，相当于这样
                // fn.call(obj);
            }
        };
        function fn2() {
            console.log(this);  // 最终this指向obj
        }
        obj.fn();*/

        /*----------------------------------------------*/

        var obj = {
            fn : function () {

                // 这里的this指向数组，
                // 所以这句代码的含义调用fn2函数，
                // 并指定fn2函数中的this也指向数组
                fn2.call(this);

                // 上面的代码，相当于这样
                // fn.call(那个数组);
            }
        };
        function fn2() {
            console.log(this);  // 最终this指向数组
        }
        obj.fn.apply([1,2,3,4]);
```

> 属性继承：

```javascript
		function Person(name, age) {
            this.name = name;
            this.age = age;
        }

        function Student() {

        }

        //创建一个Student实例
        var xiaofang = new Student();

        // 这个实例，没有任何属性
        console.log(xiaofang);

        // 但是这个学生实例，也是人，
        // 也应该有人类的一些属性，
        // 所以通过call借用了一下Person构造函数，
        // 来给自己添加点人都有的属性
        Person.call(xiaofang, '小芳', 18);

        // 现在这个实例，就有name和age属性
        console.log(xiaofang);

        // 小小也想有人的那些属性，他也得通过call调用一下Person构造函数
        var xiaoxiao = new Student();
        Person.call(xiaoxiao, '小小', 18);

```

> 代码改进：

```javascript
		
        // 通过上面的例子，推出这里的改进
        function Person(name, age, sex) {
            this.name = name;
            this.age = age;
            this.sex = sex;
        }

        function Student(name, age, sex) {
            // 借用父类构造函数，给子类的实例添加属性
            // 业界有些人，把这称之为属性继承
            Person.call(this, name, age, sex);

            // 这中写法和上面无异，相当于上面的简写。
            // Person.apply(this, arguments);
        }

        //创建一个Student实例
        var xiaofang = new Student();
        var xiaohong = new Student();
```



##### 7.2.44  bind 

	>bind也是Function.prototype上定义的函数


> 语法：函数名.bind(指定函数的this指向);
>
> 返回值：返回一个新函数(相当于是之前的函数的一个封装)，新函数执行的this，指向你传入的this

```javascript
		function fn() {
            console.log(this);
            console.log(100);
        }

        // 返回的函数f，相当于是fn，
        // 但是这个函数，无论怎么调用，
        // this都指向传给bind函数的对象
        var f = fn.bind([1,2,3]);
        f();

        /*------------------------------------------------*/

        // 把f函数添加到对象obj上
        var obj = {
            f: f
        };
        // 通过方法模式调用函数f，
        // 发现f里的this仍然指向当初传给bind函数的数组
        obj.f();
```

#### 7.2.5   构造函数的返回值

>如果构造函数里，返回的是基本数据类型则忽略；如果返回的是引用数据类型(对象)则采纳，会把实例覆盖掉。

```javascript
	function Person(name, age) {
            this.name = name;
            this.age = age;
            return [1,2,3];
        }

        // 最终小美变成了数组
        var xiaomei = new Person('小美', 16);
        console.log(xiaomei);
```

#### 7.2.6   自调函数

```javascript
		// 沙箱模式
        // 命名空间

        /*
        * 好处：
        * 防止全局变量污染。
        * */
        (function (global) {

            var val = 2;

            global.fn = function () {
                return val;
            }
        }(window));

        console.log(fn());
```

### 7.3   递归

> 一般都说函数调用函数自己，就叫递归。

```javascript
		// 这种只有递，没有归，相当于死循环
        function fn() {
            fn();
       }

```

> 简单的递归：

```javascript
		var val = 10;
        function fn() {
            val--;
            if (val > 0) {
                fn();
            }
        }
```

> 编写递归的两个要点：

1. 找到临界条件(结束递归的条件，一般是return语句)；
2. 解决一个问题，尽量的把这个问题拆分细化，如果发现解决后面的小问题，需要使用前面已经解决的结果，并且规律一致，那么就可以考虑转换称递归的形式。

> 例子：次幂

```javascript
		/*
        * 2的几次幂：
        * 2^0 = 1
        * 2^1 = 2^0 * 2 = 2
        * 2^2 = 2^1 * 2 = 4
        * 2^3 = 2^2 * 2 = 8
        * */
       // 递归获取2的几次幂
       
        function fn(n) {
            if (n === 0) {
                return 1;
            }
            return fn(n - 1) * 2;
        }
        console.log(fn(5));

        /*
         * m^0 = 1
         * m^1 = m^0 * m
         * m^2 = m^1 * m
         * m^3 = m^2 * m
         * */
        // 递归获取任意数的几次方
       function fn(m, n) {
            if (n === 0) {
                return 1;
            }
            return fn(m, n - 1) * m;
        }
        console.log(fn(10, 6));
```

> 阶乘：

```javascript
		 /*
        * 计算阶乘：
        * 0! = 1
        * 1! = 0! * 1
        * 2! = 1! * 2
        * 3! = 2! * 3
        *
        * 1、1、2、6、24、120、720
        * */

        // 计算几的阶乘
        function f(n) {
            if (n === 0) {
                return 1;
            }
            return f(n - 1) * n;
        }

        for (var i = 0; i < 10; i++) {
            console.log(f(i));
        }
```

> 斐波那契数列:

```javascript
		/*
        * fibonacci 斐波那契数列
        * 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55
        *
        * fib(0) = 0
        * fib(1) = 1
        * fib(2) = fib(1) + fib(0)
        * fib(3) = fib(2) + fib(1)
        * */

        // 用来统计fib函数调用的次数
        var total = 0;

        // 获取斐波那契数列的递归实现
        function fib(n) {
            total++;

            if (n === 0) {
                return 0;
            }
            if (n === 1) {
                return 1;
            }

            return fib(n - 1) + fib(n - 2);
        }

        /*for(var i = 0; i < 10; i++) {
            console.log(fib(i));
        }*/

        console.log(fib(4));
        console.log(total);
```

