### 269.Alien-Dictionary

我们比较任何两个相邻的单词，逐个对比每个字母，可以得到两个字母之间的字典序大小的关系。如果a<b，那么我们就定义一条有向边a->b。

于是本题就转化为：有一系列的有向边，要求给出一个包括所有节点的顺序排列，使得任何一条边x->y的两个节点(x,y)在这个序列里的顺序都是满足x的位置在y之前。这是一个拓扑排序的问题，适合BFS来做。

我们需要预处理所有的节点，得到所有节点的入度值。在队列的初始值里，加入所有的外围字母（即入度为零的节点）。因为这些字母的入度为0，说明没有任何字母比它们更小，所以可以安全地放在字典序中的最前面（它们彼此之间的顺序无所谓）。接着在BFS过程中，每弹出一个字母x，就找到对应的后续节点y（可能有多个），并将y的入度减一（因为我们已经处理完了字母x）。如果此时y的入度降至0，那么我们就可以将其加入队列中，做为下一批的外围节点。

核心代码如下：
```cpp
while (!q.emtpy())
{
   char current = q.front();
   q.pop();
   for (auto next: Next[current])
   {
      inDegree[next]--;
      if (inDegree[next]==0)
        q.push(next);
   }
}
```


[Leetcode Link](https://leetcode.com/problems/alien-dictionary)
