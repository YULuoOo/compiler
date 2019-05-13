# 编译原理作业十二
## 一.用LR(1)与LALR分析下面文法（20）

### 1.（10）
```
E→E+T|T

T→TF|F

F → F *| a | b
```
拓展文法G'
```
E'->E      (0)
E->E+T     (1)
E->T       (2)
T->TF      (3)
T->F       (4)
F->F*      (5)
F->a       (6)
F->b       (7)
```
计算first集和follow集
```
first(E)={a,b}
first(T)={a,b}
first(F)={a,b}
follow(E)={+,$}
follow(T)={+,a,b,$}
follow(F)={+,a,b,*,$}
```
#### LR(1)
开始罗列GOTO得到的状态
```
I0:
    E'->.E,$      
    E->.E+T,$     
    E->.T,$   
    T->.TF,$     
    T->.F,$       
    F->.F*,$      
    F->.a,$       
    F->.b,$ 
    
GOTO(I0,E)->I1:
I1:
    E'->E.,$
    E->E.+T,$

GOTO(I0,T)->I2
I2:
    T->T.F,$  add closure(F)
    E->T.,$
    F->.F*,$
    F->.a,$
    F->.b,$
    
GOTO(I0,F)->I3
I3:
    T->F.,$
    F->F.*,$
    
GOTO(I0,a)->I4
I4:
    F->a.,$

GOTO(I0,b)->I5
I5:
    F->b.,$
    
GOTO(I1,+)->I6
I6:
    E->E+.T,$  add closure(T)
    T->.TF,$
    T->.F,$    add closure(F)
    F->.F*,$
    F->.a,$
    F->.b,$
    
GOTO(I2,F)->I7
I7:
    T->TF.,$
    F->F.*,$

GOTO(I2,a)->I4
GOTO(I2,b)->I5

GOTO(I3,*)->I8
I8:
    F-F*.,$

GOTO(I6,T)->I9
I9:
    T->T.F  add closure(F)
    F->.F*,$
    F->.a,$
    F->.b,$
    
GOTO(I6,F)->I3
GOTO(I6,a)->I4
GOTO(I6,b)->I5

GOTO(I7,*)->I8

GOTO(I9,F)->I3
GOTO(I9,a)->I4
GOTO(I9,b)->I5
```
构造LR(1)分析表  

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
        <td>R2</td>
        <td></td>
        <td>R2</td>
        <td></td>
        <td></td>
        <td>7</td>
    </tr>
    <tr>
        <td>3</td>
        <td>R4</td>
        <td>R4</td>
        <td>R4</td>
        <td>S8</td>
        <td>R4</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>4</td>
        <td>R6</td>
        <td>R6</td>
        <td>R6</td>
        <td>R6</td>
        <td>R6</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>5</td>
        <td>R7</td>
        <td>R7</td>
        <td>R7</td>
        <td>R7</td>
        <td>R7</td>
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
        <td>R3</td>
        <td>R3</td>
        <td>R3</td>
        <td>S8</td>
        <td>R3</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>8</td>
        <td>R5</td>
        <td>R5</td>
        <td>R5</td>
        <td>R5</td>
        <td>R5</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>9</td>
        <td>S4</td>
        <td>S5</td>
        <td>R1</td>
        <td></td>
        <td>R1</td>
        <td></td>
        <td></td>
        <td>7</td>
    </tr>
</table>

#### LALR
## `很显然，没有可以进行核心合并的地方 LALR的构造表是与上面相同的`



#### 2. （10）
```
S→AaAb | BbBa

A→e

B→e
```
拓展文法G'
```
S'->S      (0)
S->AaAb    (1)
S->BbBa    (2)
A->e       (3)
B->e       (4)
```
计算first集和follow集
```
follow(S)={a,b,$}
follow(A)={a,b}
follow(B)={a,b}
```
#### LR(1)
开始罗列GOTO得到的状态
```
I0:
  S'->.S,$      
  S->.AaAb,$  
  S->.BbBa,$    
  A->.,a      
  B->.,b
  
GOTO(I0,S)=I1
I1:
  S'->S.,$
  
GOTO(I0,A)=I2
I2:
  S'->A.aAb,$
  
GOTO(I0,B)=I3
I3:
  S'->B.bBa,$
  
GOTO(I2,a)=I4
I2:
  S'->Aa.Ab,$
  A->.,b
  
GOTO(I3,b)=I5
I4:
  S'->Bb.Ba,$
  B->.,a
  
GOTO(I4,A)=I6
I6:
  S'->AaA.b,$
  
GOTO(I5,B)=I7
I3:
  S'->BbB.a,$
  
GOTO(I6,b)=I8
I2:
  S'->AaAb.,$

GOTO(I7,a)=I9
I2:
  S'->BbBa.,$
```
构造LR(1)表
<table>
    <tr>
        <th rowspan="2">状态</th>
        <th colspan="3">ACTION</th>
        <th colspan="3">GOTO</th>
    </tr>
    <tr>
        <td>a</td>
        <td>b</td>
        <td>$</td>
        <td>S</td>
        <td>L</td>
        <td>R</td>
    </tr>
    <tr>
        <td>0</td>
        <td>R3</td>
        <td>R4</td>
        <td></td>
        <td>1</td>
        <td>2</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1</td>
        <td></td>
        <td></td>
        <td>acc</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>2</td>
        <td>S4</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>3</td>
        <td></td>
        <td>S5</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>4</td>
        <td></td>
        <td>R3</td>
        <td></td>
        <td></td>
        <td>6</td>
        <td></td>
    </tr>
    <tr>
        <td>5</td>
        <td>R4</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>7</td>
    </tr>
    <tr>
        <td>6</td>
        <td></td>
        <td>S8</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>7</td>
        <td>S9</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>8</td>
        <td></td>
        <td></td>
        <td>R1</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>9</td>
        <td></td>
        <td></td>
        <td>R2</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
</table>


#### LALR
## `很显然，没有可以进行核心合并的地方 LALR的构造表是与上面相同的`
