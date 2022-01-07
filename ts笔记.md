**1、devDependencies和dependencies的区别**

`devDependencies`：中的依赖只参与项目开发，开发完成上线，并不需要打包到生产环境中，不需要部署到服务中

`dependencies`：中所有的依赖都会打包放在服务器上





//数组,写法一

```let arr: number[] = [1,2,3,4]```

//写法二,泛型

```let arr2: Array<number> = [1,2]```

//写法三,自动识别为number数组

```let arr3 = [1,2,3]```

//要想给数组添加任意类型的数据

```let arr4: any[] =  [1,"2", true]```

//注意any与以下差别,下面的写法，表示这个数组中只能存放字符串和number

```let arr5 = [1,"2"]```



//联合类型,可以是string和number类型

```let union: string | number```

//指定值,1,2,3

```let union2 :1 | 2 | 3```



//枚举类型 Enum

```
enum Color {

  red = "red",

  green = "green",

  blue = 7

}

let color = Color.red

console.log(color)//red
```

//void

```
function text(): void {

  console.log("noh");//没有返回值

}

```





//带参数的函数,必传两个参数

```
function fun(name: string, age: number){

  console.log(name, age);

}
```



//不确定的参数，加个？,

```
function fun2(name: string, age?:number){

  console.log(name, age);

}

```





//给参数设定默认值

```
function fun3(name: string, age: number = 0){

  console.log(name, age)

}
```



//interface 和 class, private public module、 getter、setter

```
interface IPoint {

  x: number,

  y: number,

  drawPoint: () => void,

  getDistance: (p:IPoint) => number,

}

class Point implements IPoint{

  x: number;

  y: number;

  constructor(x:number, y:number){

​    this.x = x;

​    this.y = y;

  }

  drawPoint = () => {

​    console.log(this.x, this.y);

  }

  getDistance = (p: IPoint) => {

​    return p.x + this.x

  }



}
```



//Generics 泛型,只能对number数组进行操作

```
let lastInArray = (arr: Array<number>) => {

  return arr[arr.length - 1];

}

const l1 = lastInArray([1,2,3]);
```





//让他既处理number, 也处理字符串,<T>表示动态类型

```
let lastInArray2 = <T>(arr: Array<T>) => {

  return arr[arr.length - 1];

}

const l2 = lastInArray2(["1","2"]);
```



