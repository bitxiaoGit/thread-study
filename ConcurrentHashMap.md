
# ConcurrentHashMap
> * 底层采用分段的数组+链表实现，***线程安全***
> * 通过把整个Map分为N个Segment，可以提供相同的线程安全，但是效率提升N倍，默认提升16倍。(读操作不加锁，由于HashEntry的value变量是 volatile的，也能保证读取到最新的值。)
> * 允许多个修改操作并发进行，其关键在于使用了 ***锁分离技术***
> * 对于需要锁定整个Map的方法，例如size()和containsValue()，在操作完成后，按顺序释放所有段的锁
> * 段内扩容（段内元素超过该段对应Entry数组长度的75%触发扩容，不会对整个Map进行扩容），插入前检测需不需要扩容，有效避免无效扩容

# HashTable
> * 底层数组+链表实现，无论key还是value都 ***不能为null，线程安全***
> * 修改数据时锁住整个HashTable，效率低，ConcurrentHashMap做了相关优化
> * 初始size为11，扩容：newsize = olesize*2+1
> * 计算index的方法：index = (hash & 0x7FFFFFFF) % tab.length

# HashMap
> * 底层数组+链表实现，可以 ***存储null键和null值***，***线程不安全***
> * 初始size为16，扩容：newsize = oldsize*2，size一定为2的n次幂
> * 扩容针对整个Map，每次扩容时，原来数组中的元素依次重新计算存放位置，并重新插入
> * 插入元素后才判断该不该扩容，有可能无效扩容（插入后如果扩容，如果没有再次插入，就会产生无效扩容）
> * 当Map中元素总数超过Entry数组的75%，触发扩容操作，为了减少链表长度，元素分配更均匀
> * 计算index方法：index = hash & (tab.length – 1)



>> gfda
