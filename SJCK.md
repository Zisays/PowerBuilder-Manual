## 1、CRUD



### （1）、将编辑的数据放到主缓冲区



```c
dw_1.accepttext()
```



### （2）、增加数据



```c
dw_1.insertrow(0)
```



### （3）、删除数据



[ 1 ]、删除第一行



```c
dw_1.deleterow(1)
```



[ 2 ]、保留数据窗口第1行，并循环删除其他行



```c
for ll_i = dw_1.rowcount() to 1  step - 1
	if ll_i = 1 then
		dw_1.object.字段名[1] = 值
	else
		dw_1.deleterow(ll_i)
	end if
next
```



### （4）、更新数据



```c
string ls_err
if dw_1.update() = 1 then
	commit using sqlca;
	messagebox('提示','更新成功')
else
	ls_err = sqlca.sqlerrtext
	rollback using sqlca;
	messagebox('提示','更新失败' + ls_err)
end if
```



### （5）、检索数据



[ 1 ]、设置数据窗口控件外部事务对象，必须指定connect,commit,disconnect



```c
dw_1.settransobject(sqlca)
dw_1.retrieve()
```



[ 2 ]、设置数据窗口控件内部事务的值。自动connect,commit,disconnect



```c
dw_1.settrans(sqlca)
dw_1.retrieve()
```



## 2、赋值与取值



### 1、赋值



```c
dw.setitem(行,  '列名称', 值)
dw.object.列名[行号] = 值
```



### 2、取值



```c
dw_1.object.字段名(行数) //直接取值
dw_1.object.标题名.text  //标题文本框
dw_1.GetItemString(行数,列名) //字符串
dw_1.GetItemNumber(行数,列名) //数值
dw_1.GetItemDate(行数,列名) //日期
dw_1.GetItemDateTime(行数,列名) //日期时间
dw_1.GetItemDecimal(行数,列名) //小数
```



## 3、行



### （1）、行处理



```c
dw_1.rowcount() //获取总行 
dw_1.getrow() //获取当前行
dw_1.setrow(1) //设置当前行
dw_1.scrolltorow(1) //滚动到目标行
dw_1.selectrow(1, true) //将第一行变成选中状态
dw_1.isselected(1) //检查第一行是否被选择
```



### （2）、高亮显示



[ 1 ]、在数据窗口的click事件中，写入以下代码



```c
if row > 0 then
	this.setrow(row)
	this.selectrow(0,false)
	this.selectrow(row,true)
end if
```



[ 2 ]、在数据窗口rowfocuschanged事件中，写入以下代码



```c
if currentrow > 0 then
	this.scrolltorow(currentrow)
	this.selectRow(0, false)
	this.selectRow(currentrow,true)
end if
```



### （3）、隔行换色



[ 1 ]、打开数据窗口



[ 2 ]、右键 `detail`



[ 3 ]、找到右侧 `color` 属性右侧的小图标



[ 4 ]、在表达式中输入以下代码



```c
if ( mod( getrow() ,  2) = 1 , rgb(255,255,255) , rgb(235,255,235) )
```



### （4）、自增行



[ 1 ]、添加计算列，`page n of n`



[ 2 ]、输入`getrow()`



### （5）、移动行



语法：dw_name.rowsmove(开始行,结束行,缓冲区,要移动到的另一窗口名,在哪一行前面插入,插入哪个缓冲区)



可选参数：



primary!	  主缓冲区



delete!		 删除缓冲区



filter!			过滤缓冲区



```c
例子：从删除缓冲区移动行到主缓冲区实现恢复功能： 
dw_1.deleterow(1) //删除第1行 
dw_1.rowsmove(1,dw_1.deletedcount(),delete!,dw_1,1,primary!) //恢复第1行
```



### （6）、复制行



语法：dw_name.rowscopy(开始行,结束行,缓冲区,要复制到的另一窗口名,在哪一行前面插入,插入哪个缓冲区)



```c
例子：
dw_1.deleterow(1) //删除第1行
dw_1.rowscopy(1,dw_1.deletedcount(),delete!,dw_1,1,primary!) //复制第1行
```



### （7）、设置行为只读



```c
long i
for i=1 to dw_1.rowcount()
	dw_1.Modify("字段名.Protect='" + string(i) + "~tif(表示只读状态字段=1, 1,0)'")
next
```



## 4、列



### （1）、获得数据窗口的列名



```c
integer li_index
for li_index = 1 to integer(dw_1.object.datawindow.column.count)
	messagebox(string(li_index),dw_1.describe("#" + string(li_index) + ".name"))
next
```



### （2）、获得字段对应的dbname



```c
integer li_index
for li_index = 1 to integer(dw_1.object.datawindow.column.count)
	messagebox(string(li_index),dw_1.describe("#" + string(li_index) + ".dbname"))
next
```



### （3）、复制列



```c
dw_1.object.字段名.primary = dw_1.object.字段名.primary
```



### （4）、获取显示列



```c
describe('DataWindow.Table.GridColumns')
```



### （5）、设置列为只读



```c
方式1、将tab order 设置为0
方式2、dw_1.modify("cname.tabsequence = 0  ")
方式3、dw_1.modify( "meno.edit.displayonly=yes")
方式4、dw_1.modify("code_course.protect= 1")
```



## 5、过滤



### （1）、列名过滤



```c
dw_1.setfilter("isnull(列名)")
dw_1.filter()
```



### （2）、条件过滤



```c
dw_1.setfilter("列名='" + 列值 + "'")
dw_1.filter()
```



### （3）、清除过滤



方式1：



```c
dw_1.setfilter('')
dw_1.filter()
```



方式2：



```c
dw_1.setfilter('1=1')
```



### （4）、SQL语句过滤



```c
sql = 'select * from 表名 where isnull(字段名 , ''空'') = ''空'' ' ;
```



## 6、排序



### （1）、正序排列



```c
dw_1.setsort("列名 a")
dw_1.sort()
```



### （2）、倒序排列



```c
dw_1.setsort("列名 d")
dw_1.sort()
```



### （3）、双击排序



```c
string ls_old_sort, ls_column
char  lc_sort
if right(dwo.name,2) = '_t' then
 ls_column = left(dwo.name, len(string(dwo.name)) - 2)
 ls_old_sort = this.describe("datawindow.table.sort")
 if ls_column = left(ls_old_sort,  len(ls_old_sort) - 2)  then
 lc_sort = right(ls_old_sort, 1)
 if lc_sort =  'a' then
  lc_sort = 'd'
 else
  lc_sort = 'a'
 end if
 this.setsort(ls_column + " " +  lc_sort)
 else
 this.setsort(ls_column + "  a")
 end if
 this.sort()
end if
```



## 7、分页



（1）、增加一个计算列
此计算列必须放在detail段
expression中输入: ceiling(getrow()/500)  <--这里500还可以用全局函数取代
这样可以允许用户任意设置每页多少行。



（2）、定义分组,选择菜单rows->create group...
按计算列字段分组，并一定将check box-->new page on group  break选中。



（3）、将此计算列设为不可视
然后添加以下按钮，完成分页功能



[ 1 ]、首页



```c
dw_1.scrolltorow(0)
dw_1.setrow(0)
```



[ 2 ]、上一页



```c
dw_1.scrollpriorpage()
```



[ 3 ]、下一页



```c
dw_1.scrollnextpage()
```



[ 4 ]、尾页



```c
dw_1.scrolltorow(dw_1.rowcount())
dw_1.setrow(dw_1.rowcount())
```



## 8、在 `SQL` 中传递 `in`



```c
//注：在传给数据窗口时，in中的内容必须是数组类型

string ls_in[]
for i = 1 to dw_1.rowcount()
 ls_in[i] =  string(dw_1.object.test[i])
next

dw_1.retrieve(ls_in)
```



## 9、操作子数据窗口



```c
integer rtncode
datawindowchild dwc_child
rtncode = dw_1.getchild("主窗口字段", dwc_child)
if rtncode = 1 then
 messagebox('',dwc_child.getitemstring(1,'子窗口字段'))
else
 messagebox('提示','未获取到子数据窗口!')
end if
```



## 10、判断数据窗口是否修改



```c
//判断数据窗口是否修改,建议写在closequery事件中
dw_1.accepttext()
if dw_1.modifiedcount() + dw_1.deletedcount() > 0 then
	messagebox('提示','数据窗口已经修改,是否保存？')
else
	messagebox('提示','数据窗口没有修改,正常退出')
 end if
```



## 11、数据窗口状态



### （1）、获取数据窗口状态



当第一次使用retrieve()函数从数据库中读取数据时，所有在数据窗口缓冲区的记录与字段都是属于NotModified!状态。
当时数据被修改过后，被修改过的记录状态标志与字段状态标志都会被改成DataModified!
当增加一笔数据时，增加数据的字段状态标志为NotModified!,记录状态标志为New!.
当我们在增加的字段中填上数据后，字段状态标志为DataModified！记录状态标志为NewModified!



```c
if dw_1.getitemStatus(1,dw_1.deletedcount(),primary!) = datamodified! then
	messagebox('1:已修改数据','datamodified!')
elseif dw_1.getitemStatus(1,dw_1.deletedcount(),primary!) = new! then
	messagebox('2:已增加数据','new!')
elseif dw_1.getitemStatus(1,dw_1.deletedcount(),primary!) = newmodified! then
	messagebox('3:已填写数据','newmodified!')
elseif dw_1.getitemStatus(1,dw_1.deletedcount(),primary!) = notmodified! then
	messagebox('4:未修改数据','notmodified!')
end if
```



### （2）、设置数据窗口状态



```c
dw_1.setitemstatus(1,dw_1.deletedcount(),primary!,notmodified!)
```



## 12、多选框



（1）、在数据窗口的sql中，添加多选框字段



```c
'ls_checkbox' = '0',
```



（2）、设置字段的`edit`属性为`checkbox`，并勾选`3d look`



（3）、设置(data value for on = 1)，设置(data value for off = 0)



（4）、再dw_1数据窗口的click事件中写



```c
if dwo.name =  "ls_checkbox_t" then
 if dw_1.rowcount() = 0 then
 else
 if  dw_1.object.ls_checkbox[1] = "1" then
  for row = 1 to  dw_1.rowcount()
  dw_1.object.ls_checkbox[row] =  "0"
  next
 else
  for row = 1 to  dw_1.rowcount()
  dw_1.object.ls_checkbox[row] = "1"
  next
 end  if
 end if
end if
```



（5）、如何取值？



```c
long cbx_i
if  dw_1.rowcount() = 0 then return 0
for cbx_i = 1 to dw_1.rowcount()
 if  dw_1.getitemstring(cbx_i, "ls_checkbox") = '1' then
 end if
next
```



## 13、数据窗口SQL语句



（1）、获取数据窗口 `SQL` 语句



```c
dw_1.getsqlselect()
```



（2）、设置数据窗口的 `SQL` 语句



```c
string ls_sql
ls_sql = 'select * from test'
dw_1.setsqlselect(sql)
```



## 14、DataStore



```c
datastore lds_test
lds_test = create  datastore

//给实例化后的datastore变量关联数据窗口对象
lds_test.dataobject =  'd_main'

//给数据存储对象指定事务对象
lds_test.settransobject(sqlca)

//接下来就和操作普通数据窗口一样了（例）
lds_test.insertrow(0)
lds_test.object.title[1]  = '我是测试标题'
messagebox('',string(lds_test.object.title[1]))
```



## 15、动态数据窗口



### （1）、describe（获取数据窗口中的各种属性）



```c
messagebox('获取字段名称',dw_1.Describe("#1.name")) //title
messagebox('获取字段类型',dw_1.Describe("title.ColType")) //char(10)
messagebox('获取字段背景颜色',dw_1.Describe("title.background.color")) //536870912
messagebox('获取字段背景模式',dw_1.Describe("title.background.mode")) //1
messagebox('获取字段是否允许自动横向滚动',dw_1.Describe("title.edit.Autohscroll")) //yes
messagebox('获取字段是否为主键',dw_1.Describe("title.key")) //no
messagebox('获取字段中的数据保护',dw_1.Describe("title.protect")) //0
messagebox('获取字段的滑动属性（当左面空白时是否向左滑动）',dw_1.Describe("title.SlideLeft")) //no
messagebox('获取字段的滑动属性（当上面出现空白时是否向上滑动）',dw_1.Describe("title.slideup")) //no
messagebox('获取字段的TabOrder值',dw_1.Describe("title.tabsequence")) //10
messagebox('获取字段是否可以修改',dw_1.Describe("title.update")) //no
messagebox('获取字段的校验规则',dw_1.Describe("title.validation")) //?
messagebox('获取字段的表达式',dw_1.Describe("title.expression"))
```



### （2）、modify（修改数据窗口中的各种属性）



```c
messagebox('隐藏字段',dw_1.modify("title.visible='1'"))
messagebox('修改字段背景模式',dw_1.modify("title.background.mode='1'"))
messagebox('修改字段背景颜色',dw_1.modify("title.background.color  = '0'"))
messagebox('修改检索规则',dw_1.modify("title.criteria.dialog = yes  sex.criteria.override_edit  =yes"))
messagebox('修改字段显示格式为日期格式',dw_1.modify("title.format =  'yyyy-mm-dd'"))
messagebox('修改字段为主键',dw_1.modify("title.key =  yes"))
messagebox('修改字段的保护属性',dw_1.modify("title.protect =  '1~tif(isrownew(),0,1)'"))
dw_1.modify("字段名.expression='表达式值'")  //修改数据窗口表达式
```



### （3）、syntaxfromsql（动态创建数据窗口）



```c
//连接默认事务sqlca
sqlca.dbms = "mss microsoft sql server"
sqlca.database = "数据库名称"
sqlca.logpass = '登陆密码'
sqlca.servername = "服务器名称或ip"
sqlca.logid = "服务器登陆用户名"
sqlca.autocommit = false
sqlca.dbparm = ""
connect using sqlca;

string dw_sql,dw_style
string dw_syntax,dw_syntax_error,dw_create_error

//设置数据窗口sql
dw_sql = "select * from 表名"

//设置数据窗口风格
dw_style = "style(type=grid)"

//构造sql数据源
dw_syntax = sqlca.syntaxfromsql(dw_sql, dw_style, dw_syntax_error)

//判断sql数据源是否有错误
if len(dw_syntax_error) > 0 then
	messagebox("提示", "构造sql数据源错误: " + dw_syntax_error)
	return
end if

//通过sql数据源创建dw_1数据窗口
dw_1.create(dw_syntax,dw_create_error)

//判断dw_1数据窗口在创建中是否有错误
if len(dw_create_error) > 0 then
	messagebox("提示", "创建数据窗口错误: " + dw_create_error)
	return
end if

//检索数据
dw_1.settransobject(sqlca)
dw_1.retrieve()
```



## 16、导入导出



### （1）、数据窗口导入



```c
//dw_1.importfile(导入的文件类型, 文件名, 文件的开始行 , 文件的结束行, 文件的开始列, 文件的结束列, 数据窗口的开始列 )
//因为导出的数据窗口都有标题，所以我们这边从第2行开始导入
dw_1.importfile(text!,'1.txt',2,10,1,10,1) //导入txt文件
dw_1.importfile(excel!,'1.xls',2,10,1,10,1) //导入xls文件
dw_1.importfile(excel!,'1.xlsx',2,10,1,10,1)//导入xlsl文件
dw_1.importfile(csv!,'1.csv',2,10,1,10,1)//导入csv文件
```



### （2）、数据窗口导出



```c
//dw_name.saveas(名字可含路径,另存为的类型,是否显示列标题)
dw_1.saveas("1.txt",text!,true)  //另存为txt文件
dw_1.saveas("1.xls",excel!,true) //另存为xls文件
dw_1.saveas("1.xlsx",excel!,true) //另存为xlsl文件
dw_1.saveas("1.csv",csv!,true) //另存为csv文件
```



## 17、数据窗口快捷键



```c
//1、新建事件
事件名   keydown
event ID  pbm_dwnkey（选择这个就可以了，其他参数它会自己设置）

//2、在此事件中，写入以下代码
if key = KeyEnter! then  Send(Handle(this),256,9,0)
```



## 18、设置当前行指示图标



（1）、在datawindow中建立一个计算列,expression为'',并将该计算列移动为datawindow的第一个列
（2）、在datawindow控件的rowfocuschanged事件中写入以下代码



```c
SetRowFocusIndicator(hand!) //小手指样式
setrowfucsindicator(p_1) //自定义图片样式
```



## 19、打印数据窗口的内容到文件中



将数据窗口打印出 pdf 文件



```c
dw_1.object.datawindow.print.filename ="c:/temp.pdf"
dw_1.print()
```



## 20、将Grid风格改成自由格式



```c
在DW的editsource中将processing=1的1改为0
```



## 21、自动高度



（1）、点中`Detail Band` (即写有`Detail`的灰色长带), 选中右侧的`Autosize Height`多选框



（2）、点击你要设置的列名



（3）、选择右侧的`Position`选项, 选中`Autosize Height` 多选框



（4）、选择右侧的`Edit`选项，去掉`Auto Horz Scroll`并勾选`Auto Vert Scroll`



## 22、下拉框



### 1、设置下拉框只读但不可修改



```c
dw_1.modify("qydd.dddw.allowedit=no")
```



### 2、获取下拉窗口显示值



```c
messagebox('获取显示值的属性',dw_1.Describe("Evaluate('LookupDisplay(sex)',1)")) //后面这个1是行号
```



## 23、其他



### （1）、dw_1.find



查找条件表达式,开始行, 结束行



如果表达式成立，那么就返回符合条件的行号



```c
dw_1.find('id=8',1,10)
```



### （2）、设置焦点



```c
dw_1.setfocus()
dw_1.setrow("数据行号")
dw_1.setcolumn("字段名")
```



### （3）、切换数据窗口



```c
dw_1.dataobject = "数据窗口名"
```



### （4）、隐藏数据窗口刷新过程



```c
dw_1.setredraw(false) //不刷新
dw_1.setredraw(true) //刷新
```



### （5）、数据窗口共享



```c
dw_2.sharedata(dw_1)
```



### （6）、数据窗口重置



```c
dw_1.reset()
```



### （7）、数据窗口重新分组



```c
//在我们处理过滤和排序后，如果是分组窗口可能会破坏分组规则，所以我们要进行重新分组
//重新分组一般都是在filter()或sort()后面
dw_1.groupcalc()
```