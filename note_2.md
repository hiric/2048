* choice()

  描述：choice() 方法返回一个列表，元组或字符串的随机项。
  
  语法：
  以下是 choice() 方法的语法:
  import random
  random.choice( seq  )
  
  实例：
  下展示了使用 choice() 方法的实例：
  !/usr/bin/python
  import random

  print "choice([1, 2, 3, 5, 9]) : ", random.choice([1, 2, 3, 5, 9])
  rint "choice('A String') : ", random.choice('A String')
  以上实例运行后输出结果为：
  hoice([1, 2, 3, 5, 9]) :  2
  hoice('A String') :  n
  
  
* any()

  any(...)
    any(iterable) -> bool
    
    Return True if bool(x) is True for any x in the iterable.
    If the iterable is empty, return False.
  以上是python doc中得说明，意思就是当传入空可迭代对象时返回False，当可迭代对象中有任意一个不为False，则返回
  
  实例：
  >> any('123')
  rue
  >>> any([0, 1])
  True
  >>> any([0, ''])
  alse
