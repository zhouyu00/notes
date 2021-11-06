# 4 复合数据类型
## 4.1 数组
1.在数组字面量中，如果省略号出现在数组长度的位置，则数组长度由初始化的数组长度数目决定
2.数组长度是数组类型的一部分，这个值在编译期就可以确定
3.在go语言中数组是使用值传递的（和java不同哦）

## 4.2 slice
1. slice 有三个属性，指针，长度和容量（底层数组能容纳的元素个数）len返回长度，cap返回容量
2. slice 传递指针，可以修改数组
3. slice 无法做比较，slice 唯一可比较的是nil
4. 对于任何类型，如果它们的值可以是nil,那么这个类型的nil值可以使用一种转换表达式
5. 使用len(s)==0检查slice是否为空

```
//创建指定元素类型，长度和容量的slice
make(T[],len)
make(T[],len,cap)
```

### 4.2.1 append函数
1. append 可能导致一次新的内存分配，不能假设append后原来的slice仍然指向同一个底层数组，因此需要将append后返回的slice赋值给传入的slice
```
runes = append(runes,r)
```
### 4.2.2 就地修改


## 4.3 map


## 4.6 文本和HTML模板

# 5 函数
## 5.1 函数声明
1. 每个函数声明都包含一个名字，一个函数列表，一个可选的返回列表以及函数体
```
func name(parameter-list) (result-list){
    body
}
```

2. 返回值可以像形参一样命。这个时候每个命名的返回值会声明为一个变量，并根据变量类型初始化为0值
3. 当存在返回列表时，必须显式地以return语句结束，除非函数明确不会以
4. 函数的类型叫做函数签名。当两个函数拥有相同的形参和返回列表时，认为这两个函数的类型或者签名是相同的

## 5.2 递归

## 5.3 多返回值
1. 一个函数如果有命名的返回值，可以省略return 语句的操作数，这成为裸返回；裸返回是将每个命名返回结果按照顺序返回的快捷方法

## 5.4 错误
### 5.4.1 错误处理策略
1. 按照流程控制返回错误
2. 重试然后报错
3. log输出错误，并优雅退出

### 5.4.2 文件结束标识

## 5.5 函数变量
1. 函数变量的零值是nil
2. 

## 5.6 匿名函数
1. go也有闭包，因此需要注意循环中变量的作用域
2. 对匿名函数的递归调用需要闭包，将函数声明和调用分开
**捕获迭代变量**


## 5.7 变长函数

## 5.8 延迟函数调用
1. defer 语句的实际调用推迟到包含defer的函数结束后才执行
2. defer语句不限制使用次数，执行的时候以调用defer语句的顺序倒序进行
3. defer语句常用语成对的操作，保证资源的正确释放
4. 延迟执行的匿名函数可以改变外层函数返回给调用者的结果


## 5.9 宕机
1. 宕机发生时，正常的程序执行会终止。

