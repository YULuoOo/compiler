# 编译原理作业五
## 思考题 在计算followpos时，为什么只要concatenation-node和star-node算子就行？为什么不需要"|"算子？

    从表面来理解，如果是|符号，例如 S1 | S2  显然S1S2只能取一，不可能S1后接上S2  
    从直接构造法计算followpos的算法来看，star-node算子的firstpos和lastpoos即为子节点的两者  
    concatenation-node算子也确保了两个子节点必然被计算到
    所以只需要只要concatenation-node和star-node算子，就能覆盖到"|"算子两边的节点
    
    
