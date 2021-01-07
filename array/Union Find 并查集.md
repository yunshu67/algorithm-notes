## 可以解决的问题

1. 给出未知类别的n个元素，将这些元素根据给定的规则进行划分类别

   

---





# Union Find 并查集

### Definition 

> **Union Find** is a data structure that keeps track of elements which are split into one or more disjoint sets.



### Two primary operations

1. `find(elem)`: return the group/class which $elem$ belongs to 
2. `union(e1,e2)`: unify two elements $e1$ and $e2$ 



### Complexity

|     Operation      | Time Complexity |
| :----------------: | :-------------: |
|    construction    |      O(n)       |
|       union        |      a(n)       |
|        find        |      a(n)       |
| Get component size |      a(n)       |
| check if connected |      a(n)       |
|  Count components  |      O(1)       |
- **a(n)**: amortized constant time



### Represent of an element node

1. struct

```c
#define MAX 10000
struct Node
{
    int data;		// 该元素保存的数据
    int rank;		// 以该元素为root形成的子树的高度
    int parent; // parent node
 }node[MAX];
```

2. array

```c
int set[max];//集合index的类别，或者用parent表示
int rank[max];//集合index的层次，通常初始化为0
int data[max];//集合index的数据

//初始化集合
void Make_Set(int i)
{
    set[i]=i;//初始化的时候，一个集合的parent都是这个集合自己的标号。没有跟它同类的集合，那么这个集合的源头只能是自己了。
    rank[i]=0;
}
```



### Algorithm

- 用集合中的某个元素来代表这个集合，该元素称为集合的`代表元`。

- 每个集合都是以集合的`代表元`为**root**,其余元素为**child**的树形结构。

- `parent(x)` : return the parent node of element `x`.
  
  - `parent(root) = root` 
  
- `find(x)` returns the group/set/class of element `x`, ==which in essence is to search the `代表元` of this group/set/class==
  
  - 可以沿着`parent(x)`不断在树形结构中向上移动，直到到达根节点。
  
- `union(e1,e2)`:

  ```python
  # to unify two elements, first find their roots
  root1 = root of e1
  root2 = root of e2
  
  # if roots are different, let one be the parent of the other
  if root1 == root2:
    return
  else:
    parent[root1] = root2 / parent[root2] = root1
  ```
  
  - 在合并两个子树/集合时，可以将高度`rank`较小的作为 **child**, to prevent the degeneration from tree to list.





