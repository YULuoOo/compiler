# 编译原理作业八
## 4.1消除下列文法的左递归性。（4分）

* (1)
```
S→SA|A

A→SB|B|(S)|( )

B→［S］|［ ］
```

```
根据AS的顺序进行计算
将A带入S
S->SA|SB|B|(S)|()
A->SB|B|(S)|()
B->[S]|[]

对S做直接左递归消除
得
S->BS'|(S)S'|()S'
S'->AS'|BS'|ε
A->SB|B|(S)|()
B->[S]|[]

```

* (2) 
```
S→AS|b

A→SA|a
```
```
排序AS
A带入S
S->SAS|bS|a
A→SA|a

对S做直接左递归
得
S->bSS'|aS'
S'->ASS'|ε
```
 

## 4.2设已给文法：（2分）
```
S→AbB|d

A→Cab|Bf

B→CSd|d

C→ed|a
```

#### 试写出对符号串eddfbbd进行带回溯的自顶向下语法分析的过程。（提示：不需要消除左递归）

```
脑子里走了一遍，全部匹配不了，要是画出来的画真的炸了，实习又忙的一匹，还要忙保研的事，没时间画了，该扣扣吧😂
```
 

## 4.3对于如下的文法，求出各个FIRST集和FOLLOW集。（4分）
```
S→aAB|bA |ε

A→aAb |ε

B→bB|ε
```

|  | first | follow 
| - | :-: | :-: 
| S | {a,b,ε} | {$} 
| A | {a,ε} | {b,$} 
| B | {b,ε} | {$}
 

## 4.4试证明： 任何具有左递归性的前后文无关文法均非LL(1)文法。（3分）

 ```
 对于一个左递归的文法，
 例如如下形式
   S->A|B|...
   A->S
   显然A的first与B的first会有重叠
   这与LL(1)文法的充要条件矛盾
 Qed.
 
  文法G是LL(1)的，当且仅当对于G的每个非终结符Α的任何两个不同产生式 
  Α→α,Α→β均满足下面条件(其中α和β不能同时推出ε): 
  1、FIRST(α)∩FIRST(β)=Φ 
 ```

## 4.5试证明： 任何LL(1)文法均为无二义性文法。（3分）

 ```
 存在二义性 也就是说在表格中 非终结符S到终结符a的那一格会有大于1的路径
 这与LL(1)文法的定义不符 
 LL(1)文法在每一步替换的时候 都应该是确定的
 ```

## 4.6验证下列文法是否为LL(1)文法。（4分）

* (1)
```
S→AB|CDa

A→ab|c

B→dE

C→eC|ε

D→fD|f

E→dE|ε
```
```
显然 D的两个产生式的first集交集为{f} 不是LL(1)
```

* (2)
```
S→aABbCD|ε

A→ASd|ε

B→Sac|eC|ε

C→Sf|Cg|ε

D→aBD|ε
```
```
显然 A是直接左递归的 所以不是LL(1)
```