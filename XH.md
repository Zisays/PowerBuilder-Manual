## 1、for



```c
//语法1
for i = 1 to 99
 i++
next

//语法2
for i = 1 to 99 step 2
 i++
next
```



## 2、do  until



```c
当条件为false时，执行循环体。当条件为true时，跳出循环体

//语法1
do until i>99
loop
    
//语法2
do
loop until i>99
```



## 3、do  while



```c
当条件为true时，执行循环体。当条件为false时，跳出循环体

//语法1
do while i > 99
loop
    
//语法2
do
loop while i > 99
```



## 4、continue



continue只能用于do...loop和for...next语句中，遇到continue语句时，将不执行continue后面的语句，跳回到循环条件处继续执行



## 5、exit



exit 语句只能用于do...loop和for...next语句中，遇到exit语句时，将结束循环



## 6、goto



goto语句可直接跳出循环或任意位置



```c
fo i=1 to 10
    if  i = 3 then
        goto a
    end if
end if

a;
```