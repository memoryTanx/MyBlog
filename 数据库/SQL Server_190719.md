MS SQL Server 清除缓存

> 在性能调优的时候，清空缓存是必需的，缓冲池（Buffer Pool)是 SQL Server 的缓存管理器，包含了 SQL Server 的绝大部分的缓存数据（Cache）。
> 例如：计划缓存（Plan Cache），数据缓存（Data Cache)等


清空缓存的命令有三个：

```sql
CHECKPOINT

DBCC DROPCLEANBUFFERS

DBCC FREEPROCCACHE
```


分别解释一下：

**CHECKPOINT**：用于清空脏的数据缓存
> CHECKPOINT 用于将脏页（Dirty Pages）写入硬盘，脏页（Dirty Pages) 是指数据从硬盘读到内存中，
> 就是被读到缓存中，然后被修改过，导致内存中的数据页和硬盘中的数据页的内容不同。


**DBCC DROPCLEANBUFFERS**：用于清空干净的数据缓存
> 干净页（Clean Pages) 是指数据页被从硬盘读到内存中，没有被修改过的数据，
> 这样内存中的数据页和硬盘中的数据页的内容是相同的


**DBCC FREEPROCCACHE**：用于清空计划缓存


不管是 Dirty Pages 还是 Clean Pages 都是 Data Cache
