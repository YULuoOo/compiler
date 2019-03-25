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
--- 
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

<br/><br/><br/>
--- 

#### c) ((e | a)b\*)\* 
((e | 1)2\*)\*3


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

#### d) (a | b)\*abb(a | b)\*
(1 | 2)\*345(6 | 7)\*8

![Image text](https://github.com/YULuoOo/compiler/blob/master/homework/13DC8933-B706-4328-ACA8-D92A0B0C9C17.png)  

| 节点 | followpos 
| - | :-: 
| 1 | {1,2,3}
| 2 | {1,2,3}
| 3 | {4}
| 4 | {5}
| 5 | {6,7,8}
| 6 | {6,7,8}
| 7 | {6,7,8}
| 8 | ∅

    S={1,2,3}
    move(S,a) = 1 + 3 = {1,2,3,4} = S1
    move(S,b) = 2 = {1,2,3} = S
    move(S1,a) = 1 + 3 = S1
    move(S1,b) = 2 + 4 = {1,2,3,5} = S2
    move(S2,a) = S1
    move(S2,b) = 2 + 5 = {1,2,3,6,7,8} = S3 为退出状态
    move{S3,a} = 1 + 3 + 6 = S3
    move(S3,b) = 2 + 7 = S3

| 节点 | a | b 
| - | :-: | :-: |
| S | S1 | S
| S1 | S1 | S2
| S2 | S1 | S3
| S3 | S3 | S3

    没有最小化的必要，已经是最小
    
![Image text](https://github.com/YULuoOo/compiler/blob/master/homework/33586078-54D1-407F-BD33-D8B96FB2E08D.png)  



