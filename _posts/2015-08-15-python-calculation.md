---
layout: post
tags: algorithm
date: 2015-08-15 19:00
title: Python Reverse Polish Notation
published: true
---

yesterday one of my colleagues raise this with performance issue.<br/>
***the target*** is: input a string with numbers and brackets, calculate the result.
let's use 
**python**

{% highlight python %}

from compiler.misc import Stack
stackBracket = Stack()
def calculateOne(lastLeft, firstRight, purestr):
    result = 0
    operation = "plus"
    list = purestr[lastLeft + 1:firstRight]
    for i in list:
        if i == "+":
            operation = "plus"
        elif i == "-":
            operation = "minus"
        else:
            if operation == "plus":
                result = result + int(i)
            else:
                result = result - int(i)
    return result
def convertStringToList(purestr):
    list = []
    part = ""
    for i in range(len(purestr)):
        s = purestr[i]
        if s in ["+", "-", "(", ")"]:
            if part != "":
                list.append(part)
                part = ""
            list.append(s)
        else:
            part = part + s
    return list
def replaceOne(lastLeft, firstRight, result, purestr):
    before = purestr[0:lastLeft]
    after = purestr[firstRight + 1:]
    before.append(str(result))
    before.extend(after)
    return before

def updateIndex(lastLeft, firstRight, i):
    return i - (firstRight - lastLeft + 1)

def matchBracket(purelist):
    totalLen = len(purelist)
    i = 0
    while i < totalLen:
        s = purelist[i]
        if s == '(':
            stackBracket.push(i)
        elif s == ')':
            lastLeft = stackBracket.pop()
            firstRight = i
            result = calculateOne(lastLeft, firstRight, purelist)
            purelist = replaceOne(lastLeft, firstRight, result, purelist)
            totalLen = len(purelist)
            i = updateIndex(lastLeft, firstRight, i)
        i = i + 1
    result=purelist;
    if len(purelist)>2:
        result=calculateOne(-1,len(purelist),purelist)
    print result

def cal(purestr):
    purelist = convertStringToList(purestr)
    matchBracket(purelist)

if __name__ == '__main__':
    inputStr='''(1+(2+(1+2-1+5)+2))+(((2+3)-1+5)-2+11)+\
	(12-2-1+1)+((22+11-3)+(26-2-1-20+3))+4+(28+2)-10+\
	(1+(2+(1+2-1+5)+2))+(((2+3)-1+5)-2+11)+(12-2-1+1)+\
	((22+11-3)+(26-2-1-20+3))+4+(28+2)-10+\
	(1+(2+(1+2-1+5)+2))+(((2+3)-1+5)-2+11)+(12-2-1+1)+\
	((22+11-3)+(26-2-1-20+3))+4+(28+2)-10+\
	(1+(2+(1+2-1+5)+2))+(((2+3)-1+5)-2+11)+(12-2-1+1)+\
	((22+11-3)+(26-2-1-20+3))+4+(28+2)-10+\
	(1+(2+(1+2-1+5)+2))+(((2+3)-1+5)-2+11)+(12-2-1+1)+\
	((22+11-3)+(26-2-1-20+3))+4+(28+2)-10+\
'''
    cal(inputStr)

{% endhighlight %}