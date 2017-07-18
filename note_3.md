cast(''.join('|{: ^5} '.format(num) if num > 0 else '| ' for num in row) + '|')

join 是split 的逆方法

^ 是居中显式，<是左对齐，>是右对齐，冒号后面有一个空格，意思是空格填充，例如使用a = '{:0<5}'.format(123)那么结果就是'12300',
左对齐，长度为5，使用 0 填充，对于题目中|{: ^5} '.format(num)，同理，不同的是使用空格填充，并且是居中
('|{: ^5} '.format(num) if num > 0 else '| ' for num in row),仔细分析，类似于 ([x if x > 3 else x**2 for x in range(10)])，
这个跟上面的结构基本类似，加上方括号更好理解一点，range(10) = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],for x in range(10),即在0-9 之间，
if x > 3 ，如果x > 3，得到 x ，else x**2 ，否则得到 x**2
