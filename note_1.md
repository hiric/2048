*关于zip()的使用

 Help on built-in function zip in module __builtin__:

 zip(...)
    zip(seq1 [, seq2 [...]]) -> [(seq1[0], seq2[0] ...), (...)]

    Return a list of tuples, where each tuple contains the i-th element
    from each of the argument sequences.  The returned list is truncated
    in length to the length of the shortest argument sequence.
 None
 
 大意：
 
 定义：zip([seql, …])接受一系列可迭代对象作为参数，将对象中对应的元素打包成一个个tuple（元组），
 然后返回由这些tuples组成的list（列表）。若传入参数的长度不等，则返回list的长度和参数中长度最短的对象相同。
 
 实例：
 
 x = [1, 2, 3]
 y = [4, 5, 6]
 z = [7, 8, 9]

 xyz = zip(x, y, z)

 print xyz

 '''结果是:'''
 [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
 #对应元素组成一个新的元组，元组构成列表
 #---------------------------------------#

 #无参数时，
 x = zip()
 print x

 #结果是：
 []

 #---------------------------------------#

 #长度不等时，取长度的最小的

 x = [1, 2, 3]
 y = ['a', 'b', 'c', 'd']
 xy = zip(x, y)
 print xy

 #结果是：
 [(1, 'a'), (2, 'b'), (3, 'c')]
 
* 矩阵转置

 x = [[1,2,3],
     [4,5,6],
     [7,8,9]]
 y = zip(*x)
 print y

 #结果是：
 [(1, 4, 7), (2, 5, 8), (3, 6, 9)]


 

 
