- SQL 查询处理的步骤序号:

  > (1) FROM <left_table>
  > (2) <join_type> JOIN <right_table> 
  > (3) ON <join_condition>
  > (4) WHERE <where_condition>
  > (5) GROUP BY <group_by_list>
  > (6) WITH {CUBE | ROLLUP}
  > (7) HAVING <having_condition> 
  > (8) SELECT
  > (9) DISTINCT
  > (9) ORDER BY <order_by_list>
  > (10) <TOP_specification> <select_list>

- 以上每个步骤都会产生一个虚拟表，该虚拟表被用作下一个步骤的输入。这些虚拟表对调用 者(客户端应用程序或者外部查询)不可用。只有最后一步生成的表才会会给调用者。如果没有在 查询中指定某一个子句，将跳过相应的步骤。

- 逻辑查询处理阶段

  >1、 FROM:对 FROM 子句中的前两个表执行笛卡尔积(交叉联接)，生成虚拟表 VT1。2、 ON:对 VT1 应用 ON 筛选器，只有那些使为真才被插入到 TV2。
  >3、 OUTER (JOIN):如果指定了 OUTER JOIN(相对于 CROSS JOIN 或 INNER JOIN)，保留
  >
  >表中未找到匹配的行将作为外部行添加到 VT2，生成 TV3。如果 FROM 子句包含两个以上的表， 则对上一个联接生成的结果表和下一个表重复执行步骤 1 到步骤 3，直到处理完所有的表位置。
  >
  >4、 WHERE:对 TV3 应用 WHERE 筛选器，只有使为 true 的行才插入 TV4。
  >5、 GROUP BY:按 GROUP BY 子句中的列列表对 TV4 中的行进行分组，生成 TV5。
  >6、 CUTE|ROLLUP:把超组插入 VT5，生成 VT6。
  >7、 HAVING:对 VT6 应用 HAVING 筛选器，只有使为 true 的组插入到 VT7。
  >8、 SELECT:处理 SELECT 列表，产生 VT8。
  >9、 DISTINCT:将重复的行从 VT8 中删除，产品 VT9。
  >10、 ORDER BY:将 VT9 中的行按 ORDER BY 子句中的列列表顺序，生成一个游标(VC10)。11、 TOP:从 VC10 的开始处选择指定数量或比例的行，生成表 TV11，并返回给调用者。where 子句中的条件书写顺序

- 事务的特性

  >1、**原子性**(Atomicity):事务中的全部操作在数据库中是不可分割的，要么全部完成，要么均不执 行。
  >
  >2、**一致性**(Consistency):几个并行执行的事务，其执行结果必须与按某一顺序串行执行的结果相 一致。
  >
  >3、**隔离性**(Isolation):事务的执行不受其他事务的干扰，事务执行的中间结果对其他事务必须是透 明的。
  >
  >4、**持久性**(Durability):对于任意已提交事务，系统必须保证该事务对数据库的改变不被丢失，即 使数据库出现故障