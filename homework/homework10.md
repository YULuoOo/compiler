# 编译原理作业十
## S->aSbS|bSaS|ε 

#### a) 该文法是否有二义性，证明之。

```
重复题

对abab进行两种最左推导

S => aSbS => abS => abaSbS => ababS => abab

S => aSbS => abSaSbS => abaSbS => ababS => abab
```

#### b) 构造abab的最右推导
```
S => aSbS => aSbaSbS => aSbaSb => aSbab => abab
```

#### c) 构造abab语法树


