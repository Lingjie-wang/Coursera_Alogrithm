# Coursera: Algorithms I & II

## Module 2: Dynamic Conectivity

### quick-find alogrithm

![image-20240914174056304](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409141740375.png)

Quadratic algorithm do not scale

![image-20240914174410724](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409141744758.png)

### quick-union alogrithm

![image-20240914175638295](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409141756355.png)

the comparison between quick-union and quick-find

![image-20240914180045388](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409141800428.png) 

### quick-union improvements

![image-20240914184536212](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409141845324.png)

quick-union and weighted quick-union example

![image-20240914185104536](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409141851589.png)

java implementation for weighted quick-union

![image-20240914185641408](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409141856506.png)

weighted quick-union analysis

![image-20240914202508541](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409142025685.png)

Path compression: java implementation

![image-20240914203134755](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409142031801.png)

summary

![image-20240914204344735](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409142043787.png)

> 算法中lg*指的是什么
>
> ![image-20240914204654852](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409142046890.png)

### union-find application

the most important one is the **Percolation**

- how to  solve Dynamic connectivity solution to estimate percolation threshold

![image-20240917120612700](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409171206787.png)

How to solve this problem:
![image-20240917134823471](https://cdn.jsdelivr.net/gh/Lingjie-wang/picture@main/image/202409171348623.png)

> ### Steps:
>
> 1. **Initial Setup**:
>    - Start with a union-find data structure where every element from `0` to `n-1` is in its own set.
> 2. **Handling Removal**:
>    - When you remove an element `x`, you perform a **union** between `x` and `x+1`. This effectively means that when `x` is removed, its successor becomes `x+1`.
> 3. **Find Successor**:
>    - To find the successor of `x`, you perform a **find** operation on `x`. If `x` is removed, the find operation will return the representative of the set containing the smallest element greater than `x`.
> 4. **Union and Find with Path Compression**:
>    - Use **path compression** in the find operation to keep the data structure efficient, ensuring that both **find** and **union** operations run in **amortized logarithmic time**.

### lab:Percolation

> 在这段代码中，`ufForFull` 是一个 `WeightedQuickUnionUF` 对象，它的主要作用是用于检查某个站点是否是“满的”（即与顶部虚拟节点相连）。它与 `uf` 的作用有一些不同。
>
> 具体来说，`ufForFull` 的作用在于防止**错误的满站点判断**。在 `Percolation` 模型中，"满" 的定义是指某个站点可以通过已打开的路径与顶部虚拟节点相连。然而，如果 `uf` 中直接包含底部的虚拟节点（用于判断系统是否渗透），那么当系统渗透时，所有与底部相连的站点也会错误地被认为是“满的”，因为它们与顶部的节点通过底部间接相连了。
>
> 因此，`ufForFull` 排除了底部虚拟节点，只包含顶部虚拟节点，它仅用于判断一个站点是否与顶部虚拟节点相连，而不会影响系统的渗透性判断。这可以防止底部站点在系统渗透后被错误地标记为满的。
>
> 总结来说：
> - `uf` 包含顶部和底部虚拟节点，用于判断系统是否渗透。
> - `ufForFull` 只包含顶部虚拟节点，用于判断某个站点是否与顶部相连，即判断是否为满站点。