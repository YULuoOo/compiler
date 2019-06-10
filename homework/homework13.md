# 编译原理作业十三
##一、写出下面文法的属性文法（5分）：     
```
Number → Number1  Digit      

Number → Digit     

Digit → 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9|
```
```
Number.val = Number1.val * 10 + Digit.val

Number.val = Digit.val

Digit.val = 0
Digit.val = 1
Digit.val = 2
Digit.val = 3
Digit.val = 4
Digit.val = 5
Digit.val = 6
Digit.val = 7
Digit.val = 8
Digit.val = 9
```

##二、写出下面文法的属性文法（5分）：    
```

Number →  Digit  Number1  

Number → Digit     

Digit → 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9|
```

```
Number.mul = Number 1.mul * 10
Number.val = Digit.val * Number.mul + Number 1.val

Number.mul = 1
Number.val = Digit.val

Digit.val = 0
Digit.val = 1
Digit.val = 2
Digit.val = 3
Digit.val = 4
Digit.val = 5
Digit.val = 6
Digit.val = 7
Digit.val = 8
Digit.val = 9
```


##三、十进制浮点数的文法修改如下（5分）： 
```

dnum → num.snum 

num → num1 digit | digit 

snum → digit snum1 | digit 

digit → 0|1|2|3|4|5|6|7|8|9
```


```
dnum.val = num.val + snum.val

num.val = num1.val * 10 + digit.val

num.val = digit.val

snum.val = (snum1.val + digit.val ) / 10

snum.val = digit.val / 10

Digit.val = 0
Digit.val = 1
Digit.val = 2
Digit.val = 3
Digit.val = 4
Digit.val = 5
Digit.val = 6
Digit.val = 7
Digit.val = 8
Digit.val = 9
```
