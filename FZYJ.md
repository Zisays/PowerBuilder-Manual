## 1、if



```c
if 1 = 1 then
 messagebox('提示','相等')
else
 messagebox('提示','不相等')
end if
```



## 2、choose



```c
choose case 变量
 case 值 1 
    messagebox('提示','我是 1')
 case 值 2 
    messagebox('提示','我是 2')
 case 值 3
    messagebox('提示','我是 3')
 case else
    messagebox('提示','如果都没有，那就来找我 ') 
end choose
```



## 3、try



```c
string ls_arr[1],ls_test
try
 ls_test = ls_arr[2]
catch(runtimeerror r)
 messagebox('运行时异常提示',r.className() + '~r~n' + r.getmessage())
catch(throwable t)
 messagebox('其他异常提示',t.className() + '~r~n' + t.getmessage())
finally
 messagebox('提示','不管什么情况下都会执行')
end try
```



# 