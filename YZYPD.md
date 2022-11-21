## 1、判断字符串是否存在



```c
string ls_test
if ls_test = '' or isnull(ls_test) then
	messagebox('提示','不存在');
else
    messagebox('提示','存在');
end if
```



## 2、判断变量是否为null



```c
string ls_test
if isnull(ls_test) then
    messagebox('提示','为null')
elseif not isnull(ls_test) then
    messagebox('提示','不为null')
end if

//将变量设置为null
setnull(ls_test)
```