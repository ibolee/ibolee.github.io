# Power Pivot Tips

1. 为什么power pivot在对时间划分的时候不能以365天每一天生成折线图?
+ 在设置中关闭全局和当前文件的[时间智能]
系统创建的日期表无法添加自定义字段,比如节假日;比如农历日期,法定节假日;还可以写度量值;
2. 如何关闭power pivot自动连线功能?
+ 在设置中关闭自动检测新关系即可;选项和设置----选项----数据加载---关掉[加载数据后自动检测新关系]
3. power bi可以直接导入Excel中创建好的查询
+ 操作步骤:文件→导入→点击第一个选项Power Query.→启动→等待导入完成→使用PBI从新做图.
+ 导入后原来的Excel查询与pb里的数据没有关联性;
4. power pivot表连接多对多报错怎么解决？
+ 这种情况就去建立桥接表，用distinct函数去建立；
![](https://img.ibolee.com/git_blog/distinct.png)

5.power bi 和power pivot导出数据到没有powerquery的excel

+ 在power query的表查询中，随便点一列，然后复制表，再到excel中去粘贴即可。

+ 直接在power bi的图标预览中点右上方三个点，导出数据即可。
