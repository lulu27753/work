## Set 集合

- 无重复元素的列表
- has()查找键名

## Map集合

- Map集合内含多组键值对，集合中每个元素分别存放着可访问的键名和它对应的值
- has()查找键值
- 键可以是“数字”、“对象”
- 常用于缓存频繁取用的数据

## WeakSet

- 成员只能是对象
- 成员都是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象是否还存在于 WeakSet 中，