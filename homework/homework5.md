# 编译原理作业五
## 一、直接构造法构造这四个正则表达式的DFA，并且最小化DFA。
#### a) (a | b)\*

![Image text](https://github.com/YULuoOo/compiler/blob/master/homework/547DD9CD-30A4-4EB5-93F9-49BD074579B7.png)

| 节点 | followpos 
| - | :-: 
| 1 | {1,2,3}
| 2 | {1,2,3}
| 3 | ∅

    A = {1,2,3}  
    Dtran(A,a) = followpos(1)+followpos(3) = {1,2,3}  
    Dtran(A,b) = followpos(2) = {1,2,3}  
    **no new states!**

![Image text](https://github.com/YULuoOo/compiler/blob/master/homework/4EAE3D3C-ED7A-4714-9732-954EC1497032.png)  
<br/><br/><br/>
#### b) (a\* | b\*)\*  

![Image text](https://github.com/YULuoOo/compiler/blob/master/homework/F96F5678-2605-4649-8673-439831F30978.png)

| 节点 | followpos 
| - | :-: 
| 1 | {1,2,3}
| 2 | {1,2,3}
| 3 | ∅

    A = {1,2,3}  
    Dtran(A,a) = followpos(1)+followpos(3) = {1,2,3}  
    Dtran(A,b) = followpos(2) = {1,2,3}  
    **no new states!**

![Image text](https://github.com/YULuoOo/compiler/blob/master/homework/4EAE3D3C-ED7A-4714-9732-954EC1497032.png)



#### c) ((e | a)b\*)\* 

#### d) (a | b)\*abb(a | b)\*
