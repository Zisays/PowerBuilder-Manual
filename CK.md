## 1、通过窗口传递参数



### （1）、字符串



```c
// 1、当前窗口 ——> 传递
openwithparm( 新窗口名称 , '1' )

// 2、新窗口 ——> 接收
string  ls_str 
ls_str = message.stringparm
messagebox('提示',ls_str);
```



### （2）、数值



```c
// 1、当前窗口 ——> 传递
openwithparm( 新窗口名称 , 1 )

// 2、新窗口 ——> 接收
double  ldb_double
ldb_double = message.doubleparm
messagebox('提示',ldb_double);
```



### （3）、结构体



```c
// 1、当前窗口 ——> 传递
st_parameter s_pm
s_pm.a = 1
openwithparm( 新窗口名称 , s_pm )

// 2、新窗口 ——> 接收
st_parameter s_pm 
s_pm =  message.powerobjectparm
messagebox('提示',s_pm.a)
```



### （4）、用户对象



```c
// 1、当前窗口 ——> 传递
u_parameter  u_pm
u_pm = create u_parameter
u_pm.a = '1'
openwithparm( 新窗口名称 , u_pm )

// 2、新窗口 ——> 接收
u_parameter u_pm 
u_pm =  message.powerobjectparm
messagebox('提示',u_pm.a)
```



### （5）、可视化类用户对象传值



```c
u_customvisual u_cv
u_cv = create  u_customvisual
openuserobjectwithparm(u_cv,1)
```



## 2、通信



### （1）、当前窗口



```c
//1、传递 string 消息
w_main.triggerevent('ue_open',0,'test')
//在用户自定义事件 ue_open 中接收消息：
string ls_msg
ls_msg = string(message.longparm,'address')

//2、传递 long 消息
w_main.triggerevent('ue_open',100,0)
//在用户自定义事件 ue_open 中接收消息：
long ll_msg
ll_msg = message.wordparm
```



### （2）、新的应用程序



```c
// 1、当前程序 ——> 传递到新的应用程序
ls_exe = 'a.exe' + '|值1|' + '|值2|'
run(ls_exe)

// 2、新的应用程序 ——> 接收
string ls_parameter 
ls_parameter = commandparm()
```



## 3、动态触发事件与函数



### （1）、立即触发



```c
对象名.triggerevent(clicked!)		// 事件 { clicked! }
对象名.trigger event  ue_init()	// 事件 { ue_init }
对象名.trigger function wf_init()	// 函数 { wf_init }
```



### （2）、在事件队列最后触发



```c
对象名.postevent(clicked!) 		// 事件 { clicked! }
对象名.post event ue_init()		// 事件 { ue_init }
对象名.post function wf_init()		// 函数 { wf_init }
```



### （3）、动态绑定触发



```c
对象名.dynamic event ue_init()		// 事件 { ue_init }
对象名.dynamic function  wf_init()	// 函数 { wf_init } 

/*
注：
动态调用和静态调用的区别
静态调用就是在编译代码时就对函数进行彻底编译
动态调用就是在程序执行的时候才回去查找和调用相应的函数 
*/
```



### （4）、在规定的时间内触发



```c
//如果 60 秒没有任何操作的话就触发 {application} 对象的 {idle} 事件
idle(60) 

//每隔 60 秒就触发一次当前窗口的 {timer} 事件
timer(60)
```



## 4、游标



### （1）、用 for 循环实现游标



注：在项目中使用的时候，请去掉注释



```c
long ll_count = 10

//定义游标
string test

//声明游标
declare test cursor for 

// SQL 语句
select 字段名 from  表名 where 表达式 using sqlca; 

//打开游标
open test; 

for i=1 to ll_count
 //获取数据
 fetch test into :变量名; 
 
 //在这里写你的业务
 
next

//关闭游标
close test;
```



### （2）、用 do while 循环实现游标



注：在项目中使用的时候，请去掉注释



```c
//定义游标
string test 

//声明游标
declare test cursor for 
    
// SQL语句
select 字段名 from 表名 where 条件 using sqlca;

//打开游标
open test;

//获取数据
fetch test into:字段名变量;

do while sqlca.sqlcode = 0

 //在这里写你的业务
 
 //再次获取数据
 fetch test into:字段名变量; 
 
loop

//关闭游标
close test;
```



## 5、存储过程



### （1）、处理结果集



```c
string ls_stuno
string ls_stuname
string ls_stuage
string ls_stusex
string ls_result
integer fetchcount = 0

ls_stuno = '06'
ls_stuname = '张三'
ls_stuage = '1980-01-01'
ls_stusex = '男'

//此处声明存储过程名称
declare emp_proc  procedure for stu11
 @stuno = :ls_stuno,
 @stuname = :ls_stuname,
 @stuage = :ls_stuage,
 @stusex = :ls_stusex,
 @result = :ls_result output using sqlca;

//执行存储过程
execute emp_proc;
choose case sqlca.sqlcode
 case 0
  //处理结果集
  do
   fetch emp_proc  into:ls_result ;
   choose case sqlca.sqlcode
    case 0
     messagebox('结果集',ls_result)
     fetchcount ++
    case 100
     commit using sqlca;
     messagebox ("结果集结束",'共执行' + string (fetchcount) + " 条数据")
    case - 1
     rollback using sqlca;
     messagebox ("存储过程结果集获取失败",string (sqlca.sqldbcode) + " = " + sqlca.sqlerrtext)
   end choose
  loop while sqlca.sqlcode = 0
 case 100
  rollback using sqlca;
  messagebox ("执行成功", "无结果集")
 case else
  rollback using sqlca;
  messagebox ("存储过程执行失败",string (sqlca.sqldbcode) + " = " + sqlca.sqlerrtext)
end choose

//关闭存储过程
close emp_proc;
```



### （2）、处理返回值



```c
string ls_stuno
string ls_stuname
string ls_stuage
string ls_stusex
string ls_result
integer fetchcount = 0

ls_stuno = '06'
ls_stuname = '张三'
ls_stuage = '1980-01-01'
ls_stusex = '男'

//此处声明存储过程名称
declare emp_proc  procedure for stu11
 @stuno = :ls_stuno,
 @stuname = :ls_stuname,
 @stuage = :ls_stuage,
 @stusex = :ls_stusex,
 @result = :ls_result output using sqlca;

//执行存储过程
execute emp_proc;

choose case sqlca.sqlcode
 case 0
  //执行一次fetch语句以获取return值和output参数
  fetch emp_proc  into:ls_result ;
  choose case sqlca.sqlcode
   case 0
    commit using sqlca;
    messagebox ("获取返回值和输出参数成功", "返回值是: " + string (ls_result))
   case 100
    messagebox ("提示", "未找到返回值和输出参数")
   case else
    rollback using sqlca;
    messagebox ("获取返回值和输出参数失败", "sqldbcode is " + string (sqlca.sqldbcode) + " = " + sqlca.sqlerrtext)
  end choose
 case 100
  rollback using sqlca;
  messagebox ("执行成功", "无结果集")
 case else
  rollback using sqlca;
  messagebox ("存储过程执行失败",string (sqlca.sqldbcode) + " = " + sqlca.sqlerrtext)
end choose

//关闭存储过程
close emp_proc;
```



## 6、直接执行 `SQL` 语句



```c
string ls_sql,ls_err
ls_sql = "update 表名 set 字段名 =:字段值 where 表达式条件"
execute immediate :ls_sql using sqlca;
if sqlca.sqlcode = 0 then
    commit using sqlca;
    messagebox('提示','执行成功')
else
    ls_err =  sqlca.sqlerrtext
    rollback using sqlca;
    messagebox('提示','执行失败' + ls_err)
end if
```



## 7、直接访问 `web` 地址



```c
Inet iinet_base
GetContextService("Internet", iinet_base)
iinet_base.HyperlinkToURL('www.baidu.com')
```



## 8、弹窗



语法：messagebox(标题,内容,左侧的图标,对话框底部的按钮,按钮编号)



（1）、左侧的图标



```c
1、information!默认值
2、stopsign!
3、exclamation!
4、question!
5、None!
```



（2）、对话框底部的按钮



```c
1、ok!(默认值)
2、okcancel!
3、yesno!
4、yesnocancel!
5、retrycancel!
6、abortretryignore!
```



（3）、例子



```c
if messagebox('提示','是否执行此操作?',question!,yesno!) = 1 then
 messagebox('提示','是')
else
 messagebox('提示','否')
end if
```



## 9、显示当前窗口名称



可以写到open事件，打开窗口，窗口标题就显示当前窗口文件名



```c
IF handle(getapplication()) = 0 THEN
	THIS.Title = THIS.Title + '(' + this.classname() + ')'
END IF
```



## 10、快捷键



（1）、设置外部函数



```c
Subroutine keybd_event(int bVk,int bScan,ulong dwFlags,ulong dwExtraInfo) LIBRARY "user32.dll"
```



（2）、在key事件中写入以下代码



```c
If key = KeyEnter! Or Key = KeyRightArrow! Then 
//判断焦点对应的控件名称
CHOOSE CASE getfocus().classname() 
CASE 'sle_1 
messagebox('1','1')
CASE 'sle_2' 
messagebox('2','2')
CASE ELSE 
END CHOOSE 

//处理结束后按下tab键
keybd_event( 9,0,0,0 ) //   按下tab
keybd_event( 9,0,2,0 ) //   释放tab
End If
```



（3）、代码含义



[ 1 ]、按键说明



```c
keybd_event( 9,0,0,0 )  //   按下tab      
keybd_event( 9,0,2,0 )  //   释放tab   
keybd_event( 16,0,0,0 ) //   按下shift     
keybd_event( 16,0,2,0 ) //   释放shift
```



[ 2 ]、获取当前控件名称（可选）



```c
getfocus().classname()
```



（4）、键值对照表



[ 1 ]、字母和数字键

| 键   | 键码 |
| ---- | ---- |
| A    | 65   |
| B    | 66   |
| C    | 67   |
| D    | 68   |
| E    | 69   |
| F    | 70   |
| G    | 71   |
| H    | 72   |
| I    | 73   |
| J    | 74   |
| K    | 75   |
| L    | 76   |
| M    | 77   |
| N    | 78   |
| O    | 79   |
| P    | 80   |
| Q    | 81   |
| R    | 82   |
| S    | 83   |
| T    | 84   |
| U    | 85   |
| V    | 86   |
| W    | 87   |
| X    | 88   |
| Y    | 89   |
| Z    | 90   |
| 0    | 48   |
| 1    | 49   |
| 2    | 50   |
| 3    | 51   |
| 4    | 52   |
| 5    | 53   |
| 6    | 54   |
| 7    | 55   |
| 8    | 56   |
| 9    | 57   |



[ 2 ]、小键盘上的键

| 键    | 键码 |
| ----- | ---- |
| 0     | 96   |
| 1     | 97   |
| 2     | 98   |
| 3     | 99   |
| 4     | 100  |
| 5     | 101  |
| 6     | 102  |
| 7     | 103  |
| 8     | 104  |
| 9     | 105  |
| *     | 106  |
| +     | 107  |
| Enter | 108  |
| -     | 109  |
| .     | 110  |
| /     | 111  |



[ 3 ]、功能键

| 键   | 键码 |
| ---- | ---- |
| F1   | 112  |
| F2   | 113  |
| F3   | 114  |
| F4   | 115  |
| F5   | 116  |
| F6   | 117  |
| F7   | 118  |
| F8   | 119  |
| F9   | 120  |
| F10  | 121  |
| F11  | 122  |
| F12  | 123  |



[ 4 ]、其他键

| 键          | 键码 |
| ----------- | ---- |
| Backspace   | 8    |
| Tab         | 9    |
| Clear       | 12   |
| Enter       | 13   |
| Shift       | 16   |
| Control     | 17   |
| Alt         | 18   |
| Caps Lock   | 20   |
| Esc         | 27   |
| Spacebar    | 32   |
| Page Up     | 33   |
| Page Down   | 34   |
| End         | 35   |
| Home        | 36   |
| Left Arrow  | 37   |
| Up Arrow    | 38   |
| Right Arrow | 39   |
| Down Arrow  | 40   |
| Insert      | 45   |
| Delete      | 46   |
| Help        | 47   |
| Num Lock    | 144  |



## 11、获取各种时间



（1）、获取（日期 + 时间）



```c
datetime ldt_dqsj 
ldt_dqsj = datetime(today(),now())
```



（2）、获取（日期）



```c
string ls_dqrq
ls_dqrq =  string(today(),'yyyy-mm-dd')
```



（3）、获取SqlServer数据库的（日期 + 时间）



```c
datetime ldt_server_time
select getdate()  into :ldt_server_time from 表名;
```



（4）、在数据窗口中显示（日期 + 时间）



```c
string(today(),'yyyy-mm-dd hh:mm:ss')
```



（5）、字符串转（日期 + 时间）



```c
string(字符串,"yyyy-mm-dd hh:mm:ss")
```



（6）、获取0点到23:59:59秒的时间
[ 1 ]、方式1



```c
em_kssj.Text =  String(DateTime(today(),Time("00:00:00")))
em_jssj.Text =  String(DateTime(today(),Time("23:59:59")))
```



[ 2 ]、方式2



```c
em_kssj.Text = String(DateTime(ToDay(), 00:00:00))
em_jssj.Text =  String(DateTime(today(),23:59:59))
```



（7）、通过日期计算年龄（SQL语句）



```c
select (year(getdate())-year('出生日期')) from  表名
```



（8）、将string格式转为datetime格式



```c
string ls_rq
string ls_sj
ls_rq =  mid(ls_datetime,1,10)
ls_sj = mid(ls_datetime,12,21)
messagebox('提示',string(datetime(date(ls_rq),time(ls_sj))
```



（9）、将date和time转换为datetiem格式



```c
date lde_rq
time ltm_sj
lde_rq = 2022-04-15
ltm_sj = 10:10:10
messagebox('提示',string(datetime(lde_rq,ltm_sj)))
```



## 12、其他



（1）、给变量分配空间



```c
string ls_test
ls_test =  space(1024)
```



（2）、定位断点位置



```c
debugbreak()
```



（3）、获取当前项目路径



```c
getcurrentdirectory()
```



（4）、读、写ini文件



```c
profilestring(getcurrentdirectory() + "\pb.ini","pb","abc","我是备用的默认值")
setProfilestring(getcurrentdirectory() + "\pb.ini","pb","abc","我是要写入的参数")
```



（5）、创建与删除对象



```c
create //创建一个对象
destroy //删除一个对象
```



（6）、数据库链接与断开



```c
connect using sqlca; //连接
disconnect using sqlca; //断开
```



（7）、事务提交与回滚



```c
commit using sqlca;  //提交
rollback using sqlca; //回滚
```



（8）、设置控件焦点



```c
控件名.setfocus()
```