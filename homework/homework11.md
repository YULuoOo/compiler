# 编译原理作业十一
## 1.考虑下面文法，构造 SLR 分析表（5）
```
E→E+T|T

T→TF|F

F → F *| a | b
```
拓展文法G'
```
E'->E      (1)
E->E+T     (2)
E->T       (3)
T->TF      (4)
T->F       (5)
F->F*      (6)
F->a       (7)
F->b       (8)
```
计算first集和follow集
```
first(E)={a,b}
first(T)={a,b}
first(F)={a,b}
follow(E)={+,$}
follow(T)={a,b,$}
follow(F)={a,b,*,$}

follow算错了 所以后面表也错了
follow(T)={+,a,b,$}
follow(F)={+,a,b,*,$}

```
开始罗列GOTO得到的状态
```
I0:
    E'->.E      
    E->.E+T     
    E->.T       
    T->.TF      
    T->.F       
    F->.F*      
    F->.a       
    F->.b 
    
GOTO(I0,E)->I1:
I1:
    E'->E.
    E->E.+T

GOTO(I0,T)->I2
I2:
    T->T.F  add closure(F)
    E->T.
    F->.F*
    F->.a
    F->.b
    
GOTO(I0,F)->I3
I3:
    T->F.
    F->F.*
    
GOTO(I0,a)->I4
I4:
    F->a.

GOTO(I0,b)->I5
I5:
    F->b.
    
GOTO(I1,+)->I6
I6:
    E->E+.T  add closure(T)
    T->.TF
    T->.F    add closure(F)
    F->.F*
    F->.a
    F->.b
    
GOTO(I2,F)->I7
I7:
    T->TF.
    F->F.*

GOTO(I2,a)->I4
GOTO(I2,b)->I5

GOTO(I3,*)->I8
I8:
    F-F*.

GOTO(I6,T)->I9
I9:
    T->T.F  add closure(F)
    F->.F*
    F->.a
    F->.b
    
GOTO(I6,F)->I3
GOTO(I6,a)->I4
GOTO(I6,b)->I5

GOTO(I7,*)->I8

GOTO(I9,F)->I3
GOTO(I9,a)->I4
GOTO(I9,b)->I5
```
构造SLR分析表  

<table>
    <tr>
        <th rowspan="2">状态</th>
        <th colspan="5">ACTION</th>
        <th colspan="5">GOTO</th>
    </tr>
    <tr>
        <td>a</td>
        <td>b</td>
        <td>+</td>
        <td>*</td>
        <td>$</td>
        <td>E</td>
        <td>T</td>
        <td>F</td>
    </tr>
    <tr>
        <td>0</td>
        <td>S4</td>
        <td>S5</td>
        <td></td>
        <td></td>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1</td>
        <td></td>
        <td></td>
        <td>S6</td>
        <td></td>
        <td>acc</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>2</td>
        <td>S4</td>
        <td>S5</td>
        <td>R3</td>
        <td></td>
        <td>R3</td>
        <td></td>
        <td></td>
        <td>7</td>
    </tr>
    <tr>
        <td>3</td>
        <td>R5</td>
        <td>R5</td>
        <td></td>
        <td>S8</td>
        <td>R5</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>4</td>
        <td>R7</td>
        <td>R7</td>
        <td></td>
        <td>R7</td>
        <td>R7</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>5</td>
        <td>R8</td>
        <td>R8</td>
        <td></td>
        <td>R8</td>
        <td>R8</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>6</td>
        <td>S4</td>
        <td>S5</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>9</td>
        <td>3</td>
    </tr>
    <tr>
        <td>7</td>
        <td>R4</td>
        <td>R4</td>
        <td></td>
        <td>S8</td>
        <td>R4</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>8</td>
        <td>R6</td>
        <td>R6</td>
        <td></td>
        <td>R6</td>
        <td>R6</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>9</td>
        <td>S4</td>
        <td>S5</td>
        <td>R2</td>
        <td></td>
        <td>R2</td>
        <td></td>
        <td></td>
        <td>7</td>
    </tr>
</table>



## 2. 对文法，证明它是 LL(1)文法但不是 SLR(1)文法（5）
```
S→AaAb | BbBa

A→ε

B→ε
```
1. 证明是LL(1)
```
LL(1)的充要条件
S->AaAb | BbBa
First(AaAb)={a}
First(BbBa)={b}
交集为空
```
2. 证明不是SLR(1)文法
```
follow(A)={a,b}=follow(B)
```
```
    I0:
        S'->.S
        S->.AaAb
        S->.BbBa
        A->.    （4）
        B->.    （5）
```
所以填表时0->4 0->5 中都会有两个reduce
Qed.

