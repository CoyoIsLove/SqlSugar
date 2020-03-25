分支至原项目 5.0.0.11 版本，主要针对一些使用上的问题进行解决后自用。

## 已修改
1. 修复 `UpdateableProvider` 和 `InsertableProvider` 中无法正确识别**可空枚举**类型的字段，导致保存到数据库结果为 `0`。[commit 539db15](https://github.com/CoyoIsLove/SqlSugar/commit/4aa2d323031a5aa395a5584ecccca107541592bb)
2. 修复 `InsertableProvider` 中 `IInsertable<T> InsertColumns(Expression<Func<T, object>> columns)` 方法无法正确作用于某些标识了 `ColumnName` 的列的问题。[commit 539db15](https://github.com/CoyoIsLove/SqlSugar/commit/4aa2d323031a5aa395a5584ecccca107541592bb)
```csharp
[ColumnName("name")]
public string Name { get; set; } //生效
[ColumnName("book_desc")]
public string BookDesc { get; set; } //不生效
public double Price { get; set; } // 生效

Db.Saveable(entity).InsertColumns(x => new { x.Name, x.BookDesc, x.Price }).ExecuteCommand();
```
