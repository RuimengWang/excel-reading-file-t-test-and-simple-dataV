# excel-reading-file-t-test-and-simple-dataV
# coding: utf-8

# In[ ]:

# Python mini-project
# 这是我最近在写的一个非常大的project里面的一个小部分。相比于那个不太容易的project，这个项目很简单，也很有趣，同时也非常有用！
# 这个项目一共有三部分。从excel（保存为csv格式）里读数据并存在列表（list）里面；对两个list进行t-test;对两个list绘图。
# 这个代码如果真正熟悉的话，写下来应该在10-15分钟。
# 如果在产业界直接应用的话，删掉一些cell，把code直接拼起来就可以运行了。


# In[ ]:

# 第一部分：从excel里面读文件
# 用python可以读取许多种类的文件，从寻常的excel，txt再到各种非常高大上的文件，比如.xyz格式的文件（存储量子化学数据的，本人曾经开发过
# 一个读量子化学数据的软件）等等。而python自带有不少的可以用于读各种格式的文件的package。比如xlrd(Python module to extract data from excel)
# 这一部分的方法相对来说比较灵活。需要结合具体的文件格式。我们在这里读的是一个.csv格式的文件。这种我们采用的是python的csv module


# In[ ]:

#这一部分我们直接import这个项目里所需要的四个module
import csv
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats


# In[ ]:

#第一部分：从excel里面读文件
#首先定义两个list用于接收数据
a1=[]
a2=[]
#请注意，相比于有些博客上的open-close方法，尽量要用python设计的with方法。with可以帮助我们自动调用close
#用open-close的缺点在于，这个方法运行起来非常繁琐。而且，根据编程规范，文件一旦结束使用，必须关闭。因为打开的文件会占用系统的资源。而且一个
#操作系统能够在一段时间内处理的文件的数目也是有限的。
#使用read还有一个很大的风险，就是假如要读的文件size很大。比如，有15个G。强行用read的话，肯定内存就会爆掉。在这个地方解决方案就是用readline（）
#函数或者readsize（）函数
with open('C:/Users/wrm/Desktop/searching233engine233result.csv') as f:
    f_csv = csv.reader(f)
    headers = next(f_csv)
    #print (f_csv)
    for row in f_csv:
      a1.append(float(row[0]))
      a2.append(float(row[1]))
#print (a1)
#print (a2)


# In[ ]:

#第二部分：对两个list的数据进行t-test
#这个也可以用R语言去处理：
#R语言的代码是：
t1 = read.table('file1.txt')$V1
t2 = read.table('file2.txt')$V1
t.test(t1, t2, paired=T)

#在这里我们采用scipy里自带的检测t-test的module
print (stats.ttest_ind(a1,a2))


# In[1]:

#第三个部分：对获得的两个list进行绘图，这个地方我们直接用最流行的matplotlib.pyplot解决。两句代码，搞定！
plt.plot(a1,a2)
plt.show()


# In[ ]:



