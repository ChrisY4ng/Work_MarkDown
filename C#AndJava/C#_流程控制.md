[TOC]

# C# 流程控制

控制流程语句是在每一种语言中都包含的。它可以控制程序的执行逻辑，可以使用计算机的特性--重复执行某一个动作或代码,也可以在执行一段程序之后做出相应的跳转。C#中三种类型的控制流程语句，分别是条件判断语句(if)、循环控制语句(for、while、do while、foreach),条件选择语句(switch)和跳转语句(continue、break、return、goto)。

## 条件判断

C#中的条件判断语句只有if，在if后加入condition，"运行时"会判断condition是为True还是False，若为True则执行相应的代码块，为False则执行相应的代码块。并且可以在if语句之后附加else if或者else语句来增加条件判断的选择。如下举例说明：<br>

```C#
if(condition){
    代码块1
}else 
    if(condition2){
        代码块2
    }else{
        代码块3
    }
```

## 循环控制

循环控制有四种相应的语句可以选择，其中也包含一定的差异。下面主要来讨论一下有关的差异。

### for循环与foreach循环

*在知道要循环的次数，或者要用到循环中的计数器时，推荐使用for循环*
for循环控制语句的循环头中可以加入三个部分，第一部分为声明部分；第二部分为循环主体的执行条件判断语句，第三部分为描述更新循环变量的语句。当然，这三个部分都可以省略。三个部分都省略后为死循环语句(会一直循环执行)，需要在循环体中加入跳转语句来避免死循环。这三个部分的执行步骤是：**声明在循环开始时执行，在循环开始时，执行一次条件判断，若条件成立则执行循环体，在循环体执行完成之后执行更新循环变量语句，之后再执行条件判断到循环变量更新的循环。**<br>
foreach循环和for循环有所不同。它用来遍历数据项集合，声明一个循环变量用来依次接收数据项集合中的每一个数据项。数据项集合中的每一项只会被遍历一次，不会出现计数器超过集合边界的问题和出现计数出错问题。foreach循环期间禁止修改循环变量。

```C#
//for循环
for(initial;condition;loop){
    statement;
}
//当循环体statement只有一条语句时可以省略for循环语句之后的‘{}’

//foreach循环
foreach(type[var] variable in collection){//in为遍历关键词，variable用来接收数据项集合中的每一项
    statements;
}
```

### while和do while循环

*在不知道循环次数，且不会用到计数器时，推荐while循环。*
while循环是最简单的条件循环。它只需要在while之后加上一个条件判断就能实现流程的循环与控制。while循环语句在循环开始时先进行一次条件判断，如为True则执行循环体并进入下一个循环，为False则跳出循环。do while循环是while循环的异体，它是先进行循环体的执行，再进行条件的判断。保证了循环的主体部分一定会执行一次。<br>

```C#
//while循环
while(condition){
    statement;
}
//do while循环
do{
    statement;
}while(condition)

//使用while循环实现for循环的转换
initial;
while(condition){
    statement;
    loop;
}
```

## 条件选择

switch条件选择可以在一个值需要与多个值进行比较选择时，提供比if判断更加方便，容易理解的语句。其使用方法为在switch后附加expression，用于和之后的case中的constant子句比较，若相等，则执行该case中的statement，若不匹配则匹配下一个case。需要注意的是case与case之间不能贯穿，可以通过break、goto等语句来断开。如不断开，则在上一个case匹配到并执行完之后，还会和下面的每一个case进行匹配。default是switch中的默认选择，当程序运行到default子项时，就会执行default中的statements。目前，C#中支持的expression返回的类型为所有值类型和string这一引用类型。switch实例：<br>

```C#
switch(expression){
    case constant:
        statements;
        break;//用来隔断case，不一定为break
    case constant:
        statements;
        break;
    default://当前面的case都不匹配时，执行默认case(default)
        statements;
}
```

## 跳转

跳转语句用来改变程序的运行顺序(如：循环的执行逻辑)。跳转语句可以退出循环，跳出本次循环的剩余部分进入下一次循环或者结束这个函数(方法)。

### break

C#中使用break语句来退出循环或者switch语句。任何时候遇到break语句，控制都会立刻离开循环或者switch。<br>

```C#
for(;;){
    statements;
    break;//跳出这个for循环
    statements;
}
```

### continue

C#中continue语句用来跳出本次循环的剩余部分进入下一次循环。<br>

```C#
for(;;){
    statements;
    continue;//跳入下一次的循环
    statements;//不会被执行
}
```

### goto

C#中goto语句用来在switch语句中实现贯穿<br>

```C#
switch(expression){
    case constant1:
        statements;
        goto default;//当expression返回的结果等于constant1时，进入这个子项，运行到goto之后会跳到default子项，继续运行。
    case constant2:
        statements;
        break;
    default:
        statements;
        break;
}
```

### return

C#中用来在一个函数(方法)中返回一个数据，当执行到return时，这个函数就意味着运行完毕。<br>

```C#
public int getAge(){
    return 18;
}
```