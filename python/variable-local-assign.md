# Python变量在局部重新赋值时的问题

刚碰到一个错误：

```
defined in enclosing scope on line 57) referenced before assignment
```

代码很简单，形如：

```python
def func(test):
    def func2():
       if test:
          test = test.split(',')
    return func2
```

然后就报错了。。。

## 原因

本地变量没有定义就使用了！为什么`test`变量被当成了本地变量？

因为`test在本地被赋值了`！

## 解决

```python
def func(test):
   if test:
      test = test.split(',')
    def func2():
        # do somethins
    return func2
```


## 附：网上看到的一个例子


```python
lst = [1, 2, 3]
def foo1():
    lst.append(5)   # This works ok...

foo1()
print lst
# output: [1, 2, 3, 5]

lst = [1, 2, 3]
def foo2():
    lst += [5]      # ... but this bombs!

foo2()

# 发生错误：
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 2, in foo
UnboundLocalError: local variable 'lst' referenced before assignment
```

## 附：另外还看见了一个大坑：函数的默认值只在函数定义的时候执行一次

英文表述是：
`the default value for a function argument is only evaluated once, at the time that the function is defined.`

看代码：

```python
def func(bar=[]):
    bar.append(1)
    return bar

func()   # [1]
func()   # [1, 1]
```

这是一个大坑不是，哈哈

## 扩展阅读

- [Python命名空间和作用域窥探](http://blog.cipherc.com/2015/04/25/python_namespace_and_scope/)
- [python学习笔记 - local, global and free variable](http://www.jianshu.com/p/e1fd4f14136a)
