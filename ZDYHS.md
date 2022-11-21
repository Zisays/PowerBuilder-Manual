## 1、shell



（1）、定义外部动态库



```c
Function long ShellExecuteA (long hwnd, string lpOperation ,String lpFile, String lpParameters, String lpDirectory, Long nShowCmd) Library "shell32.dll"
Function long FindWindowA (String lpClassName , String lpWindowName ) Library "user32.dll"
Function boolean IsWindow (Long hwnd ) Library "user32.dll"
```



（2）、创建函数



```c
/*====================================================================
> Function: shell.
>--------------------------------------------------------------------
> 描述:运行一个外部程序（或者是打开一个已注册的文件、打开一个目录、打印一个文件等等），并对外部程序有一定的控制。
>--------------------------------------------------------------------
> 参数:
1、lpoperation（指定动作, 譬如: open、runas、print、edit、explore、find）
（1）、open		【运行第一个参数中指定的文件。如果该文件不是一个可执行文件，则用相应的可以打开该文件的软件打开它】
（2）、runas	【以管理员账户运行第一个参数指定的程序。用户账户管理系统（uac）会提示用户确认程序以更高的权限运行或要求用户输入管理员账户的凭证】
（3）、print	【打印第一个参数中指定的文件】
（4）、edit		【使用对应的编辑器打开第一个参数中输入的文件以对其编辑】
（5）、explore	【函数打开浏览由lpfile指定的目录窗口】
（6）、find		【在指定的目录下查找一个指定的文件】
（7）、如果该参数为null，则相当于使用"open"操作方式。
2、lpfile（一个非空字符串指定要打开或打印的文件，或者是要打开浏览的目录名。该函数可以打开一个可执行文件或一个文档文件，也可以打印一个文件。    ）
3、lpparameters（如果lpfile指定一个可执行文件，则lpparameters代表要传给这个应用程序的参数。如果lpfile指定一个文档文件，则其应该为空。）
4、lpdirectory（非空字符串指定缺省目录）
5、nshowcmd（如果lpfile指定一个可执行文件，nshowcmd指定应用程序运行时如何显示。如果lpfile指定的是文档文件，则nshowcmd应该为0。）
nshowcmd 可选参数如下：
（0）、sw_hide					【隐藏窗体，激活另一个窗口】
（1）、sw_shownormal			【用最近的大小和位置显示，激活】
（2）、sw_minimize			【最小化，激活】
（3）、sw_maximize			【最大化，激活】
（4）、sw_shownoactivate 	【用最近的大小和位置显示, 不激活】
（5）、sw_show					【最近的大小和位置显示, 不激活】
（6）、sw_minimize			【最小化, 不激活】
（7）、sw_showminnoactive	【最小化，不激活】
（8）、sw_showna				【用最近的大小和位置显示, 不激活】
（9）、sw_restore				【用最近的大小和位置显示，激活】
>--------------------------------------------------------------------
> 返回: 执行成功返回0，失败返回-1
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
long ll_handle
long li_loop
long ll_return
ll_handle = handle(this)
ll_return = shellexecuteA(0,lpoperation,lpfile,lpparameters,lpdirectory,nshowcmd)
if ll_return = 0 then
	messagebox('提示','内存不足!')
	return -1
elseif ll_return = 2 then
	messagebox('提示','文件名错误!')
	return -1
elseif ll_return = 3 then
	messagebox('提示','路径名错误!')
	return -1
elseif ll_return = 11 then
	messagebox('提示','EXE文件无效!')
	return -1
elseif ll_return = 26 then
	messagebox('提示','发生共享错误!')
	return -1
elseif ll_return = 27 then
	messagebox('提示','文件名不完全或无效!')
	return -1
elseif ll_return = 28 then
	messagebox('提示','超时!')
	return -1
elseif ll_return = 29 then
	messagebox('提示','DDE 事务失败!')
	return -1
elseif ll_return = 30 then
	messagebox('提示','正在处理其他 DDE 事务而不能完成该 DDE 事务!')
	return -1
elseif ll_return = 31 then
	messagebox("错误", "没有相关联的应用程序")
	return -1
else
	for li_loop = 1 to 10000
		ll_handle = findwindowa("tty",lpfile)
		yield()
		if ll_handle <> 0 then
			exit
		end if
	next
	do while iswindow(ll_handle)
		yield()
	loop
end if
return 0
```



（3）、调用函数



```c
shell("open", "calc.exe",'','',1); 											//打开计算器
shell("open", "notepad.exe",'','',1); 										//打开记事本
shell("open", "www.baidu.com",'','',1); 									//打开百度
shell("open","C:\Windows\System32\drivers\etc\hosts","","",1);				//打开hosts文件
shell("open","C:\Windows\","","",1);										//打开Windows文件夹
shell("print","C:\Windows\WindowsUpdate.log","","",0);						//打印WindowsUpdate.log文件
shell("runas","C:\Program Files (x86)\Tencent\WeChat\WeChat.exe","","",1); 	//管理员身份运行微信
```



（4）、使用shell写入命令行参数，读取命令行参数



```c
//在Application下的open事件中写入以下代码
if commandline = '' or  isnull(commandline) then
    //写入命令行参数
	shell("runas","zisay.exe","1234","",0);
else
    //接收命令行参数
	messagebox('接收到的命令行参数',commandline)				
end if
```



## 2、getage



（1）、创建函数



```c
/*====================================================================
> Function: getage
>--------------------------------------------------------------------
> 描述: 根据日期获取年龄
>--------------------------------------------------------------------
> 参数: 
> 	datetime as_datetime_start 	//开始日期
> 	datetime as_datetime_end	//结束日期
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long ll_seconds,ll_y,ll_m,ll_t,i
string ls_age
ll_seconds = (daysafter(date(as_datetime_start),date(as_datetime_end)) * 86400 + SecondsAfter ( time(as_datetime_start), time(as_datetime_end) ))
ll_y = integer(ll_seconds / (365 * 86400))
if ll_y > 0 then
	for i = 1 to ll_y
		ll_seconds = ll_seconds - (365 * 86400)
	next
end if
ll_m = integer(ll_seconds / (30 * 86400))
if ll_m > 0 then
	for i = 1 to ll_m
		ll_seconds = ll_seconds - (30 * 86400)
	next
end if
ll_t = integer(ll_seconds / 86400)
if ll_y > 0 then
	ls_age += string(ll_y) + '岁'
end if
if ll_m > 0 then
	ls_age += string(ll_m) + '月'
end if
if ll_t > 0 then
	ls_age += string(ll_t) + '天'
else
	ls_age = '0天'
end if
return ls_age
```



（2）、调用函数



```c
string ls_sj
ls_sj = getage(datetime(1980-05-26,00:00:00), datetime(2022-05-26,00:00:00))
messagebox('提示',ls_sj)
```



## 3、gethms



（1）、创建函数



```c
/*====================================================================
> Function: gethms
>--------------------------------------------------------------------
> 描述: 根据日期获取总共过了多少个时分秒
>--------------------------------------------------------------------
> 参数: 
> 	datetime as_datetime_start
> 	datetime as_datetime_end	
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
long ll_seconds,ll_h,ll_m,ll_s
string ls_hms
ll_seconds = (daysafter(date(as_datetime_start),date(as_datetime_end)) * 86400 + SecondsAfter ( time(as_datetime_start), time(as_datetime_end) ))
ll_h = ll_seconds / 3600
ll_m = (ll_seconds - ll_h * 3600) / 60
ll_s = ll_seconds - (ll_h * 3600 + ll_m * 60)
if ll_h > 0 then
	ls_hms += string(ll_h) + '小时'
end if
if ll_m > 0 then
	ls_hms += string(ll_m) + '分钟'
end if
if ll_s > 0 then
	ls_hms += string(ll_s) + '秒'
end if
return ls_hms
```



（2）、调用函数



```c
string ls_hms
ls_hms = gethms(datetime(2022-05-26,01:02:01),datetime(2022-05-27,23:02:02))
messagebox('提示',ls_hms)
```



## 4、fileread



（1）、创建函数



```c
/*====================================================================
> Function: fileread
>--------------------------------------------------------------------
> 描述: 文件读取
>--------------------------------------------------------------------
> 参数: 
> 	string as_fileway					//读取文件的方式
> 	string as_filepath				//要读取的文件路径和文件名称
> 	ref string as_filecontent[]	//返回的内容
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long  ll_file,ll_FLength,ll_i,ll_j,ll_count
string  ls_content
if as_fileway = 'a' then
	//流模式、读取、所有用户均可读写该文件
	ll_file = fileopen(as_filepath,streamMode!,Read!,Shared!)
	IF ll_file > 0 THEN
		ll_FLength = len(as_filepath)
		if ll_FLength > 32765  then
			if mod(ll_FLength,32765) = 0 then
				ll_count = ll_FLength / 32765
			else
				ll_count = ll_FLength / 32765 + 1
			end if
		else
			ll_count = 1
			end  if
			for ll_i = 1 to ll_count
				FileRead(ll_file,ls_content)
				as_filecontent[1] += ls_content
			next
		else
			messagebox('提示','fileread:文件打开失败!')
			return - 1
		end if
	elseif as_fileway = 'r' then
		//行模式、读取、所有用户均可读写该文件
		ll_file = fileopen(as_filepath,LineMode!,Read!,Shared!)
		IF ll_file > 0 THEN
			ll_j = 1
			ll_i = FileRead(ll_file,as_filecontent[ll_j])
			do until  string(ll_i) = '-100'
				ll_j = ll_j + 1
				ll_i = FileRead(ll_file,as_filecontent[ll_j])
			loop
			FileClose(ll_file)
		else
			messagebox('提示','fileread:文件打开失败!')
			return - 1
		end if
	else
		messagebox('提示','fileread:传入的参数错误')
		return - 1
	end if
	
	return 0
```



（2）、调用函数



```c
（1）、以流模式读取文件 
string ls_data[] 
fileread('r',getcurrentdirectory() + '\1.txt',ls_data[] ) 
messagebox('流模式返回值',ls_data[1])

（2）、以行模式读取文件 
string ls_data[] 
fileread('rl',getcurrentdirectory() + '\1.txt',ls_data[] ) 
messagebox('第1行数据',ls_data[1]) 
messagebox('第2行数据',ls_data[2]) 
messagebox('第3行数据',ls_data[3])
```



## 5、filewrite



（1）、创建函数



```c
/*====================================================================
> Function: filewrite
>--------------------------------------------------------------------
> 描述: 文件写入
>--------------------------------------------------------------------
> 参数: 
> 	string as_fileway			//打开文件的方式
> 	string as_filepath		//要写入的文件路径和文件名称
> 	string as_filecontent	//要写入的内容
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long  ll_file,ll_FLength,ll_i,ll_count
string ls_content
choose case as_fileway
	case 'w'
		//流模式、写入、所有用户均可读写该文件、覆盖
		ll_file = fileopen(as_filepath,streamMode!,Write!,Shared!,Replace!)
	case 'w+'
		//流模式、写入、所有用户均可读写该文件、追加
		ll_file = fileopen(as_filepath,streamMode!,Write!,Shared!,append!)
	case 'wl'
		//行模式、写入、所有用户均可读写该文件、覆盖
		ll_file = fileopen(as_filepath,LineMode!,Write!,Shared!,Replace!)
	case 'wl+'
		//行模式、写入、所有用户均可读写该文件、追加
		ll_file = fileopen(as_filepath,LineMode!,Write!,Shared!,append!)
	case else
		messagebox('提示','filewrite:传入的参数错误!')
		return - 1
end choose
IF ll_file > 0  THEN
	ll_FLength = len(as_filecontent)
	if ll_FLength > 32765 then
		if  mod(ll_FLength,32765) = 0 then
			ll_count = ll_FLength / 32765
		else
			ll_count = ll_FLength / 32765 + 1
		end if
	else
		ll_count = 1
	end if
	for ll_i = 1 to  ll_count
		ls_content = left(as_filecontent,32765)
		FileWrite(ll_file,ls_content)
		as_filecontent = right(as_filecontent,len(as_filecontent) - 32765)
	next
	FileClose(ll_file)
else
	messagebox('提示','filewrite:文件打开失败!')
	return - 1
end if
return 0
```



（2）、调用函数



```c
filewrite('w',getcurrentdirectory() + '\1.txt','流模式覆盖') 
filewrite('w+',getcurrentdirectory() + '\1.txt','流模式追加') 
filewrite('wr',getcurrentdirectory() + '\1.txt','行模式覆盖')
filewrite('wr+',getcurrentdirectory() + '\1.txt','行模式追加')
```



## 6、adodb_blob_read



（1）、创建函数



```c
/*====================================================================
> Function: adodb_blob_read
>--------------------------------------------------------------------
> 描述: 大文件读取（二进制数据流）
>--------------------------------------------------------------------
> 参数: 
> 	string as_filepath //文件路径	
>--------------------------------------------------------------------
> 返回:  blob
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long li_rtn
blob lb_data
if as_filepath = '' or isnull(as_filepath) then
	messagebox('提示','缺少文件路径!')
else
	OLEObject ADODB
	ADODB = CREATE OLEObject
	li_rtn = ADODB.ConnectToNewObject("ADODB.Stream")
	if li_rtn = 0  then
		ADODB.Type = 1 //设置ADODB类型（1、二进制数据，2、文本数据）
		ADODB.Mode = 3 //设置读写模式（1、读，2、写，3、读写）
		ADODB.Open() //打开ADODB
		ADODB.LoadFromFile(as_filepath) //加载文件
		lb_data = ADODB.Read() //Read 和 ReadText 方法向 Stream  中读取字节或文本。
		ADODB.flush() //清空缓冲区数据
		ADODB.Close() //关闭流
		destroy ADODB
	else
		messagebox('提示', '无法连接【ADODB.Stream】!~r~n读取文件失败!')
	end if
end if
return lb_data
```



（2）、调用函数



```c
string ls_data
ls_data = adodb_blob_read('D:\1.txt')
messagebox('提示',ls_data)
```



## 7、adodb_string_read



（1）、创建函数



```c
/*====================================================================
> Function: adodb_string_read
>--------------------------------------------------------------------
> 描述: 大文件读取（文本流）
>--------------------------------------------------------------------
> 参数: 
> 	string as_filepath //文件路径
> 	string as_charset	 //字符集（可选参数：GB2312，Unicode，UTF-8...）
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long li_rtn
string ls_data
if as_filepath = '' or isnull(as_filepath) then
	messagebox('提示','缺少文件路径!')
else
	OLEObject ADODB
	ADODB = CREATE OLEObject
	li_rtn = ADODB.ConnectToNewObject("ADODB.Stream")
	if li_rtn = 0  then
		ADODB.Type = 2 //设置ADODB类型（1、二进制数据，2、文本数据）
		ADODB.Mode = 3 //设置读写模式（1、读，2、写，3、读写）
		ADODB.Open() //打开ADODB
		//设置字符集
		if as_charset <> '' and not isnull(as_charset) then
			ADODB.Position = 0 //Position=0才能设置Charset
			ADODB.Charset = as_charset
		end if
		ADODB.LoadFromFile(as_filepath) //加载文件
		ls_data = ADODB.ReadText() //Read 和 ReadText 方法向  Stream 中读取字节或文本。
		ADODB.flush() //清空缓冲区数据
		ADODB.Close() //关闭流
		destroy ADODB
	else
		messagebox('提示', '无法连接【ADODB.Stream】!~r~n读取文件失败!')
	end if
end if
return ls_data
```



（2）、调用函数



```c
string ls_data
ls_data = adodb_string_read('D:\1.txt','UTF-8')
messagebox('提示',ls_data)
```



## 8、adodb_blob_write



（1）、创建函数



```c
/*====================================================================
> Function: adodb_blob_write
>--------------------------------------------------------------------
> 描述: 大文件写入（二进制数据流） 
>--------------------------------------------------------------------
> 参数: 
> 	string as_filepath	//文件路径
> 	blob as_filecontent	//要写入的内容
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long li_rtn,ll_file
string ls_data
OLEObject ADODB
ADODB = CREATE OLEObject
li_rtn = ADODB.ConnectToNewObject("ADODB.Stream")
if li_rtn = 0  then
	ADODB.Type = 1 //设置ADODB类型（1、二进制数据，2、文本数据）
	ADODB.Mode = 3 //设置读写模式（1、读，2、写，3、读写）
	ADODB.open() //打开ADODB
	ADODB.Position = 0 //Position=0才能设置Charset
	ADODB.Write(as_filecontent) //Write 和 WriteText 方法向 Stream 中输入字节或文本。
	ADODB.savetofile(as_filepath,2) //savetofile(1、只写入1次。2、可覆盖写入多次)
	ADODB.flush() //清空缓冲区数据
	ADODB.Close() //关闭流
	destroy ADODB
else
	messagebox('提示', '无法连接【ADODB.Stream】!~r~n读取文件失败!')
	return - 1
end if
return 0
```



（2）、调用函数



```c
adodb_blob_write('D:\1.txt',blob('我是要写入的内容'))
```



## 9、adodb_string_write



（1）、创建函数



```c
/*====================================================================
> Function: adodb_string_write
>--------------------------------------------------------------------
> 描述: 大文件写入（文本流）
>--------------------------------------------------------------------
> 参数: 
> 	string as_filepath		//文件路径
> 	string as_filecontent	//要写入的内容
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long li_rtn,ll_file
string ls_data
OLEObject ADODB
ADODB = CREATE OLEObject
li_rtn = ADODB.ConnectToNewObject("ADODB.Stream")
if li_rtn = 0  then
	ADODB.Type = 2 //设置ADODB类型（1、二进制数据，2、文本数据）
	ADODB.Mode = 3 //设置读写模式（1、读，2、写，3、读写）
	ADODB.open() //打开ADODB
	ADODB.Position = 0 //Position=0才能设置Charset
	ADODB.WriteText(as_filecontent) //Write 和 WriteText 方法向 Stream 中输入字节或文本。
	ADODB.savetofile(as_filepath,2) //savetofile(1、只写入1次。2、可覆盖写入多次)
	ADODB.flush() //清空缓冲区数据
	ADODB.Close() //关闭流
	destroy ADODB
else
	messagebox('提示', '无法连接【ADODB.Stream】!~r~n读取文件失败!')
	return - 1
end if
return 0
```



（2）、调用函数



```c
adodb_string_write('D:\1.txt','我是要写入的内容')
```



## 10、messagebox



（1）、创建函数



```c
/*====================================================================
> Function: messagebox
>--------------------------------------------------------------------
> 描述: 使用弹窗触发Application下的SystemError事件
>--------------------------------------------------------------------
> 参数: 
> 	integer as_number		//错误号
> 	string as_text			//错误消息
> 	string as_object		//错误对象
> 	string as_objectevent	//错误事件
> 	long as_line			//错误行
>--------------------------------------------------------------------
> 返回:  无
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
//以应用程序定制的错误号和错误信息填充Error对象，该函数不触发应用对象的SystemError事件。
PopulateError(as_number,as_text)
//自定义错误对象
error.object = as_object
//自定义错误事件
error.objectevent = as_objectevent
//自定义错误行
error.line = as_line
//以编程方式触发应用对象的SystemError事件。
SignalError()
```



（2）、在Application下的SystemError事件，写入以下代码



```c
string ls_errmsg
ls_errmsg = "错误时间:" + string(today(),'yyyy-mm-dd hh:mm:ss') + "~r~n"
ls_errmsg += "错误编号: " + string(error.number) + "~r~n"
ls_errmsg += "错误信息: " + string(error.text) + "~r~n"
ls_errmsg += "错误对象: " + string(error.object) + "~r~n"
ls_errmsg += "错误事件: " + string(error.objectevent) + "~r~n"
ls_errmsg += "错误行号: " + string(error.line) + "~r~n~r~n"
integer debug = 1
if debug = 0 then
	if error.number = 1 then
		messagebox('',string(error.text),none!)
	elseif error.number = 2 then
		messagebox('提示信息',string(error.text),information!)
	elseif error.number = 3 then
		messagebox('警告信息',string(error.text),exclamation!)
	elseif error.number = 4 then
		messagebox('疑问信息',string(error.text),question!)
	elseif error.number = 5 then
		messagebox('错误信息',string(error.text),stopsign!)
	else
		messagebox('系统错误',ls_errmsg,none!)
	end if
else
	messagebox('调试模式',ls_errmsg)
end if
```



（3）、调用函数



```c
messagebox(1,'我是自定义的内容','w_main','open',2)
```



## 11、gf_dw_ddlb



（1）、创建函数



```c
/*====================================================================
> Function: gf_dw_ddlb
>--------------------------------------------------------------------
> 描述: 动态添加数据窗口字段下的ddlb下拉框
>--------------------------------------------------------------------
> 参数: 
> 	datawindow as_dw  		要添加下拉框的数据窗口
> 	string as_dw_column 		要添加下拉框的列
> 	transaction as_affairs 	要查询的sql事务
> 	string as_table 			要查询的表
>  string as_table_where 	要查询的where条件
> 	string as_table_display 要在下拉框显示的列
> 	string as_table_data	 	要在下拉框中指定的数据
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
string dw_sql,dw_style
string dw_syntax,dw_syntax_error,dw_create_error
boolean lb_flag = false
string ls_data,ls_display
string ls_value
datastore dw_new
dw_new = create datastore
as_dw.modify(as_dw_column + ".ddlb.case='any'")
as_dw.modify(as_dw_column + ".ddlb.vscrollbar='yes'")
if as_table_where = '' or isnull(as_table_where) then
	dw_sql = "select distinct " + as_table_display + ',' + as_table_data + " from " + as_table
else
	dw_sql = "select distinct " + as_table_display + ',' + as_table_data + " from " + as_table + ' where ' + as_table_where
end if
dw_style = "style(type=grid)"
dw_syntax = sqlca.syntaxfromsql(dw_sql, dw_style, dw_syntax_error)
if len(dw_syntax_error) > 0 then
	messagebox("提示", "构造sql数据源错误: " + dw_syntax_error)
	return - 1
end if
dw_new.create(dw_syntax,dw_create_error)
if len(dw_create_error) > 0 then
	messagebox("提示", "创建数据窗口错误: " + dw_create_error)
	return - 1
end if
dw_new.settransobject(as_affairs)
dw_new.retrieve()
long i,ll_rowcount
ll_rowcount = dw_new.rowcount()
if ll_rowcount > 0 then
	for i = 1 to ll_rowcount
		ls_display = string(dw_new.getitemstring(i,as_table_display))
		ls_data = string(dw_new.getitemstring(i,as_table_data))
		if not lb_flag then
			ls_value = as_dw_column + ".values='"
			lb_flag = true
		else
			ls_value += "/"
		end if
		ls_value += trim(ls_display) + "~t" + trim(ls_data)
	next
	ls_value += "'"
	if as_dw.modify(ls_value) <> "" then
		return - 1
	end if
else
	return - 1
end if
return 0
```



（2）、调用函数



```c
gf_dw_ddlb(dw_1,'name',sqlca,'user','type=1','name','id')
```



## 12、gf_remove_letter



（1）、创建函数



```c
/*====================================================================
> Function: gf_remove_letter
>--------------------------------------------------------------------
> 描述: 移除字符串中的字母
>--------------------------------------------------------------------
> 参数: 
> 	string ls_data	
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
string str =  'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
string ls_data_new
long i
if ls_data = '' or isnull(ls_data) then
 ls_data_new = ''
else
 for i = 1 to len(ls_data)
 if pos(str,mid(ls_data,i,1)) = 0 then
  ls_data_new += mid(ls_data,i,1)
 end if
 next
end if
return ls_data_new
```



（2）、调用函数



```c
messagebox('提示',gf_remove_letter('12abc3sdfsg4'))
```



## 13、gf_capital_amount



（1）、创建函数



```c
/*====================================================================
> Function: gf_capital_amount
>--------------------------------------------------------------------
> 描述: 将金额转换为大写金额
>--------------------------------------------------------------------
> 参数:
> 	decimal as_money
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
string ls_numstr[10] = {"零","壹","贰","叁","肆","伍","陆","柒","捌","玖"}
string ls_monstr[20] = {"元","拾","佰","仟","万","拾","佰","仟","亿","拾","佰","仟","万","拾","佰","仟","亿","拾","佰","仟"}
integer i
integer li_len
string  ls_temp
string  ls_char
string  ls_intstr
string  ls_decstr
string  ls_rtnintstr
string  ls_rtndecstr
ls_temp = string(abs(as_money),"0.00")
ls_intstr = left (ls_temp,len(ls_temp) - 3)
ls_decstr = right(ls_temp,2)
li_len = len(ls_intstr)
for i = 1 to li_len
	ls_char = mid(ls_intstr,li_len - i + 1,1)
	if ls_char = "0" then
		choose case i
			case 1,9,17
				ls_rtnintstr = ls_monstr[i] + ls_rtnintstr
			case 5,13
				if li_len > i + 3 then
					if mid(ls_intstr,li_len - i - 2,3) <> "000" then
						ls_rtnintstr = ls_monstr[i] + ls_rtnintstr
					end if
				else
					ls_rtnintstr = ls_monstr[i] + ls_rtnintstr
				end if
			case else
				if mid(ls_intstr,li_len - i + 2,1) <> "0" then
					ls_rtnintstr = "零" + ls_rtnintstr
				end if
		end choose
	else
		ls_rtnintstr = ls_numstr[integer(ls_char) + 1] + ls_monstr[i] + ls_rtnintstr
	end if
next
if long(ls_intstr) = 0 then
	if long(ls_decstr) > 0 then
		ls_rtnintstr = ""
	else
		ls_rtnintstr = "零元"
	end if
end if
if ls_decstr = "00" then
	ls_rtndecstr = "整"
elseif mid(ls_decstr,1,1) = "0" then
	ls_rtndecstr = ls_numstr[integer(mid(ls_decstr,2,1)) + 1] + "分"
	if long(ls_intstr) > 0 then ls_rtndecstr = "零" + ls_rtndecstr
elseif mid(ls_decstr,2,1) = "0" then
	ls_rtndecstr = ls_numstr[integer(mid(ls_decstr,1,1)) + 1] + "角"
else
	ls_rtndecstr = ls_numstr[integer(mid(ls_decstr,1,1)) + 1] + "角" + &
		ls_numstr[integer(mid(ls_decstr,2,1)) + 1] + "分"
end if
if as_money >= 0 then
	return ls_rtnintstr + ls_rtndecstr
else
	return "负" + ls_rtnintstr + ls_rtndecstr
end if
```



（2）、调用函数



```c
string ls_dxje
ls_dxje = gf_capital_amount(11.22)
messagebox('提示',ls_dxje)
```



## 14、gf_cut_string



（1）、创建函数



```c
/*====================================================================
> Function: gf_cut_string
>--------------------------------------------------------------------
> 描述: 根据条件切割字符串，并返回切割后的字符串
>--------------------------------------------------------------------
> 参数: 
> 	string as_data
> 	string as_conditions
> 	ref string as_value	
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
long ll_empty_pos,i = 1
string  ls_value_string,ls_value_array[]
ll_empty_pos = pos(as_data,as_conditions)
if ll_empty_pos > 0 then
	do
		ls_value_string += trim(mid(as_data,1,ll_empty_pos - 1))
		as_data = trim(mid(as_data,ll_empty_pos + 1))
		ll_empty_pos = pos(as_data,as_conditions)
		if  ll_empty_pos = 0 then
			ls_value_string += trim(mid(as_data,0))
		end if
	loop while ll_empty_pos > 0
	as_value = ls_value_string
else
	messagebox('提示','未在字符串中找到符合切割条件的字符!')
	return - 1
end if
return 0
```



（2）、调用函数



```c
string ls_data,ls_value
ls_data  = '123,456,789'
gf_string_cut('string',ls_data,',',ls_value)
messagebox('提示',ls_value)  //123456789
```



## 15、gf_cut_array



（1）、创建函数



```c
/*====================================================================
> Function: gf_cut_array
>--------------------------------------------------------------------
> 描述: 根据条件切割字符串，并返回数组
>--------------------------------------------------------------------
> 参数: 
> 	string as_data
> 	string as_conditions
> 	ref string as_value[]	
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
long ll_empty_pos,i = 1
string  ls_value_string,ls_value_array[]
ll_empty_pos = pos(as_data,as_conditions)
if ll_empty_pos > 0 then
	do
		ls_value_array[i] = trim(mid(as_data,1,ll_empty_pos - 1))
		as_data = trim(mid(as_data,ll_empty_pos + 1))
		ll_empty_pos = pos(as_data,as_conditions)
		i ++
		if  ll_empty_pos = 0 then
			ls_value_array[i] = trim(mid(as_data,0))
		end if
	loop while ll_empty_pos > 0
	as_value[] = ls_value_array[]
else
	messagebox('提示','未在字符串中找到符合切割条件的字符!')
	return - 1
end if
return 0
```



（2）、调用函数



```c
string ls_data,ls_value[]
ls_data  = '123,456,789'
gf_string_cut('array',ls_data,',',ls_value[])
messagebox('',ls_value[1])  //123
messagebox('',ls_value[2])  //456
messagebox('',ls_value[3])  //789
```



## 16、gf_replace_string



（1）、创建函数



```c
/*====================================================================
> Function: gf_replace_string
>--------------------------------------------------------------------
> 描述: 将字符串中的某些字符替换成新的字符
>--------------------------------------------------------------------
> 参数: 
> 	string as_data
> 	string as_old
> 	string as_new	
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
long ll_oldlen, ll_newlen,  ll_pos
ll_pos = Pos(as_data,as_old)
IF  ll_pos > 0 Then
 ll_oldlen = Len(as_old)
 ll_newlen = Len(as_new)
 DO WHILE  ll_pos > 0
 as_data =  Replace(as_data,ll_pos,ll_oldlen,as_new)
 ll_pos =  Pos(as_data,as_old,ll_pos + ll_newlen)
 LOOP
END IF
RETURN as_data
```



（2）、调用函数



```c
string ls_data
ls_data =  gf_string_replace('1_31_3','_','2')
messagebox('提示',ls_data)  //123123
```



## 17、gf_datetime_string



（1）、创建函数



```c
/*====================================================================
> Function: gf_datetime_string
>--------------------------------------------------------------------
> 描述: 根据指定条件，返回datetime字符串中的内容
>--------------------------------------------------------------------
> 参数:
>     string as_datetime
>     string as_select
>     string as_conditions
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:    Zisay(QQ:15593838)
====================================================================*/
string ls_y,ls_m,ls_d,ls_h,ls_i,ls_s
long ll_y,ll_m,ll_d,ll_h,ll_i,ll_s
string ls_format,ls_return
as_datetime = trim(as_datetime)
ls_format = trim(as_conditions)
if pos(as_datetime,'-') > 0 then
	ll_y = pos(as_datetime,'-')
	ll_m = pos(as_datetime,'-',ll_y + 1)
	ll_d = pos(as_datetime,' ',ll_m + 1)
	ll_h = pos(as_datetime,':')
	ll_i = pos(as_datetime,':',ll_h + 1)
elseif pos(as_datetime,'/') > 0 then
	ll_y = pos(as_datetime,'/')
	ll_m = pos(as_datetime,'/',ll_y + 1)
	ll_d = pos(as_datetime,' ',ll_m + 1)
	ll_h = pos(as_datetime,':')
	ll_i = pos(as_datetime,':',ll_h + 1)
elseif pos(as_datetime,'.') > 0 then
	ll_y = pos(as_datetime,'.')
	ll_m = pos(as_datetime,'.',ll_y + 1)
	ll_d = pos(as_datetime,' ',ll_m + 1)
	ll_h = pos(as_datetime,':')
	ll_i = pos(as_datetime,':',ll_h + 1)
end if
ls_y = mid(as_datetime,1,ll_y - 1)
ls_m = mid(as_datetime,ll_y + 1,ll_m - 1 - ll_y)
if ll_d = 0 then
	ll_d = ll_m + 1
	ls_d = mid(as_datetime,ll_d)
else
	ls_d = mid(as_datetime,ll_m + 1,ll_d - 1 - ll_m)
end if
ls_h = mid(as_datetime,ll_d + 1,ll_h - 1 - ll_d)
ls_i = mid(as_datetime,ll_h + 1,ll_i - 1 - ll_h)
ls_s = mid(as_datetime,ll_i + 1)
Integer li_year,li_month
string ls_ymd,ls_month
li_year = Integer(ls_y)
li_month = Integer(ls_m)
choose case lower(as_select)
	case 'y' //年
		ls_return = ls_y
	case 'm' //月
		ls_return = ls_m
	case 'd' //日
		ls_return = ls_d
	case 'h' //时
		ls_return = ls_h
	case 'i' //分
		ls_return = ls_i
	case 's' //秒
		ls_return = ls_s
	case 'ym' //年月
		ls_return = ls_y + ls_format + ls_m
	case 'ymd' //年月日
		ls_return = ls_y + ls_format + ls_m + ls_format + ls_d
	case 'hi' //时分
		ls_return = ls_h + ls_format + ls_i
	case 'his' //时分秒
		ls_return = ls_h + ls_format + ls_i + ls_format + ls_s
	case 'ymdh' //年月日时
		ls_return = ls_y + ls_format + ls_m + ls_format + ls_d + ' ' + ls_h
	case 'ymdhi' //年月日时分
		ls_return = ls_y + ls_format + ls_m + ls_format + ls_d + ' ' + ls_h + ':' + ls_i
	case 'ymdhis' //年月日时分秒
		ls_return = ls_y + ls_format + ls_m + ls_format + ls_d + ' ' + ls_h + ':' + ls_i + ':' + ls_s
	case 'yhdh24is'
		ls_return = ls_y + ls_m  + ls_d + ls_h + '24' + ls_i +  ls_s
    case 'firstday' //获取当月第一天
		ls_return = ls_y + ls_format + ls_m + ls_format + '01'
	case 'lastday' //获取当月最后一天
		if li_month = 12 then
			li_month = 1
			li_year ++
		else
			li_month = li_month + 1
		end if
		ls_ymd = string(RelativeDate(Date(String(li_year) + ls_format + String(li_month) + ls_format + '01'), - 1))
		if pos(as_datetime,'-') > 0 then
			ll_y = pos(as_datetime,'-')
			ll_m = pos(as_datetime,'-',ll_y + 1)
			ll_d = pos(as_datetime,' ',ll_m + 1)
		elseif pos(as_datetime,'/') > 0 then
			ll_y = pos(as_datetime,'/')
			ll_m = pos(as_datetime,'/',ll_y + 1)
			ll_d = pos(as_datetime,' ',ll_m + 1)
		elseif pos(as_datetime,'.') > 0 then
			ll_y = pos(as_datetime,'.')
			ll_m = pos(as_datetime,'.',ll_y + 1)
			ll_d = pos(as_datetime,' ',ll_m + 1)
		end if
		ls_m = mid(ls_ymd,ll_y + 1,ll_m - 1 - ll_y)
		ls_d = mid(ls_ymd,ll_m + 1)
		ls_return = ls_y + ls_format + ls_m + ls_format + ls_d
	case 'sfirstday' //获取上个月第1天
		if li_month = 1 then
			li_month = 12
			li_year --
		else
			li_month = li_month - 1
		end if
		if li_month < 10 then
			ls_month = '0' + string(li_month)
		else
			ls_month = string(li_month)
		end if
		ls_return = string(li_year) + ls_format + ls_month + ls_format + '01'
	case 'slastday' //获取上个月最后1天
		ls_ymd = string(RelativeDate(Date(String(li_year) + ls_format + String(li_month) + ls_format + '01'), - 1))
		if pos(as_datetime,'-') > 0 then
			ll_y = pos(as_datetime,'-')
			ll_m = pos(as_datetime,'-',ll_y + 1)
			ll_d = pos(as_datetime,' ',ll_m + 1)
		elseif pos(as_datetime,'/') > 0 then
			ll_y = pos(as_datetime,'/')
			ll_m = pos(as_datetime,'/',ll_y + 1)
			ll_d = pos(as_datetime,' ',ll_m + 1)
		elseif pos(as_datetime,'.') > 0 then
			ll_y = pos(as_datetime,'.')
			ll_m = pos(as_datetime,'.',ll_y + 1)
			ll_d = pos(as_datetime,' ',ll_m + 1)
		end if
		ls_m = mid(ls_ymd,ll_y + 1,ll_m - 1 - ll_y)
		ls_d = mid(ls_ymd,ll_m + 1)
		ls_return = ls_y + ls_format + ls_m + ls_format + ls_d
end choose
return ls_return
```



（2）、调用函数



```c
string ls_datetime
ls_datetime = '2022-06-01 12:12:12'
gf_datetime_string(ls_datetime,'y','') //获取年
gf_datetime_string(ls_datetime,'m','') //获取月
gf_datetime_string(ls_datetime,'d','') //获取日
gf_datetime_string(ls_datetime,'h','') //获取时
gf_datetime_string(ls_datetime,'i','') //获取分
gf_datetime_string(ls_datetime,'s','') //获取秒
gf_datetime_string(ls_datetime,'ym','-') //获取年+月
gf_datetime_string(ls_datetime,'ymd','/') //获取年+月+日
gf_datetime_string(ls_datetime,'hi',':') //获取时+分
gf_datetime_string(ls_datetime,'his',':') //获取时+分+秒
gf_datetime_string(ls_datetime,'ymdh','-') //获取年+月+日 时
gf_datetime_string(ls_datetime,'ymdhi','/') //获取年+月+日 时+分
gf_datetime_string(ls_datetime,'ymdhis','.') //获取年+月+日 时+分+秒
gf_datetime_string(ls_datetime,'ymdh24is','') //获取年月日时24分秒
gf_datetime_string(ls_datetime,'firstday','-') //获取当月第1天
gf_datetime_string(ls_datetime,'lastday','-') //获取当月最后1天
gf_datetime_string(ls_datetime,'sfirstday','-') //获取上个月第1天
gf_datetime_string(ls_datetime,'slastday','-') //获取上个月最后1天
```



## 18、filewrite_blob



（1）、创建函数



```c
/*====================================================================
> Function: filewrite_blob
>--------------------------------------------------------------------
> 描述: 文件写入
>--------------------------------------------------------------------
> 参数:
> 	string as_fileway			//打开文件的方式
> 	string as_filepath		//要写入的文件路径和文件名称
> 	blob as_filecontent	//要写入的内容
>--------------------------------------------------------------------
> 返回:  integer
>--------------------------------------------------------------------
> 作者:	Zisay（QQ：15593838）
====================================================================*/
long  ll_file,ll_FLength,ll_i,ll_count,ll_Pos
string ls_content
blob lblb_Data
choose case as_fileway
	case 'w'
		//流模式、写入、所有用户均可读写该文件、覆盖
		ll_file = fileopen(as_filepath,streamMode!,Write!,Shared!,Replace!)
	case 'w+'
		//流模式、写入、所有用户均可读写该文件、追加
		ll_file = fileopen(as_filepath,streamMode!,Write!,Shared!,append!)
	case 'wl'
		//行模式、写入、所有用户均可读写该文件、覆盖
		ll_file = fileopen(as_filepath,LineMode!,Write!,Shared!,Replace!)
	case 'wl+'
		//行模式、写入、所有用户均可读写该文件、追加
		ll_file = fileopen(as_filepath,LineMode!,Write!,Shared!,append!)
	case else
		messagebox('提示','filewrite:传入的参数错误!')
		return - 1
end choose
IF ll_file > 0  THEN
	ll_FLength = len(as_filecontent)
	if ll_FLength > 32765 then
		if  mod(ll_FLength,32765) = 0 then
			ll_count = ll_FLength / 32765
		else
			ll_count = ll_FLength / 32765 + 1
		end if
	else
		ll_count = 1
	end if
	ll_Pos = 1
	For ll_i = 1 To ll_count
		lblb_Data = BlobMid(as_filecontent, ll_Pos, 32765)
		ll_Pos += 32765
		If FileWrite(ll_file, lblb_Data) = -1 Then
			Return - 1
		End if
	Next
	FileClose(ll_file)
else
	messagebox('提示','filewrite_blob:文件打开失败!')
	return - 1
end if
return 0
```



（2）、调用函数



```c
filewrite_blob('w','1.txt',blob('123'))
```



## 19、midstring



（1）、创建函数



```c
/*====================================================================
> Function: midstring
>--------------------------------------------------------------------
> 描述: 反向截取字符串 
>--------------------------------------------------------------------
> 参数: 
> 	string as_data
> 	integer as_start
>--------------------------------------------------------------------
> 返回:  string
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
return Reverse(mid(Reverse(as_data),as_start + 1))
```



（2）、调用函数



```c
string ls_test
ls_test = '123,456,789,'
//去掉最后一个逗号
messagebox('提示',midstring(ls_test,1)) //输出结果为：123，456，789
```

## 20、dcidw



1、创建函数



```c
/*====================================================================
> Function: dcidw
>--------------------------------------------------------------------
> 描述: 动态创建不可视数据窗口（注：仅用于快速检索数据使用）
>--------------------------------------------------------------------
> 参数: 
> 	transaction as_transaction
> 	string as_sql	
>--------------------------------------------------------------------
> 返回:  datastore
>--------------------------------------------------------------------
> 作者:	Zisay(QQ:15593838)
====================================================================*/
string dw_style
string dw_syntax,dw_syntax_error,dw_create_error
datastore dw_dcidw
dw_dcidw = create datastore
dw_style = "style(type=grid)"
dw_syntax = as_transaction.syntaxfromsql(as_sql, dw_style, dw_syntax_error)
if len(dw_syntax_error) > 0 then
	messagebox("提示", "构造sql数据源错误: " + dw_syntax_error)
else
	dw_dcidw.create(dw_syntax,dw_create_error)
	if len(dw_create_error) > 0 then
		messagebox("提示", "创建数据窗口错误: " + dw_create_error)
	else
		dw_dcidw.settransobject(as_transaction)
		dw_dcidw.retrieve()
	end if
end if
return dw_dcidw
```



2、调用函数



```sql
datastore ds_1
ds_1 = dcidw(sqlca,'select * from 表名 where 条件 ...')
messagebox('提示',ds_1.rowcount())
```