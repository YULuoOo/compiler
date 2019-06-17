## 编译原理第十四次作业
### 1、 翻译算术表达式a ∗ −(b + c)为 （12分）

#### (1)一个语法树。
```
               a*-(b+c)
               /   |   \
             a     *     -(b+c)
                       /    |     
                      -    (b+c)
                        /    |    \
                       (    b+c    )
                           / | \
                           b + c
```

#### (2)后缀式。
```
a0bc+-*
```

#### (3)三地址代码。
```
mov t1,,b
mov t2,,c
add t3,t1,t2
uminus t4,,t3
mov t5,,a
mult t6,t4,t5
```


### 2、有一个语法制导翻译的语义动作如下:（10分）

T → aDa    {print”1”}

D → (A      {print”2”}

D → d        {print”3”}

A → Dd)    {print”4”}

若输入字符序列为a(((dd)d)d)a，且采用自上而下的分析方法，请写出语义执行的输出序列”34242421”。
```
T→aDa{print “1”}
→a(A{print “2”}a{print “1”}
→a(Dd){print “4”}{print “2”}a{print “1”} 
→a((A{print “2”}d){print “4”}{print “2”}a{print “1”}
→a((Dd){print “4”}{print “2”}d){print “4”}{print “2”}a{print “1”}
→a(((A{print “2”}d){print “4”}{print “2”}d){print “4”}{print “2”}a{print “1”} 
→a(((Dd){print “4”}{print “2”}d){print “4”}{print “2”}d){print “4”}{print “2”}a{print “1”} 
→a(((d{print “3”}d){print “4”}{print “2”}d){print “4”}{print “2”}d){print “4”}{print “2”}a{print “1”}
```



