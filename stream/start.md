### Java8 Stream原理

#### 常用流操作分类

- 中间操作(Intermediate operations)
  - 无状态(Stateless)
    - unordered
    - filter
    - map
    - mapToInt
    - mapToLong
    - mapToDouble
    - flatMap
    - flatMapToLong
    - flatMapToDouble
    - peek
  - 有状态(Stateful)
    - distinct
    - sorted
    - limit
    - skip
- 结束操作(Terminal operations)
  - 非短路操作
    - forEach
    - forEachOrdered
    - toArray
    - reduce
    - collect
    - max
    - min
    - count
  - 短路操作(short-circuiting)
    - anyMatch
    - allMatch
    - noneMatch
    - findFirst
    - findAny

#### 叠加

stage中记录了每一步操作,此事并没有执行,sink接口确定了如何执行

- `begin`:开始遍历元素之前调用该方法,通知sink做好准备
- `end`:所有元素遍历完成之后调用,通知sink没有更多元素了
- `cancellationRequested`:是否可以结束操作,让短路操作尽早结束
- `accept`:遍历元素的时候调用,接受一个待处理元素,并对元素进行处理

#### 并行原理

TODO