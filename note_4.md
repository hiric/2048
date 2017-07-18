众所周知，在Python中如果访问字典中不存在的键，会引发KeyError异常（JavaScript中如果对象中不存在某个属性，则返回undefined）。但是有时候，字典中的每个键都存在默认值是非常方便的。例如下面的例子：

strings = ('puppy', 'kitten', 'puppy', 'puppy',
           'weasel', 'puppy', 'kitten', 'puppy')
counts = {}

for kw in strings:
    counts[kw] += 1
该例子统计strings中某个单词出现的次数，并在counts字典中作记录。单词每出现一次，在counts相对应的键所存的值数字加1。但是事实上，运行这段代码会抛出KeyError异常，出现的时机是每个单词第一次统计的时候，因为Python的dict中不存在默认值的说法，可以在Python命令行中验证：

>>> counts = dict()
>>> counts
{}
>>> counts['puppy'] += 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'puppy'

使用判断语句检查

既然如此，首先可能想到的方法是在单词第一次统计的时候，在counts中相应的键存下默认值1。这需要在处理的时候添加一个判断语句：

strings = ('puppy', 'kitten', 'puppy', 'puppy',
           'weasel', 'puppy', 'kitten', 'puppy')
counts = {}

for kw in strings:
    if kw not in counts:
        counts[kw] = 1
    else:
        counts[kw] += 1

# counts:
# {'puppy': 5, 'weasel': 1, 'kitten': 2}
使用dict.setdefault()方法

也可以通过dict.setdefault()方法来设置默认值：

strings = ('puppy', 'kitten', 'puppy', 'puppy',
           'weasel', 'puppy', 'kitten', 'puppy')
counts = {}

for kw in strings:
    counts.setdefault(kw, 0)
    counts[kw] += 1 # 原PPT中这里有一个笔误
dict.setdefault()方法接收两个参数，第一个参数是健的名称，第二个参数是默认值。假如字典中不存在给定的键，则返回参数中提供的默认值；反之，则返回字典中保存的值。利用dict.setdefault()方法的返回值可以重写for循环中的代码，使其更加简洁：

strings = ('puppy', 'kitten', 'puppy', 'puppy',
           'weasel', 'puppy', 'kitten', 'puppy')
counts = {}

for kw in strings:
    counts[kw] = counts.setdefault(kw, 0) + 1
使用collections.defaultdict类

以上的方法虽然在一定程度上解决了dict中不存在默认值的问题，但是这时候我们会想，有没有一种字典它本身提供了默认值的功能呢？答案是肯定的，那就是collections.defaultdict。

defaultdict类就好像是一个dict，但是它是使用一个类型来初始化的：

>>> from collections import defaultdict
>>> dd = defaultdict(list)
>>> dd
defaultdict(<type 'list'>, {})
defaultdict类的初始化函数接受一个类型作为参数，当所访问的键不存在的时候，可以实例化一个值作为默认值：

>>> dd['foo']
[]
>>> dd
defaultdict(<type 'list'>, {'foo': []})
>>> dd['bar'].append('quux')
>>> dd
defaultdict(<type 'list'>, {'foo': [], 'bar': ['quux']})
需要注意的是，这种形式的默认值只有在通过dict[key]或者dict.__getitem__(key)访问的时候才有效，这其中的原因在下文会介绍。

>>> from collections import defaultdict
>>> dd = defaultdict(list)
>>> 'something' in dd
False
>>> dd.pop('something')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'pop(): dictionary is empty'
>>> dd.get('something')
>>> dd['something']
[]
该类除了接受类型名称作为初始化函数的参数之外，还可以使用任何不带参数的可调用函数，到时该函数的返回结果作为默认值，这样使得默认值的取值更加灵活。下面用一个例子来说明，如何用自定义的不带参数的函数zero()作为初始化函数的参数：

>>> from collections import defaultdict
>>> def zero():
...     return 0
...
>>> dd = defaultdict(zero)
>>> dd
defaultdict(<function zero at 0xb7ed2684>, {})
>>> dd['foo']
0
>>> dd
defaultdict(<function zero at 0xb7ed2684>, {'foo': 0})
利用collections.defaultdict来解决最初的单词统计问题，代码如下：

from collections import defaultdict

strings = ('puppy', 'kitten', 'puppy', 'puppy',
           'weasel', 'puppy', 'kitten', 'puppy')
counts = defaultdict(lambda: 0)  # 使用lambda来定义简单的函数

for s in strings:
    counts[s] += 1
