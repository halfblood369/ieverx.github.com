---
layout: post
title: "Python的逻辑运算"
tagline: "Logic Operation In Python"
description: "Python中的逻辑运算的规定以及实质"
category: "Python"
tags: ["Python", "语义"]
---
{% include JB/setup %}

Python的逻辑运算(and，or，not)与C/C++、Java等语言不太一样。这些语言的逻辑运算返回的值都是bool值，而Python返回的则不同。

先说非运算，Python的非运算与这些语言相比，并没有特别的地方。not只有两个返回值，True和False。在Python中，真值为假的对象，包括False，None，数字0，空字符串以及空的容器类型。除此以外的任何对象均为真。

接下来是与运算，Python的与运算的规则是

* 若左边的表达式为真，则返回右边表达式的值
* 否则，返回左边表达式的值

初看起来比较奇怪，一个逻辑运算搞得这么复杂干嘛？这么做当然是有目的的。当我们需要的不是一个表达式的bool值而事实其表达式的值，但是只是需要根据这个表达式的bool值确定下一步的动作，就会发现这种规定的好处了。

比如需要统计一下重量在500克以上的桃子的重量，用C写，可能会写成这样

    for (i = 0; i < n; ++i) {
        if (weights[i] > 500)
            sumofweight += weights[i];
    }

用Python，就可以这样写

    for x in weights:
        sumofweights += x > 500 and x

显然是简单了许多。

最后再来说或运算，Python的或运算的规则是

* 若左边的表达式为真，则返回左边的表达式的值
* 否则，返回右边的表达式的值

这个规定和或运算的目同出一辙，都是为了简化代码，增加效率。

可能有些同学觉得and和or的规则比较复杂，不容易记忆。其实，这是不需要记忆的，因为，**无论是and还是or，其结果的值就是最终决定整个表达式真值的表达式的值**。

对于与运算

    a and b

* 如果a为真，继续计算b，b将决定最终整个表达式的真值，所以，结果为b的值
* 如果a为假，无需计算b，就可以得知整个表达式的真值为假，所以，结果为a的值
 
对于或运算

    a or b

* 如果a为真，无需计算b，就可得知整个表达式的真值为真，所以结果为a的值
* 如果a为假，继续计算b，b将决定整个表达式最终的值，所以结果为b的值

最后再说一下and or表达式，通常所说的and or表达式是指如下的表达式

    condition and a or b

这个表达式和C中的唯一一个三目运算符

    condition ? a : b

比较相似，但稍有不同。C中三目表达式的语义如下

    if condition:
    	a
    else:
    	b

但是Python的and or则不同，由于Python的逻辑表达式的运算规则，必须保证a的真值为真，才和C的三目运算符相同，而若a为假，不论condition的真值为何，总会选择b而非a。

可以说，Python的逻辑运算给程序员带来了极大的编程快捷，但是若不能理解其如此设计的原因，就不能自如的运用其便捷性，甚至造成错误而不知。
