## 1、命名规范



### （1）、常量



```c
//使用 { 全大写字母 } 定义常量
Constant String NAME = 'PB手册'
```



### （2）、变量



[ 1 ]、全局变量



g + 变量类型简写字母 + 变量名称



```c
// boolean		gbl	_	{ 变量名 }
// string 		gs	_	{ 变量名 }
// int			gi	_	{ 变量名 }
// uInt			gui	_	{ 变量名 }
// long			gl	_	{ 变量名 }
// longlong		gll	_	{ 变量名 }
// date			gd	_	{ 变量名 }
// time			gt	_	{ 变量名 }
// datetime		gdt	_	{ 变量名 }
// decimal		gdc	_	{ 变量名 }
// decimal{2}	gdc2_	{ 变量名 }
// char			gc_		{ 变量名 }
// double		gdb_	{ 变量名 }
```



[ 2 ] 、共享变量



s + 变量类型简写字母 + 变量名称



```c
// boolean		sbl	_	{ 变量名 }
// string 		ss	_	{ 变量名 }
// int			si	_	{ 变量名 }
// uInt			sui	_	{ 变量名 }
// long			sl	_	{ 变量名 }
// longlong		sll	_	{ 变量名 }
// date			sd	_	{ 变量名 }
// time			st	_	{ 变量名 }
// datetime		sdt	_	{ 变量名 }
// decimal		sdc	_	{ 变量名 }
// decimal{2}	sdc2_	{ 变量名 }
// char			sc_		{ 变量名 }
// double		sdb_	{ 变量名 }
```



[ 3 ]、实例变量



i +  变量类型简写字母 + 变量名称



```c
// boolean		ibl	_	{ 变量名 }
// string 		is	_	{ 变量名 }
// int			ii	_	{ 变量名 }
// uInt			iui	_	{ 变量名 }
// long			il	_	{ 变量名 }
// longlong		ill	_	{ 变量名 }
// date			id	_	{ 变量名 }
// time			it	_	{ 变量名 }
// datetime		idt	_	{ 变量名 }
// decimal		idc	_	{ 变量名 }
// decimal{2}	idc2_	{ 变量名 }
// char			ic_		{ 变量名 }
// double		idb_	{ 变量名 }
```



### （2）、组件名规范

| 描述         | 组件全称       | 命名规则        |
| ------------ | -------------- | --------------- |
| 窗口         | Window         | w_              |
| 数据窗口     | DataWindow     | dw  * **d*dddw_ |
| 结构体       | Structure      | s * **st*       |
| 菜单         | Menu           | m_              |
| 全局函数     | Function       | gf              |
| 窗口函数     | WindowFunction | wf_             |
| 类函数       | ClassFunction  | of_             |
| 自定义类     | CustomClass    | ucc_            |
| 标准类       | StandardClass  | usc_            |
| 可视化类     | CustomVisual   | ucv_            |
| 外部可视化类 | ExternalVisual | uev_            |
| 标准可视化类 | StandardVisual | usv_            |



## 2、注释



### （1）、单行注释



```c
//我已经被注释了
```



### （2）、多行注释



```c
/*
我已经被注释了
我已经被注释了
我已经被注释了
*/
```



## 3、访问权限



### （1）、区域访问权限



```c
//1、（公共区域）以下变量区域在所有类都可以见
public:
int a = 1

//2、（私有区域）以下变量区域在当前类可见，子类不可见
Private:
int a = 2

//3、（受保护区域）以下变量区域在当前类和子类都可见
Protected:
int a = 3
```



### （2）、变量访问权限



```c
//1、公共的权限
public int a = 1

//2、私有的权限
//只有当前类可以读写
Private int a = 1
//只有当前类可以写入
PrivateWrite int a = 1
//只有当前类可以读取
PrivateRead int a = 1

//3、受保护的权限
//只有当前类和子类可以读写
Protected  int a = 1
//只有当前类和子类可以写入
ProtectedWrite int a = 1
//只有当前类和子类可以读取
ProtectedRead int a = 1
```



## 4、代码排版



### （1）、多行字符串排版



```c
string  ls_data
ls_data = "1"+&
"2" +  &
"3"
messagebox('提示',ls_data)
```



### （2）、多行字符串序列



```c
string  ls_data
ls_data = "&
1&
2&
3&
"
messagebox('提示',ls_data)
```



## 5、链式调用



1、先定义3个类 `uo_1` 、 `uo_2` 、 `uo_3`



2、在 `uo_1` 类中的 `实例变量区域` 定义



```c
uo_2  u2
```



3、在 `uo_2` 类中的 `实例变量区域` 定义



```c
uo_3 u3
```



4、在 `uo_3` 类中创建 `of_init` 函数，写入以下代码



```c
return '成功!
```



5、开始链式操作调用
在新建的 `w_main` 窗口下的 `open` 事件中，写入以下代码



```c
string ls_msg
uo_1 u1
u1 = create uo_1
ls_msg = u1.u2.u3.of_init()
messagebox('提示',ls_msg)
```