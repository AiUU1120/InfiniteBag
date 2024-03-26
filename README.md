# InfiniteBag
- 基于对象池实现BagItem的复用
- 可以只显示viewport区域内数量的Item来容纳无限多物品（上限取决于content高度上限）
### 边界条件
- 上边界Item索引minIndex: content锚点y坐标 / 单个Item占用高度 * 每行显示Item数量
- 下边界Item索引maxIndex: (content锚点y坐标 + viewport显示高度) / 单个Item占用高度 + 每行显示Item数量 - 1
### 更新逻辑
- 定义字典存储当前显示Item对象 键:Item索引 值:GameObject
- 每帧执行更新方法，遍历minIndex ~ maxIndex，当字典中不存在索引范围内Item时从对象池获取Item并加入
- 记录上一次更新的索引oldMinIndex与oldMaxIndex
- 当oldMinIndex < minIndex，背包下拉，删除上部溢出Item
- 当maxIndex < oldMaxIndex，背包上拉，删除下部溢出Item
![](https://s3.bmp.ovh/imgs/2024/03/27/6d281e4c0743007b.png)
