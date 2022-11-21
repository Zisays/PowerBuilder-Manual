# 一、数组



**1、lowerbound**



功能：



```plain
得到指定数组第n维的下界
```



语法：



```plain
lowerbound ( array {, n } )
```



参数：



```plain
array：数组名 

n ：数值类型，可选项，指定要得到数组哪一维的下界，默认值为1
```



返回值：



```plain
返回值：long 

成功返回：array数组第n维的下界 

失败返回：-1 

失败返回null：null
```



**2、upperbound**



功能：



```plain
得到指定数组第n维的上界
```



语法：



```plain
upperbound(  array {, n } )
```



参数：



```plain
array：数组名 

n ：数值类型，可选项，指定要得到数组哪一维的上界，默认值为1
```



返回值：



```plain
返回值：long 

成功返回：array数组第n维的上界 

失败返回：-1 

失败返回null：null
```



# 二、BLOB



**1、Blob**



功能：



```plain
将字符串转换成Blob类型数据
```



语法：



```plain
Blob ( text )
```



参数：



```plain
text：  string类型，指定要转换的数据
```



返回值：



```plain
返回值：Blob

成功返回：转换后的Blob类型数据 

失败返回NULL：NULL
```



**2、BlobEdit**



功能：



```plain
将任意类型的数据插入到Blob类型变量的指定位置
```



语法：



```c
BlobEdit ( blobvariable, n, data )
```



参数：



```plain
blobvariable：Blob类型的已初始化变量将向该变量中插入数据 

n：指定插入位置，有效值在1到4,294,967,295之间 

data：要插入到Blob类型变量中的数据，其数据类型可以是任何有效的PowerBuilder数据类型
```



返回值：



```plain
返回值：Unsigned long 

函数执行成功时返回下次可以插入数据的位置 

如果blobvariable变量中空间不够或任何参数的值为NULL，则BlobEdit()函数返回NULL
```



**3、BlobMid**



功能：



```plain
从Blob变量中提取出一段数据。提取之后，原Blob变量内容不变
```



语法：



```c
BlobMid ( data, n {, length } )
```



参数：



```plain
data：Blob类型的数据 

n ：指定要提取数据的起始位置，有效值在1到4,294,967,295之间 

length ：可选项，指定要提取数据的长度，以字节为单位，有效值在1到4,294,967,295之间。

缺省时提取从指定位置n到末尾的所有数据
```



返回值：



```plain
返回值：Blob

函数执行成功时返回指定字节数的数据 如果n的值大于data的字节数，函数返回空 

如果n与length的和超过了data数据的字节数，那么BlobMid()函数返回剩下的数据，数据长度将小于参数length的值 

如果任何参数的值为NULL，则BlobMid()函数返回NULL
```



**4、Len**



功能：



```plain
得到Blob类型变量的数据长度，以字节为单位
```



语法：



```plain
Len ( blob )
```



参数：



```plain
blob：Blob类型变量
```



返回值：



```plain
返回值：Long 

函数执行成功时返回blob变量的长度，发生错误时返回-1 

如果任何参数的值为NULL，则Len()函数返回NULL
```



用法：



```plain
如果在说明Blob类型的变量时指定了变量长度，那么对该变量来说，Len()函数得到的就是这个指定的长度 

如果在变量说明时未指定变量长度，那么PowerBuilder在赋值时调整长度，未赋值Blob类型变量的长度为0
```



**5、String**



功能：



```plain
将Blob类型变量的值转换成字符串类型。
如果Blob类型变量的值不是文本型数据，String()函数将其值解释成字符
```



语法：



```plain
String ( blob )
```



参数：



```plain
blob：要对其值进行类型转换的Blob类型变量
```



返回值：



```plain
返回值：String 

函数执行成功时返回转换后的数据，失败时返回空字符串（""） 

如果blob变量中包含的数据不是字符串类型的数据，那么String()函数尽可能把数据解释为字符，并返回字符串类型数据 

如果blob参数的值为NULL，则String()函数返回NULL
```



# 三、数据类型检查与转换



**1、Asc**



功能：



```plain
得到字符串第一个字符的ASCII码整数值
```



语法：



```plain
Asc ( string )
```



参数：



```plain
string：要得到第一个字符ASCII值的字符串
```



返回值：



```plain
返回值：integer 

函数执行成功时返回string参数第一个字符的ascii值

如果string参数的值为null，则asc()函数返回null
```



**2、Char**



功能：



```plain
将字符串的第一个字符、Blob变量的第一个值、或一个整数转换成字符
```



语法：



```plain
Char ( n )
```



参数：



```plain
n：字符串、Blob变量或整数，也可以是包含上述类型数据的Any类型变量
```



返回值：



```plain
返回值：Char 

返回参数n的第一个字符 

如果n参数的值为NULL，则Char()函数返回NULL
```



**3、Dec**



功能：



```plain
将字符串或Blob值转换成Decimal类型的值
```



语法：



```plain
Dec ( stringorblob )
```



参数：



```plain
stringorblob：string类型变量或Blob类型变量 Blob 类型变量时，把该变量第一个值转换为Decimal类型的值，其余部分被忽略 stringorblob  参数也可以是包含上述类型数据的Any类型变量
```



返回值：



```plain
返回值：Decimal 

函数执行成功时返回相应的Decimal类型值 

如果stringorblob参数中的值不是有效的PowerScript数字或数据类型不兼容，那么Dec()函数返回0 

如果stringorblob参数的值为NULL，则Dec()函数返回NULL
```



**4、Double**



功能：



```plain
将字符串或Blob值转换成Double类型的值
```



语法：



```plain
Double(stringorblob)
```



参数：



```plain
stringorblob：string类型变量或Blob类型变量 Blob 类型变量时，把该变量第一个值转换为Double类型的值，其余部分被忽略 stringorblob  参数也可以是包含上述类型数据的Any类型变量
```



返回值：



```plain
返回值：Double 

函数执行成功时返回相应的Double类型值 

如果stringorblob参数中的值不是有效的PowerScript数字或数据类型不兼容，那么Double()函数返回0 

如果stringorblob参数的值为NULL，则Double()函数返回NULL
```



**5、Integer**



功能：



```plain
将字符串或Blob值转换成Integer类型的值
```



语法：



```plain
Integer ( stringorblob )
```



参数：



```plain
stringorblob：string类型变量或Blob类型变量 Blob类型变量时，把该变量第一个值转换为Integer类型的值，其余部分被忽略 stringorblob参数也可以是包含上述类型数据的Any类型变量
```



返回值：



```plain
返回值：Integer 

函数执行成功时返回相应的Integer类型值 

如果stringorblob参数中的值不是有效的PowerScript数字或数据类型不兼容，那么Integer()函数返回0 

如果stringorblob参数的值为NULL，则Integer()函数返回NULL
```



**6、Long**



功能：



```plain
将其它类型的数据转换为Long类型的值
```



语法：



```plain
语法一、将两个无符号整数组合成一个长整数值 Long ( lowword, highword )  

语法二、将字符串或Blob值转换成Long类型的值 Long ( stringorblob )
```



参数：



```plain
语法一 
lowword  ：UnsignedInteger类型，指定长整数中的低位值 
highword ：UnsignedInteger类型，指定长整数中的高位值 

语法二 
stringorblob ：string类型变量或Blob类型变量 Blob  类型变量时，把该变量第一个值转换为Long类型的值，其余部分被忽略 stringorblob 参数也可以是包含上述类型数据的Any类型变量
```



返回值



```plain
语法一 
返回值Long 
函数执行成功时返回由低位值和高位值组合后的长整数值
发生错误时返回-1 
如果任何参数的值为NULL，则Long()函数返回NULL 

语法二 
返回值Long 
函数执行成功时返回相应的Long类型值 
如果stringorblob参数中的值不是有效的PowerScript数字或数据类型不兼容，那么Long()函数返回0 如果stringorblob参数的值为NULL，则Long()函数返回NULL
```



**7、Real**



功能：



```plain
将字符串或Blob值转换成Real类型的值
```



语法：



```plain
Real ( stringorblob )
```



参数：



```plain
stringorblob：string类型变量或Blob类型变量，当该参数是Blob类型变量时，把该变量第一个值转换为Real类型的值，其余部分被忽略
stringorblob 参数也可以是包含上述类型数据的Any类型变量
```



返回值：



```plain
返回值Real
函数执行成功时返回相应的Real类型值
如果stringorblob参数中的值不是有效的PowerScript数字或数据类型不兼容，那么Real()函数返回0
如果stringorblob参数的值为NULL,则Real()函数返回NULL
```



**8、Date**



功能：



```plain
将其它类型的数据转换为Date类型的数据
```



语法：



```plain
语法一、将DateTime类型或第一个值是DateTime或Date的Blob值转换成Date类型的值；
Date ( datetime )

语法二、将其值是个有效日期的字符串转换成Date类型的值；
Date ( string )

语法三、将三个整数组合成一个日期。
Date ( year, month, day )
```



参数：



```plain
语法一
datetime：DateTime类型的值或第一个值是DateTime或Date的Blob类型的值
当该参数是Blob类型变量时，把该变量第一个值转换为Date类型的值，其余部分被忽略
datetime参数也可以是包含上述类型数据的Any类型变量

语法二
string：string类型，其值包括一个有效的以字符串形式表示的日期（比如January 1, 1998或12-31-99）
string参数也可以是包含字符串类型数据的Any类型变量

语法三
year：integer类型，指定日期中的年份，用四位数字表示，从0到9999
month：integer类型，指定日期中的月份，用一位或两位数字表示，从1到12
day：integer类型，指定日期中的号数，用一位或两位数字表示，从1到31
```



返回值：



```plain
语法一
返回值：Date
函数执行成功时返回相应的Date类型值
如果datetime参数中的值不是有效的PowerScript日期或数据类型不兼容，那么Date()函数返回1900-01-01
如果datetime参数的值为NULL，则Date()函数返回NULL

语法二
返回值：Date
函数执行成功时返回相应的Date类型值。
如果string参数中的值不是有效的PowerScript日期或数据类型不兼容，那么Date()函数返回1900-01-01
如果string参数的值为NULL，则Date()函数返回NULL

语法三
返回值：Date
函数执行成功时返回由year、month、day三个参数确定的日期
如果这三个参数中任何一个参数使用了无效值（比如月份指定为14），则Date()函数返回1900-01-01
如果任何参数的值为NULL，则Date()函数返回NULL
```



**9、DateTime**



功能：



```plain
将其它类型的数据转换为DateTime类型的数据。
```



语法：



```plain
语法一、把日期和时间值组合成DateTime类型的值
DateTime ( date {, time } )

语法二、将Blob类型的值转换成DateTime类型的值
DateTime ( blob )
```



参数：



```plain
语法一
date：Date类型的日期值
time：可选参数，Time类型的时间值
省略该参数时，PowerBuilder把时间设置为午夜（00:00:00.000000）
当指定该参数时，可以仅仅指定小时值

语法二
blob：Blob类型变量，把该变量第一个值转换为DateTime类型的值，其余部分被忽略
blob参数也可以是包含blob类型数据的Any类型变量
```



返回值：



```plain
语法一 
返回值：DateTime 
函数执行成功时返回日期和时间组合而成的DateTime类型的值 
如果任何参数的值为NULL，则DateTime()函数返回NULL 

语法二 
返回值：DateTime 
函数执行成功时返回相应的DateTime类型值 
如果blob参数的值为NULL,则DateTime()函数返回NULL
```



**10、IsDate**



功能：



```plain
检测指定的字符串是否包含有效的日期
```



语法：



```plain
IsDate ( datevalue )
```



参数：



```plain
datevalue：string类型，指定要检测的字符串
```



返回值：



```plain
返回值：Boolean 
如果datevalue包含了有效的日期，则IsDate()函数返回TRUE，否则返回FALSE
如果datevalue参数的值为NULL，则IsDate()函数返回NULL
```



**11、IsNull**



功能：



```plain
测试变量或表达式的值是否是NULL
```



语法：



```plain
IsNull ( any )
```



参数：



```plain
any：要测试的变量或表达式
```



返回值：



```plain
返回值：Boolean
如果any的值为NULL，函数返回TRUE，否则函数返回FALSE
```



**12、IsNumber**



功能：



```plain
测试字符串是否是有效的数值
```



语法：



```plain
IsNumber ( string )
```



参数：



```plain
string：string类型，要测试的字符串
```



返回值：



```plain
返回值：Boolean
如果string的值为有效的PowerScript数字，函数返回TRUE，否则函数返回FALSE
如果string参数的值为NULL，则IsNumber()函数返回NULL
```



**13、IsTime**



功能：



```plain
测试字符串的值是否是有效的时间
```



语法：



```plain
IsTime ( timevalue )
```



参数：



```plain
timevalue：string类型，要测试的字符串
```



返回值：



```plain
返回值：Boolean
如果timevalue的值为有效的时间，函数返回TRUE，否则函数返回FALSE
如果timevalue 参数的值为NULL，则IsTime()函数返回NULL
```



**14、String**



功能：



```plain
按指定格式将数据转换成字符串
```



语法：



```plain
String()可以把Date、DateTime、数值类型、Time、String类型的数据转换成指定格式的字符串
String(data,{format})
```



参数：



```plain
data：指定要转换格式的数据，其数据类型可以是Date、DateTime、数值类型、Time、String
也可以是包含上述类型数据的Any类型变量

format：可选项，string类型，其值指定数据格式
如果data参数的类型为string，则必须指定format参数
```



返回值：



```plain
返回值：String

函数执行成功时返回以字符串方式表示的指定数据
如果data参数的数据类型与format参数指定的格式不匹配、format参数指定的格式无效
或data参数不是前面提到的适宜数据类型时，String()函数返回空字符串（""）
```



用法：



```plain
format 是个用掩码表示的字符串，对data参数为数值类型的情况来说，格式为：正数格式；负数格式；零的显示格式

空的显示格式除第一部分必须提供外，其它部分可以省略

数值型显示格式中使用两个掩码字符：#和0，其中，使用#代表0~9之间的任意数字，0代表每个零都要显示
另外，货币符号（$或￥）、百分号（%）、小数点（.）、逗号（，）等字符也可以出现在格式字符串中，但是，除小数点（.）、逗号（，）能够出现在格式字符#和0之间外，其它字符只能放置在格式串的前面或后面

例如，###,###$###是个错误的格式串，￥###,###,###是个正确的格式串

省略format参数时，String()函数使用PowerBuilder缺省格式

注意，如果显示格式有多个部分，各部分之间的分号（；）不能省略

其它字符也可以出现在显示格式字符串中（只能放在格式串的开头和末尾），但它们没有特殊意义，系统只是照原样显示

例如，用显示格式字符串“收入##”格式化数值12时，显示结果为“收入12”

对data参数为字符串（String）类型的情况来说，format参数的语法格式为：正常字符串格式

空值时格式在“正常字符串格式”中，@代表字符串中的任意字符，除此之外的任何字符照原样显示

例如，如果定义了下面的格式：（@@）@@@@-@@@@则字符串0166767593显示为：（01）6676-7593对data参数为日期（Date）类型的情况来说，format参数的语法格式为：正常日期格式

日期为空值时的格式日期格式中格式字符意义如下：

d开头不带0的日数（如8）

dd开头带0的日数（如08）

ddd星期的英文缩写（如Mon、Tue）

dddd星期的英文全称（如Monday、Tuesday）

m开头不带0的月份（如8）

mm开头带0的月份（如08）

mmm月份的英文缩写（如Jan、Feb）

mmmm月份的英文全称（如January、February）

yy两位数字表示的年份（如97）

yyyy四位数字表示的年份（如1997）

另外，还可以使用下面的关键字作为日期的显示格式：

[General] Windows系统中定义的短日期格式

[LongDate] Windows系统中定义的长日期格式

[ShortDate] Windows系统中定义的短日期格式

对data参数为时间（Time）类型的情况来说，语法格式为：正常时间格式；

时间为空值时的格式时间格式中格式字符意义如下：

h开头不带0的小时（比如6）

hh开头带0的小时（比如06）

m开头不带0的分钟（比如6）

mm开头带0的分钟（比如06）

s开头不带0的秒（比如6）

ss开头带0的秒（比如06）

f开头不带0的微秒，可以指定1~6个f，每个f代表一部分微秒

AM/PM用AM/PM显示上、下午时间

12小时制am/pm用am/pm显示上、下午时间

12小时制A/P用A/P显示上、下午时间

12小时制a/p用a/p显示上、下午时间

12小时制另外，显示格式中还可以使用关键字[Time]，它表示按当前Windows系统定义的格式显示时间

对data参数为日期时间（DateTime）类型的情况来说，语法格式为：

正常日期时间格式；日期时间为空值时的格式日期时间类型使用的掩码就是把日期掩码和时间掩码结合起来即可
```



**15、Time**



功能：



```plain
把其它类型的数据转换为Time类型的值
```



语法：



```plain
语法一、将DateTime类型或第一个值是DateTime或Time的Blob值转换成Time类型的值
语法Time ( datetime )

语法二、将其值是个有效时间的字符串转换成Time类型的值
语法Time ( string )

语法三、将表示时、分、秒、以及微秒的整数组合成一个时间值
语法Time ( hour, minute, second {, microsecond } )
```



参数：



```plain
语法一
datetime：DateTime类型的值或第一个值是DateTime或Time的Blob类型的值。
当该参数是Blob类型变量时，把该变量第一个值转换为Time类型的值，其余部分被忽略。
datetime参数也可以是包含上述类型数据的Any类型变量

语法二
string：string类型，其值包括一个有效的以字符串形式表示的时间（比如9am或10:25）
string参数也可以是包含时间类型数据的Any类型变量

语法三
参数hour：integer类型，指定时间中的小时，从0到23 
minute：integer类型，指定时间中的分钟，从0到59
second：integer类型，指定时间中的秒，从0到59
microsecond：integer类型，可选项，指定时间中的微秒，从0到32767
```



返回值：



```plain
语法一
返回值：Time。
函数执行成功时返回相应的Time类型值。
如果datetime参数中的值不是有效的PowerScript时间或数据类型不兼容，那么Time()函数返回00:00:00.000000。
如果datetime参数的值为NULL，则Time()函数返回NULL。

语法二
返回值：Time。
函数执行成功时返回相应的Time类型值。
如果string参数中的值不是有效的PowerScript时间或数据类型不兼容，那么Time()函数返回00:00:00.000000。
如果string参数的值为NULL，则Time()函数返回NULL。

语法三
返回值：Time。
函数执行成功时返回由hour、minute、second、microsecond 四个参数确定的时间。
如果这四个参数中任何一个参数使用了无效值（比如小时指定为44），则Time()函数返回NULL。
```



# 四、数值计算



**1、Abs**



功能：



```plain
计算绝对值。
```



语法：



```plain
Abs ( n )
```



参数：



```plain
n：要得到绝对值的数值型变量或表达式返回值返回值的数据类型与n的数据类型相同
```



返回值：



```plain
函数执行成功时返回n的绝对值。 
如果参数n的值为NULL，Abs()函数返回NULL。
```



**2、Ceiling**



功能：



```plain
返回大于n的最小整数。
```



语法：



```plain
Ceiling ( n )
```



参数：



```plain
n：数值型变量或表达式返回值返回值的数据类型与n的数据类型相同。
```



返回值：



```plain
函数执行成功时返回大于n的最小整数。 
如果参数n的值为NULL，Ceiling()函数返回NULL
```



**3、Cos**



功能：



```plain
计算余弦，其中参数以弧度为单位。
```



语法：



```plain
Cos ( n )
```



参数：



```plain
 n：数值型变量或表达式
```



返回值：



```plain
返回值：Double。
函数执行成功时返回n的余弦。
如果参数n的值为NULL，Cos()函数返回NULL。
```



**4、Exp**



功能：



```plain
计算e的n次方。
```



语法：



```plain
Exp ( n )
```



参数：



```plain
n：指定幂值
```



返回值：



```plain
返回值：Double。
函数执行成功时返回e（约等于2.71828）的n次方。 
如果参数n的值为NULL，Exp()函数返回NULL。
```



**5、Fact**



功能：



```plain
计算n的阶乘。
```



语法：



```plain
Fact ( n )
```



参数：



```plain
n：数值型变量或表达式
```



返回值：



```plain
返回值：Double。
函数执行成功时返回n的阶乘。
如果参数n的值为NULL，Fact()函数返回NULL。
```



**6、Int**



功能：



```plain
得到小于等于n的最大整数。
```



语法：



```plain
Int ( n )
```



参数：



```plain
n：数值型变量或表达式
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回小于等于n的最大整数。如果n的值太小或太大，超过了整数的表示范围，则函数返回0。
如果参数n的值为NULL，Int()函数返回NULL。
```



**7、Log**



功能：



```plain
计算n的自然对数。
```



语法：



```plain
Log ( n )
```



参数：



```plain
n：数值型变量或表达式，其值必须大于0
```



返回值：



```plain
返回值：Double。 
函数执行成功时返回n的自然对数。如果n小于等于0，将导致运行错误。
如果参数n的值为NULL，Log()函数返回NULL。
```



**8、LogTen**



功能：



```plain
计算n的常用对数（以10为底）。
```



语法：



```plain
LogTen ( n )
```



参数：



```plain
n：数值型变量或表达式，其值必须大于0
```



返回值：



```plain
返回值：Double。 
函数执行成功时返回n的常用对数。如果n小于等于0，将导致运行错误。
如果参数n的值为NULL，LogTen()函数返回NULL。
```



**9、Max**



功能：



```plain
求两个数中的最大值。
```



语法：



```plain
Max ( x, y )
```



参数：



```plain
x：数值型变量或表达式，参加比较的第一个数
y ：数值型变量或表达式，参加比较的第二个数
```



返回值：



```plain
返回值以x、y中数据类型更精确的数据类型作为该函数的返回值数据类型。
函数执行成功时返回参数比较的两个数中更大者。
如果任何参数的值为NULL，Max()函数返回NULL
```



**10、Min**



功能：



```plain
求两个数中的最小值。
```



语法：



```plain
Min( x, y )
```



参数：



```plain
x：数值型变量或表达式，参加比较的第一个数
y ：数值型变量或表达式，参加比较的第二个数
```



返回值：



```plain
返回值以x、y中数据类型更精确的数据类型作为该函数的返回值数据类型。
函数执行成功时返回参数比较的两个数中较小者。
如果任何参数的值为NULL，Min()函数返回NULL。
```



**11、Mod**



功能：



```plain
求余数。
```



语法：



```plain
Mod ( x, y )
```



参数：



```plain
x：数值型变量或表达式，被除数
y ：数值型变量或表达式，除数
```



返回值：



```plain
返回值以x、y中数据类型更精确的数据类型作为该函数的返回值数据类型。
函数执行成功时返回x除以y所得的余数 。
如果任何参数的值为NULL，Mod()函数返回NULL。
```



**12、Pi**



功能：



```plain
计算n与Pi(3.14159265358979323...)的乘积。
```



语法：



```plain
Pi ( n )
```



参数：



```plain
n：数值型变量或表达式
```



返回：



```plain
返回值：Double。 
函数执行成功时返回n与Pi(3.14159265358979323...)的乘积。
发生错误时返回-1。如果参数n的值为NULL，Pi()函数返回NULL。
```



**13、Rand**



功能：



```plain
得到1与n之间的一个伪随机数
```



语法：



```plain
Rand ( n )
```



参数：



```plain
n：数值型变量或表达式，指定要产生的伪随机数的上界。
有效值在1到32,767之间返回值与n的数据类型相同。
```



返回：



```plain
函数执行成功时返回1与n之间的一个伪随机数，包括1和n在内。
如果参数n的值为NULL，Rand()函数返回NULL。
```



**14、Randomize**



功能：



```plain
初始化伪随机数发生器，这样让应用程序每次使用不同的伪随机数序列。
```



语法：



```plain
Randomize ( n )
```



参数：



```plain
n：数值型变量或表达式，指定伪随机数生成器使用的起始值，不同的起始值可以生成不同的伪随机数序列。
当n的值为0时，该函数把系统时钟作为伪随机数生成器的起始值，这样可以生成不可重复的伪随机数序列。
当n的值不为0时，可以产生不同的伪随机数序列，但是，如果两次使用相同的伪随机数生成器起始值，那么两次生成的伪随机数序列相同。
n的值在0到32,767之间
```



返回值：



```plain
返回值：Integer。极少使用该函数的返回值。
```



**15、Round**



功能：



```plain
将x四舍五入到n位。
```



语法：



```plain
Round ( x, n )
```



参数：



```plain
x：要四舍五入的数值型数据
n：整数类型，指定从哪个小数位上四舍五入x。
有效值在0到18之间
```



返回值：



```plain
返回值：Decimal。 
函数执行成功时返回将x四舍五入到小数点后第n位的数值，如果函数执行失败或任何参数的值为NULL，Round()函数返回NULL。
```



**16、Sign**



功能：



```plain
确定n是整数、负数还是零。
```



语法：



```plain
Sign ( n )
```



参数：



```plain
n：数值型变量或表达式，指定要测试符号的值
```



返回值：



```plain
返回值Integer。当n大于0时返回1；当n小于0时返回-1；当n等于0时返回0。
如果参数n的值为NULL，Sign()函数返回NULL。
```



**17、Sin**



功能：



```plain
计算正弦，其中参数以弧度为单位。
```



语法：



```plain
Sin( n )
```



参数：



```plain
n：数值型变量或表达式
```



返回值：



```plain
返回值：Double。
函数执行成功时返回n的正弦。
如果参数n的值为NULL，Sin()函数返回NULL。
```



**18、Sqrt**



功能：



```plain
计算平方根。
```



语法：



```plain
Sqrt ( n )
```



参数：



```plain
数值型变量或表达式，指定要计算平方根的数据
```



返回值：



```plain
返回值：Double。
函数执行成功时返回n的平方根。
如果n是负数，则执行该函数时引发运行错误。
如果参数n的值为NULL，Sqrt()函数返回NULL。
```



**19、Tan**



功能：



```plain
计算正切，其中参数以弧度为单位。
```



语法：



```plain
Tan( n )
```



参数：



```plain
n：数值型变量或表达式
```



返回值：



```plain
返回值：Double。
函数执行成功时返回n的正切。
如果参数n的值为NULL，Tan()函数返回NULL。
```



**20、Truncate**



功能：



```plain
截断数值到指定的小数位。
```



语法：



```plain
Truncate ( x, n )
```



参数：



```plain
x：要截断的数值型数据
n：整数类型，指定从哪个小数位上截断x。
有效值在0到18之间
```



返回值：



```plain
返回值：Decimal。 
函数执行成功时返回将x截断到小数点后第n位的数值，如果函数执行失败或任何参数的值为NULL，Truncate()函数返回NULL。
所谓截断就是舍弃指定位之后的数值。
```



# 五、字符串



（1）、Fill



功能：



```plain
建立一个由指定字符串填充的指定长度的字符串。
```



语法：



```plain
Fill ( chars, n )
```



参数：



```plain
chars：string类型，指定用于重复填充的字符串

n：long类型，指定由该函数返回的字符串的长度
```



返回值：



```plain
返回值：String。
函数执行成功时返回n个字符的字符串，该字符串以参数chars中的字符串重复填充而成。
如果参数chars中的字符个数多于n个，那么使用chars字符串的前n个字符填充函数返回的字符串；
如果参数chars中的字符个数少于n个，那么使用chars字符串反复填充，直到返回的字符串长度达到n为止。
如果任何参数的值为NULL，Fill()函数返回NULL。
```



（2）、Left



功能：



```plain
得到字符串左部指定个数的字符。
```



语法：



```plain
Left ( string, n )
```



参数：



```plain
string：string类型，指定要提取子串的字符串

n：long类型，指定子串长度
```



返回值：



```plain
返回值String。 
函数执行成功时返回string字符串左边n个字符，发生错误时返回空字符串（""）。
如果任何参数的值为NULL，Left()函数返回NULL。
如果n的值大于string字符串的长度，那么Left()函数返回整个string字符串，但并不增加其它字符。
```



（3）、LeftTrim



功能：



```plain
返回指定字符串删除了左部空格后的字符串。
```



语法：



```plain
LeftTrim ( string )
```



参数：



```plain
string：string类型，指定要删除左部空格的字符串
```



返回值：



```plain
返回值：String。 
函数执行成功时返回删除了string字符串左部空格的字符串，发生错误时返回空字符串（""）。
如果任何参数的值为NULL，LeftTrim()函数返回NULL。
```



（4）、Len



功能：



```plain
得到字符串的长度。
```



语法：



```plain
Len (string)
```



参数：



```plain
string：string类型变量
```



返回值：



```plain
返回值：Long。 
函数执行成功时返回字符串的长度，发生错误时返回-1。
如果任何参数的值为NULL，则Len()函数返回NULL。
```



（5）、Lower



功能：



```plain
将字符串中的大写字母转换为小写字母。
```



语法：



```plain
Lower ( string )
```



参数：



```plain
string：要将其中的大写字母转换为小写字母的字符串
```



返回值：



```plain
返回值：String。 
函数执行成功时返回将大写字母转换为小写字母后的字符串，发生错误时返回空字符串（""）。
如果string参数的值为NULL，Lower()函数返回NULL。
```



（6）、Match



功能：



```plain
确定字符串中是否包含指定模式的字符
```



语法：



```plain
Match ( string, textpattern )
```



参数：



```plain
string：string类型，指定要检查是否匹配指定模式的字符串
textpattern：string类型，指定文本匹配模式
```



返回值：



```plain
返回值Boolean：如果字符串string与模式textpattern相匹配，则函数返回TRUE，否则返回FALSE。
如果指定的匹配模式无效或上述两个参数中的任何一个未曾赋值，那么Match()函数返回FALSE。
如果任何参数的值为NULL，Match()函数返回NULL。
```



用法



```plain
textpattern参数的写法与正则表达式十分相似，它由元字符和普通字符组成。
每个元字符都有不同的匹配含义，普通字符则与其自身相匹配。

下面是匹配模式中使用的元字符及其意义：

^ 指示字符串的开始，例如，^asd表示以asd开头的字符串，字符串asdfgh与模式^asd匹配，而字符串basdfg与模式^asd不匹配。
$ 指示字符串的结束，例如，red$表示所有以red结束的字符串均与该模式匹配，而redo与模式red$不匹配。
. 匹配任意单个字符，例如，^&&$匹配任何六个字符组成的字符串。
[] 匹配括号中列出的字符，例如，^[ABC]$匹配由一个字符组成的字符串，其值只能是A或B或C。

- 与方括号一起，指定匹配字符的范围，例如，^[A-Z]$只匹配那些由一个大写字母组成的字符串。方括号里还可以使用^字符，表示匹配不在指定范围内的任何字符，例如，[^0-9]匹配除数字外的任何字符。

* ，+，?这些符号跟在一个字符后面表示该字符可以出现的次数。

星号（*）表示可以出现0次或任意次；

加号（+）表示可以出现多次，但至少出现一次；

问号（?）表示出现0次或一次。

例如，
A*匹配0个或多个A（没有A、A、AA、AAA、AAAA、**）；
A+匹配1个或多个A（A、AA、AAA、AAAA、**）；
A?匹配空串或1个A。
\ 斜杠（\）是转义字符，它去掉特殊字符的特殊含义，比如，模式\$匹配字符$，模式\\匹配字符\。
```



（7）、Mid



功能：



```plain
取字符串的子串。
```



语法：



```plain
Mid ( string, start {, length } )
```



参数：



```plain
string：string类型，指定要从中提取子串的字符串
start：long类型，指定子串第一个字符在string字符串中的位置，第一个位置为1
length：long类型，可选项，指定子串的长度
```



返回值：



```plain
返回值：String
函数执行成功时返回string字符串中从start位置开始、长度为length的子串。
如果start参数的值大于string中字符个数，那么Mid()函数返回空字符串。
如果省略了length参数或length参数的值大于从start开始、string字符串中余下字符的长度，那么Mid()函数返回所有余下的字符。
如果任何参数的值为NULL，Mid()函数返回NULL。
```



（8）、Pos



功能：



```plain
在一个字符串中查找所包含的另一个字符串的起始位置。
```



语法：



```plain
Pos ( string1, string2 {, start } )
```



参数：



```plain
string1：string类型，指定要从中查找子串string2的字符串
string2：string类型，指定要在string1中查找的字符串
start：long类型，可选项，指定从string1的第几个字符开始查找。
缺省值为1
```



返回值：



```plain
返回值：Long。 
函数执行成功时返回在start位置后string2在string1中第一次出现的起始位置。
如果在string1中按指定要求未找到string2、或start的值超过了string1的长度，那么Pos()函数返回0。
如果任何参数的值为NULL，Pos()函数返回NULL。
用法Pos()函数在字符串查找时区分大小写，因此，"aa"不匹配"AA"。
```



（9）、Replace



功能：



```plain
将一个字符串中指定个数的字符串替换为另一个字符串。
```



语法：



```plain
Replace ( string1, start, n, string2 )
```



参数：



```plain
string1：string类型，指定要使用string2替换其中一部分内容的字符串
start：long类型，指定要从哪个字符位置开始替换字符串，字符串中第一个字符的位置为1
n：long类型，指定要替换多少个字符
string2：string类型，指定用哪个字符串替换string1的部分字符
```



返回值：



```plain
返回值：String。 
函数执行成功时返回替换后的字符串，发生错误时返回空字符串（""）。
如果任何参数的值为NULL，Replace()函数返回NULL。
```



用法：



```plain
如果start参数指定的位置超过了string1的长度，那么Replace()函数把将string2拼接到string1的后面形成的字符串返回。
如果n的值为0，那么Replace()函数把string2插入到string1指定位置后形成的字符串返回。
```



（10）、Right



功能：



```plain
从字符串右端取指定个数字符。
```



语法：



```plain
Right ( string, n )
```



参数：



```plain
string：string类型，指定要提取子串的字符串
n：long类型，指定子串长度
```



返回值：



```plain
返回值：String。
函数执行成功时返回string字符串右边n个字符，发生错误时返回空字符串（""）。
如果任何参数的值为NULL，Right()函数返回NULL。
如果n的值大于string字符串的长度，那么Right()函数返回整个string字符串，但并不增加其它字符。
```



（11）、RightTrim



功能：



```plain
删除字符串尾部空格
```



语法：



```plain
RightTrim ( string )
```



参数：



```plain
string：string类型，指定要删除右部空格的字符串
```



返回值：



```plain
返回值：String。 
函数执行成功时返回删除了string字符串右部空格的字符串，发生错误时返回空字符串（""）。
如果任何参数的值为NULL，RightTrim()函数返回NULL。
```



（12）、Space



功能：



```plain
生成一个由空格组成的指定字符个数的字符串
```



语法：



```plain
Space ( n )
```



参数：



```plain
n：long类型，指定要填充的空格个数，也就是填充后返回的字符串的长度
```



返回值：



```plain
返回值：String。 
函数执行成功时返回由n个空格组成的字符串，发生错误时返回空字符串。
如果参数n的值为NULL，Space()函数返回NULL
```



（13）、Trim



功能：



```plain
删除字符串首部和尾部的空格。
```



语法：



```plain
Trim ( string )
```



参数：



```plain
string：string类型，指定要删除首部和尾部空格的字符串
```



返回值：



```plain
返回值：String。 
函数执行成功时返回删除了string字符串首部和尾部空格的字符串，发生错误时返回空字符串（""）。
如果任何参数的值为NULL，Trim()函数返回NULL。
```



（14）、Upper



功能：



```plain
将字符串中的小写字母转换为大写字母。
```



语法：



```plain
Upper( string )
```



参数：



```plain
string：要将其中的小写字母转换为大写字母的字符串
```



返回值：



```plain
返回值：String。 
函数执行成功时返回将小写字母转换为大写字母后的字符串，发生错误时返回空字符串（""）。
如果string参数的值为NULL，Upper()函数返回NULL。
```



# 六、系统与环境



（1）、Clipboard



功能：



```plain
提取或替换Windows系统剪贴板的文本内容。
```



语法：



```plain
Clipboard ( { string } )
```



参数：



```plain
string：string类型，可选项，指定要复制到系统剪贴板上的文本。
如果剪贴板上已有内容的话，该文本将取代剪贴板的当前内容
```



返回值：



```plain
返回值：String。 
函数执行成功时，如果剪贴板上包含文本数据，那么函数返回剪贴板的当前内容；
如果剪贴板上包含非文本数据（比如位图）或不包含任何数据，那么函数返回空字符串（""）。
如果string参数的值为NULL，Clipboard()函数返回NULL。
用法无论是否指定string参数，Clipboard()都将返回剪贴板的当前内容。
当指定string参数时，剪贴板的原有内容被string参数的值取代；省略string参数时，仅仅得到剪贴板的内容。
```



（2）、CommandParm



功能：



```plain
得到应用程序运行时指定的命令参数。
```



语法：



```plain
CommandParm( )
```



返回值：



```plain
返回值：String。 

函数执行成功时返回应用程序运行时的命令行参数，函数执行错误或没有命令行参数时函数返回空字符串（""）。
```



用法：



```plain
命令行参数是应用程序启动时跟在应用程序名称后面的任何参数

比如，在运行窗口中输入了下述命令：

MyAppl C:\EMPLOYEE\EMPLIST.TXT

那么MyAppl应用程序中使用CommandParm()函数得到的命令行参数为：

C:\EMPLOYEE\EMPLIST.TXT

当应用程序的命令行中包含几个参数时，CommandParm()函数作为一个字符串返回所有参数。利用字符串操作函数可以分离各参数。

在应用对象的Open事件中没有必要执行CommandParm()函数。

此时，Open事件的argument参数中包含了命令行参数。
```



（3）、DoScript



功能：



```plain
执行AppleScript程序段，该函数只在Macintosh平台上有效。
```



语法：



```plain
DoScript ( script, result )
```



参数：



```plain
script：string类型，指定要运行的程序段（script）
result：string类型，由AppleScript程序段返回的结果信息或出错信息
```



返回值：



```plain
返回值：Integer。 
返回由AppleScript返回的结果代码。
如果任何参数的值为NULL，DoScript()函数返回NULL。
```



（4）、GetApplication



功能：



```plain
得到当前应用对象的句柄，这样你可以查询或设置应用对象的属性（通常用于编写通用代码）。
```



语法：



```plain
GetApplication ( )
```



返回值：



```plain
返回值：Application。
返回当前应用对象的句柄
```



（5）、GetEnvironment



功能：



```plain
得到操作系统、处理器、屏幕显示等与系统相关的信息。
```



语法：



```plain
GetEnvironment ( environmentinfo )
```



参数：



```plain
environmentinfo：Environment对象名，用于保存系统环境信息
```



返回值：



```plain
返回值：Integer。 

函数执行成功时返回1，发生错误时返回-1。

如果参数environmentinfo的值为NULL，GetEnvironment()函数返回NULL。

用法当开发交叉平台项目时，利用GetEnvironment()函数，应用程序能够得到当前运行的操作系统、使用的CPU类型、操作系统的版本、屏幕的大小以及颜色数等信息

这些信息的具体表示请参阅本书环境对象（Environment Object）的介绍。
```



（6）、GetFocus



功能：



```plain
确定当前焦点位于哪个控件上。
```



语法：



```plain
GetFocus ( )
```



返回值：



```plain
返回值：GraphicObject。 

函数执行成功时返回当前得到焦点控件的引用，发生错误时返回无效引用。

用法应用程序利用IsValid()函数可以检测GetFocus()是否返回有效的控件引用。

同时，使用TypeOf()函数可以确定控件的类型。
```



（7）、Post



功能：



```plain
将指定消息加入到某个窗口的消息队列中，这个窗口既可以是PowerBuilder应用的窗口，也可以是其它应用的窗口。
```



语法：



```plain
Post( handle, messageno, word, long )
```



参数：



```plain
handle：long类型，指定窗口的系统句柄，将向该窗口邮寄消息
messageno：UnsignedInteger类型，指定要邮寄的消息号 
word：long类型，指定与消息一起邮寄的word类参数值。如果messageno参数指定的消息不使用该参数，那么将这个参数的值设置为0
long：long类型或string，指定与消息一起邮寄的long型参数值或字符串
```



返回值：



```plain
返回值：Boolean。 
如果任何参数的值为NULL，Post()函数返回NULL。
```



用法：



```plain
Post()函数用于向窗口发送非PowerBuilder预定义事件的消息，这个窗口可以是PowerBuilder应用的窗口，也可以是其它应用的窗口。

Post()函数把发送的消息放置在指定窗口消息队列的尾部，然后返回到应用程序中，它并不等待相应事件事件处理程序的执行。

这一点与Send()函数不同，Send()函数直接触发指定窗口相应的事件，执行事件处理程序后返回到调用应用中。

因此，我们说Post()函数采用的是异步方式，Send()函数采用的是同步方式。

Post()函数的参数handle指定接收消息的窗口句柄，对PowerBuilder窗口来说，使用Handle()函数可以得到该句柄。

对其它应用程序的窗口来说，可以调用系统API函数查找窗口并得到相应窗口的句柄。

如果应用程序要邮寄PowerBuilder定义事件（包括预定义事件和用户定义事件），那么使用PostEvent()函数既简单有方便。

当应用程序在long参数位置指定一个字符串时，Post()函数复制一个该字符串的副本，然后将副本的地址传送给指定窗口。
```



（8）、ProfileInt



功能：



```plain
从初始化文件（.ini）中读取整型设置值。
```



语法：



```plain
ProfileInt ( filename, section, key, default )
```



参数：



```plain
filename：string类型，指定初始化文件的名称，可以包括路径，省略路径时，该函数按操作系统的标准路径搜索指定文件
section：string类型，指定要得到的值所在的节（Section）
key：string类型，指定要得到的值的名称，不用区分大小写
default：integer类型，当指定的文件、节名、项目名不存在或不能转换为整数时，函数返回该参数指定的值
```



返回值：



```plain
返回值：Integer。 
函数执行成功时，在指定的文件、节名、项目名不存在任何错误的情况下，函数返回相应项的值；
如果指定的文件、节名、项目名不存在或不能转换为整数时，函数返回default参数指定的缺省值。
如果发生错误，函数返回-1。如果任何参数的值为NULL，ProfileInt()函数返回NULL。
```



（9）、ProfileString



功能：



```plain
从初始化文件（.ini）中读取字符串型设置值
```



语法：



```plain
ProfileString ( filename, section, key, default )
```



参数：



```plain
filename：string类型，指定初始化文件的名称，可以包括路径，省略路径时，该函数按操作系统的标准路径搜索指定文件
section：string类型，指定要得到的值所在的节（Section）
key：string类型，指定要得到的值的名称，不用区分大小写
default：string类型，当指定的文件、节名、项目名不存在时，函数返回该参数指定的值
```



返回值：



```plain
返回值String。 
函数执行成功时，在指定的文件、节名、项目名不存在任何错误的情况下，函数返回相应项的值；
如果指定的文件、节名、项目名不存在，函数返回default参数指定的缺省值。
如果发生错误，函数返回空字符串。如果任何参数的值为NULL，ProfileString()函数返回NULL。
```



（10）、Restart



功能：



```plain
停止所有程序段的执行、关闭所有窗口、提交事务、断开与数据库的连接，然后重新启动应用程序
```



语法：



```plain
Restart()
```



返回值：



```plain
返回值Integer。
函数执行成功时返回1，发生错误时返回-1。
```



（11）、Run



功能：



```plain
运行指定的应用程序
```



语法：



```plain
Run ( string {, windowstate } )
```



参数：



```plain
string：string类型，指定要运行的应用程序的名称，其中可以包括路径以及相应的参数，就像在命令行中键入的那样
windowstate：WindowState枚举类型，可选项，指定程序运行时的窗口状态。
有效取值为：Maximized! - 最大化窗口；Minimized! - 最小化窗口；Normal! - 缺省值，正常窗口
```



返回值：



```plain
返回值Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，Run()函数返回NULL。
用法使用Run()函数，应用程序能够启动操作系统中的任何程序。
当在Run()参数中指定了要启动应用程序的参数时，参数的意义、格式、个数等由具体的应用程序确定。
如果在Run()函数的string参数中指定了文件名但没有给出扩展名时，PowerBuilder认为该文件的扩展名为.EXE。
要运行扩展名不是.EXE的应用程序（比如.BAT, .COM, 或.PIF），必须在Run()函数的参数中指定文件的扩展名。
```



（12）、Send



功能：



```plain
向窗口发送指定的消息并立即执行相应的事件处理程序
```



语法：



```plain
Send( handle, messageno, word, long )
```



参数：



```plain
handle：long类型，指定窗口的系统句柄，将向该窗口发送消息
messageno：UnsignedInteger类型，指定要发送的消息号
word：long类型，指定与消息一起发送的word类参数值。如果messageno参数指定的消息不使用该参数，那么将这个参数的值设置为0
long：long类型或string，指定与消息一起发送的long型参数值或字符串
```



返回值：



```plain
返回值：Long。 
函数执行成功时返回Windows系统调用SendMessage()的返回值，发生错误时返回-1。
如果任何参数的值为NULL，Send()函数返回NULL。
```



用法



```plain
Send()函数用于向窗口发送非PowerBuilder预定义事件的消息，这个窗口可以是PowerBuilder应用的窗口，也可以是其它应用的窗口。
Send()函数直接触发指定窗口相应的事件，执行事件处理程序后返回到调用应用中，这一点与Post()函数不同，Post()函数把发送的消息放置在指定窗口消息队列的尾部，然后返回到应用程序中，它并不等待相应事件事件处理程序的执行。
因此，我们说Post()函数采用的是异步方式，Send()函数采用的是同步方式。
Send()函数的参数handle指定接收消息的窗口句柄，对PowerBuilder窗口来说，使用Handle()函数可以得到该句柄。
对其它应用程序的窗口来说，可以调用系统API函数查找窗口并得到相应窗口的句柄。
实际上，Send()函数把它的各个参数直接传送给Windows的系统调用SendMessage()。
在各种C++开发工具的WINDOWS.H文件中可以查到各消息编号。
如果应用程序要发送PowerBuilder定义事件（包括预定义事件和用户定义事件），那么使用TriggerEvent()函数既简单有方便。
当应用程序在long参数位置指定一个字符串时，Send()函数复制一个该字符串的副本，然后将副本的地址传送给指定窗口。
```



（13）、SetProfileString



功能：



```plain
设置初始化文件中指定项的值
```



语法：



```plain
SetProfileString ( filename, section, key, value )
```



参数：



```plain
filename：string类型，指定初始化文件的名称，可以包括路径，省略路径时，该函数按操作系统的标准路径搜索指定文件
section：string类型，指定要设置的值所在的节（Section）
key：string类型，指定要设置的值的名称，不用区分大小写
default：string类型，指定要设置项的值
```



返回值：



```plain
返回值：Integer。 
函数执行成功时返回1，指定的文件未找到或指定的文件不能访问时函数返回-1。
如果任何参数的值为NULL，SetProfileString()函数返回NULL。
```



（14）、ShowHelp



功能：



```plain
显示应用程序帮助，该帮助使用Microsoft Windows帮助系统进行操作
```



语法：



```plain
ShowHelp ( helpfile, helpcommand {, typeid } )
```



参数：



```plain
helpfile：string类型，指定帮助文件的名称
helpcommand：HelpCommand枚举类型，指定显示帮助的格式。有效取值为：Index! - 显示目录主题，使用该值时不要指定
typeid参数；
Keyword! - 转移到由指定关键字确定的主题；
Topic! - 显示指定主题的帮助
typeid：可选项，指定帮助主题
```



返回值：



```plain
返回值：Integer。 
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，ShowHelp()函数返回NULL。
```



（15）、SignalError



功能：



```plain
触发应用对象的SystemError事件，通常用于代码调试。
```



语法：



```plain
SignalError ( { number }, { text } )
```



参数：



```plain
number：integer类型，可选项，其值将保存到Error对象的number属性中
text：string类型，可选项，其值将保存到Error对象的text属性中
```



返回值：



```plain
返回值：Integer。 
函数执行成功时返回1，发生错误时返回-1。
```



（16）、Yield



功能：



```plain
功能将控制权转移给其它图形对象，包括非PowerBuilder对象。该函数检测消息队列，如果有消息，就把消息取出。利用该函数可以在执行耗时较长的操作时把控制权转让给其它应用。
```



语法：



```plain
Yield()
```



返回值：



```plain
返回值：Boolean。 
如果在消息队列中提取到了消息，那么函数返回TRUE，否则返回FALSE。
```



用法



```plain
正常情况下，PowerBuilder应用程序在执行一段代码（比如函数或事件处理程序）的过程中不响应用户的操作。
对耗时短暂的代码段来说，这种处理方式没有什么不妥的地方
但是，如果某个代码段的执行耗时较长，应用程序又希望为用户提供更多的控制权，那么需要在这段代码中插入Yield()函数，让用户能够进行其它操作，特别在循环执行的代码中更应该如此。
应用程序执行Yield()函数后，如果发现消息队列中存在消息，它将允许对象处理这些消息，处理之后，继续Yield()函数后面代码的执行。
因此，代码中插入Yield()函数将降低应用程序的运行效率
```



# 七、日期时间



（1）、Day



功能：



```plain
得到日期型数据中的号数(1到31之间的整数值)。
```



语法：



```plain
Day ( date )
```



参数：



```plain
date：要得到号数的日期值
```



返回值：



```plain
返回值：Integer
函数执行成功时返回号数(1到31之间的整数值)。
如果date参数的值为NULL，则Day()函数返回NULL
```



（2）、DayName



功能：



```plain
得到指定日期是一周中的星期几(例如，Sunday, Monday...)。
```



语法：



```plain
DayName ( date )
```



参数：



```plain
date：date类型值或变量
```



返回值：



```plain
返回值：String。 
函数执行成功时返回指定日期的星期表示(例如，Sunday, Monday...)。
如果date参数的值为NULL，则DayName()函数返回NULL。
```



（3）、DayNumber



功能：



```plain
得到日期型数据是一星期中的第几天(用1到7之间的整数表示，星期天为1，星期一为2，...)。
```



语法：



```plain
DayNumber ( date )
```



参数：



```plain
date：date类型值或变量
```



返回值：



```plain
返回值：Integer。 
函数执行成功时返回指定日期是一星期中的第几天(用1~7表示，星期天为1，星期一为2，...)。
如果date参数的值为NULL，则DayNumber()函数返回NULL。
```



（4）、DaysAfter



功能：



```plain
得到两个日期间的天数。
```



语法：



```plain
DaysAfter ( date1, date2 )
```



参数：



```plain
date1：date类型，指定起始日期 

date2：date类型，指定终止日期
```



返回值：



```plain
返回值：Long。 
函数执行成功时得到两个日期之间的天数。
如果date2的日期在date1的前面，那么DaysAfter()函数返回负值。
如果任何参数的值为NULL，则DaysAfter()函数返回NULL
```



（5）、Hour



功能：



```plain
得到时间值中的小时，采用24小时制
```



语法：



```plain
Hour ( time )
```



参数：



```plain
time：time类型的值
```



返回值：



```plain
返回值：Integer。 
函数执行成功时得到time参数中的小时（00到23之间）。
如果time参数的值为NULL，则Hour()函数返回NULL。
```



（6）、Minute



功能：



```plain
得到时间值中的分钟，有效值在00～59之间。
```



语法：



```plain
Minute ( time )
```



参数：



```plain
time：time类型的值
```



返回值：



```plain
返回值：Integer。 
函数执行成功时得到time参数中的分钟（00到59之间）。
如果time参数的值为NULL，则Minute()函数返回NULL
```



（7）、Month



功能：



```plain
得到日期值中的月份，有效值在1～12之间
```



语法：



```plain
Month ( date )
```



参数：



```plain
date：date类型的值
```



返回值：



```plain
返回值：Integer。 
函数执行成功时得到date参数中的月份（1到12之间）。
如果date参数的值为NULL，则Month()函数返回NULL。
```



（8）、Now



功能：



```plain
得到客户机的当前系统时间
```



语法：



```plain
Now()
```



返回值：



```plain
返回值：Time。 
该函数返回客户机的当前系统时间。
```



（9）、RelativeDate



功能：



```plain
得到指定日期前多少天或后多少天的日期
```



语法：



```plain
RelativeDate(date,n)
```



参数：



```plain
date：Date类型，指定基准日期
n：integer类型，指定天数
```



返回值：



```plain
返回值：Date。
当n的值大于0时返回参数date指定日期后第n天的日期；
当n的值小于0时返回参数date指定日期前第n天的日期。
如果任何参数的值为NULL，则RelativeDate()函数返回NULL
```



（10）、RelativeTime



功能：



```plain
得到指定时间前多少秒或后多少秒的时间，采用24小时制
```



语法：



```plain
RelativeTime ( time, n )
```



参数：



```plain
time：time类型，指定基准时间
n：long类型，指定秒数
```



返回值：



```plain
返回值：Time。 
当n的值大于0时返回参数time指定时间后第n秒的时间；
当n的值小于0时返回参数time指定时间前第n秒的时间。
如果任何参数的值为NULL，则RelativeTime()函数返回NULL
```



（11）、Second



功能：



```plain
得到时间值中的秒，有效值在00～59之间
```



语法：



```plain
 Second ( time )
```



参数：



```plain
time：time类型的值
```



返回值：



```plain
返回值：Integer。 
函数执行成功时得到time参数中的秒（00到59之间）。
如果time参数的值为NULL，则Second()函数返回NULL
```



（12）、Today



功能：



```plain
得到当前系统日期，在某些情况下，同时得到当前系统时间
```



语法：



```plain
Today()
```



返回值：



```plain
返回值：Date。

该函数返回当前系统日期。

用法单独调用Today()函数时，该函数总是返回当前系统日期

但是，虽然Today()函数的返回值类型为Date，在该函数用做某些函数的参数、而该参数要求DateTime类型的值时，Today()函数也能够在返回当前系统日期的同时返回当前系统时间。

再如，Today()函数作为数据窗口控件SetItem()函数的参数，该函数参数中指定的数据窗口列的数据类型为DateTime，那么当前系统日期和时间将同时设置到数据窗口指定项中。
```



（13）、Year



功能：



```plain
得到日期值中的年度(有效取值1000到3000)。
```



语法：



```plain
Year(date)
```



参数：



```plain
date：date类型的值
```



返回值：



```plain
返回值：Integer。 

函数执行成功时得到date参数中的年份（采用四位数字），发生错误时返回1900，如果date参数的值为NULL，则Year()函数返回NULL。

用法当应用程序把有两位数字表示年份的字符串转换成日期时

PowerBuilder根据下述规则选择世纪：

如果年份值在00到49之间，PowerBuilder将年份中的世纪（前两位数字）当作20；

如果年份值在50到99之间，PowerBuilder将年份中的世纪（前两位数字）当作19。

比如，字符串"20-10-25"被PowerBuilder转换为2020-10-25；字符串"98-10-25"被PowerBuilder转换为1998-10-25。

因此，如果应用程序中需要指定1950年之前的日期，应该使用四位数字表示年份，以避免引起歧义。

PowerBuilder能够处理的年份从1000到3000之间
```



# 八、定时



（1）、CPU



功能：



```plain
到自当前应用程序启动后开始CPU所消耗的时间，以毫秒为单位
```



语法：



```plain
CPU()
```



返回值：



```plain
返回值：Long
返回自当前应用程序启动后开始CPU所消耗的时间，以毫秒为单位
```



（2）、Idle



功能：



```plain
该函数在用户每次活动（例如，按键盘、移动鼠标等）后重置定时器，n秒后触发应用对象的Idle事件。
```



语法：



```plain
Idle ( n )
```



参数：



```plain
n：指定空闲时间间隔，以秒为单位。

该参数的值设置为0时，停止空闲检测，不再触发应用对象的Idle事件

用法

利用Idle()函数，应用程序可以构造自己的屏幕保护程序，避免安全数据的泄露。

当使用Idle()函数已经启动了定时器后，如果再次以非0参数调用Idle()函数，那么该函数重设时间间隔，但并不启动新的定时器。

Idle()函数启动定时器后，如果在指定的时间间隔（从用户最近一次操作算起）内没有操作应用程序，那么就触发应用对象的Idle事件

在这个事件中可以编写关闭窗口、退出数据库登录等一系列代码，然后使用Restart()函数重新启动应用程序，起到保密的目的。

发生下述任何情况时，系统自动重置定时器（即重新开始计时）：

n 用户在该应用程序的任何窗口内移动鼠标或单击鼠标（双击鼠标时首先触发单击事件）

n 在该应用程序的某个窗口是当前窗口时用户按下了任意一个或多个键

n 在该应用程序的窗口最小化时，用户在该应用的图标上单击鼠标或移动鼠标

n 在该应用程序的窗口最小化并且该应用程序是当前应用程序（应用名称被加亮显示）时，用户按了任何按键

n 可视数据窗口检索数据时引起的编辑控件（指漂浮在数据窗口当前行/列上的编辑控件）重绘操作
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，此时启动定时器。
如果不能启动定时器或定时器未启动而n的值指定为0时，函数返回-1。
如果任何参数的值为NULL，Idle()函数返回NULL。
```



（3）、Timer



功能：



```plain
在指定的时间间隔内反复触发指定窗口的定时器事件
```



语法：



```plain
Timer ( interval {, windowname } )
```



参数：



```plain
interval：指定两次触发Timer事件之间的时间间隔，有效值在0到65之间。如果该参数的值指定为0，那么关闭定时器，不再触发指定窗口的Timer事件

windowname：窗口名，指定时间间隔到时要触发哪个窗口的Timer事件。省略该参数时，触发当前窗口的Timer事件
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，Timer()函数返回NULL。
```



用法：



```plain
用法

使用Timer()函数可以周期性地触发指定窗口的Timer事件，这样，每当时间间隔过去时，应用程序都可以完成一些周期性的工作，比如绘制简单动画等。

将Timer()的interval参数设置为非0值时启动定时器并开始计时；将该函数的interval参数设置为0时关闭定时器，终止计时任务。

需要注意的是，在Microsoft Windows系统中，该函数能够计时的最小时间间隔为0.055秒（约1/18秒），如果把interval参数的值设置小于0.055，那么该定时器将每隔0.055秒触发一次窗口的Timer事件。

Microsoft Windows 3.x最多只支持系统中同时启动16个定时器。
```



# 九、注册



（1）、RegistryDelete



功能：



```plain
删除Windows系统注册库中的一个键或键的某个值
```



语法：



```plain
RegistryDelete ( key, valuename )
```



参数：



```plain
key：string类型，指定键名，将删除该键或删除该键的某个值

valuename：string类型，指定要删除的值的名称。

如果想删除键、键的值、以及其下的所有子键，那么将该参数指定为空字符串
```



返回值：



```plain
返回值Integer。 
函数执行成功时返回1，发生错误时返回-1。
```



用法



```plain
为了唯一地标识某个键，在key参数中，可以从根键开始依次指定各级父键，各键之间使用反斜杠（\）分隔
```



（2）、RegistryGet



功能：



```plain
从系统注册库中得到指定键的值。
```



语法：



```plain
RegistryGet ( key, valuename, valuetype, valuevariable )
```



参数：



```plain
key：string类型，指定键名

valuename：string类型，指定要访问值的名称。每个键可以有一个未命名的值和多个命名的值。要访问未命名的值，把该参数指定为空字符串（""）

valuetype:RegistryValueType枚举类型，指定值的数据类型。有效取值请参看用法

valuevariable:用于保存键值的变量，其数据类型应该与valuetype参数指定的类型相匹配
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。

如果valuevariable的数据类型与valuetype参数指定的类型不匹配，将引发运行错误。
用法valuetype的可能取值为：

RegString!以空字符结束的字符串

RegExpandString!以空字符结束的字符串

其中包括了对环境变量的非扩展应用

RegBinary!二进制数据

ReguLong!32位数据

ReguLongBigEndian!32位大数据

RegLink!Unicode符号链

RegMultiString!动态字符串数组

为了唯一地标识某个键，在key参数中，可以从根键开始依次指定各级父键，各键之间使用反斜杠（\）分隔。
```



（3）、RegistryKeys



功能：



```plain
从系统注册库中得到指定键的有效子键。
```



语法：



```plain
RegistryKeys ( key, subkeys )
```



参数：



```plain
key：string类型，指定键名

subkeys：字符串数组变量，用于保存各子键
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。

用法

在subkeys参数中可以使用定长数组，也可以使用动态数组。

使用动态数组时，数组的上界反映了能够得到的子键个数。

当使用定长数组时，其数组元素个数必须足够多，保证能够容纳所有子键，但是，在具体得到子键之前，没有办法能够预先知道实际子键个数。

为了唯一地标识某个键，在key参数中，可以从根键开始依次指定各级父键，各键之间使用反斜杠（\）分隔。
```



（4）、RegistrySet



功能：



```plain
在系统注册库中设置或创建指定键
```



语法：



```plain
RegistrySet ( key, valuename, valuetype, value )
```



参数：



```plain
key：string类型，指定键名

valuename：string类型，指定要访问值的名称。每个键可以有一个未命名的值和多个命名的值。

要访问未命名的值，把该参数指定为空字符串（""）。如果注册库中不存在指定值名，该函数将创建新的值名

valuetype：RegistryValueType枚举类型，指定值的数据类型。有效取值请参看用法

value：要设置的值，其数据类型应该与valuetype参数指定的类型相匹配
```



返回值：



```plain
返回值Integer。

函数执行成功时返回1，发生错误时返回-1。

如果valuevariable的数据类型与valuetype参数指定的类型不匹配，将引发运行错误。
```



用法



```plain
valuetype的可能取值为：

RegString!以空字符结束的字符串

RegExpandString!以空字符结束的字符串

其中包括了对环境变量的非扩展应用

RegBinary!二进制数据

ReguLong!32位数据

ReguLongBigEndian!32位大数据

RegLink!Unicode符号链

RegMultiString!动态字符串数组

为了唯一地标识某个键，在key参数中，可以从根键开始依次指定各级父键，各键之间使用反斜杠（\）分隔。
```



（5）、RegistryValues



功能：



```plain
得到与指定键相关的一组值名。该函数在Windows 3.1中无效。
```



语法：



```plain
RegistryValues ( key, valuename )
```



参数：



```plain
key：string类型，指定键名

valuename：字符串数组变量，用于保存值名
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。
```



用法



```plain
在valuename 参数中可以使用定长数组，也可以使用动态数组。

使用动态数组时，数组的上界反映了能够得到的值名个数。

当使用定长数组时，其数组元素个数必须足够多，保证能够容纳所有值名，但是，在具体得到值名之前，没有办法能够预先知道实际值名个数。

为了唯一地标识某个键，在key参数中，可以从根键开始依次指定各级父键，各键之间使用反斜杠（\）分隔。
```



# 十、文件



（1）、FileOpen



功能：



```plain
以指定的读写方式打开指定的文件，同时返回该文件的句柄。
```



语法：



```plain
FileOpen(filename{,filemode{,fileaccess{,filelock{,writemode,{creator,filetype}}}}})
```



参数：



```plain
filename：string类型，指定要打开文件的名称，其中可以包含路径 

filemode：FileMode枚举类型，可选项，指定文件打开方式。有效取值为：（LineMode! - 缺省值，行模式）（StreamMode! - 流模式）

fileaccess：FileAccess枚举类型，可选项，指定文件访问方式。有效取值为：（Read! - 缺省值，只读方式，这样打开的文件只能进行读操作；）（Write! - 只写方式，这样打开的文件只能进行写操作）

filelock：FileLock枚举类型，可选项，指定文件加锁方式。有效取值为：

n LockReadWrite! - 缺省值，只有打开该文件的用户能够访问该文件，其它用 户对该文件的访问均被拒绝； 

n LockRead! - 只有打开该文件的用户能够读该文件，但其它任何用户均可写该文件；

n LockWrite! - 只有打开该文件的用户能够写该文件，但其它任何用户均可读该文件；

n Shared! - 所有用户均可读写该文件

writemode：WriteMode枚举类型，可选项，当fileaccess参数指定为Write!时，该参数指定在指定文件已经存在时数据的添加方式。

有效取值为：

Append! - 缺省值，将数据添加到原文件尾部；

Replace! - 覆盖原有数据

creator：可选项，用于Macintosh机，使用四个字符的字符串指定文件的创建者。指定该参数后，必须同时指定filetype参数

filetype：可选项，用于Macintosh机，使用四个字符的字符串指定文件类型
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回打开文件的句柄，随后的文件操作函数利用该句柄完成对文件的操作。
发生错误时函数返回-1。
如果任何参数的值为NULL，那么FileOpen()函数返回NULL。
```



用法



```plain
当文件以行模式打开时，每执行一次FileRead()函数读取一行数据；每执行一次FileWrite()函数，该函数自动在写出的字符串末尾增加一个回车（CR）换行（LF）符

（这是应用程序在Windows 系统中运行时的情况，在UNIX下只加一个换行字符）。

当文件以流模式打开时，执行一次FileRead()函数读取32,765个字节的数据，如果余下数据没有这么多，那么FileRead()函数就读取所有余下的数据；

执行一次FileWrite()函数时，最多可写入32,765个字节的数据，并且不添加回车换行字符。

当文件以写方式使用FileOpen()函数打开时，如果指定的文件不存在，那么FileOpen()函数创建该文件。
```



（2）、FileWrite



功能：



```plain
向指定文件中写数据。
```



语法：



```plain
FileWrite (fileno , variable )
```



参数：



```plain
fileno：integer类型，指定文件句柄（由FileOpen()函数得到） 

variable：string或blob类型，其值将写入fileno参数指定的文件
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回写入文件的字符或字节数，发生错误时返回-1。

如果任何参数的值为NULL，那么FileWrite()函数返回NULL。
```



用法



```plain
FileWrite()函数从当前文件指针开始写入指定数据，写入之后，将文件指针调整到刚刚写入数据的下一个字节位置。

当文件以writemode参数设置为Replace!方式打开时，文件指针最初位于文件的开头位置；

当文件以writemode参数设置为Append!方式打开时，文件指针最初位于文件的结尾位置。

当文件以行模式打开时，执行FileWrite()函数时，该函数自动在每次写入数据的后面加上回车换行符，并把文件指针移动到回车换行符后面。

当文件以流模式打开时，FileWrite()函数一次最多写入32,765个字节。如果variable参数中数据的长度超过了32,765个字节，那么FileWrite()函数只向文件中写入前32,765个字符并返回32,765。
```



（3）、FileRead



功能：



```plain
从指定文件中读取数据。
```



语法：



```plain
FileRead ( fileno, variable )
```



参数：



```plain
fileno：integer类型，指定文件句柄（由FileOpen()函数得到）

variable：string或blob类型的变量，用于保存读取的数据
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回读取的字符数或字节数；

如果在读取任何字符前读到了文件结束符（EOF），则FileRead()函数返回-100；

当指定文件以行模式打开时，如果在读取任何字符之前遇到了回车（CR）或换行（LF）字符，则FileRead()函数返回0。

如果发生其它错误，FileRead()函数返回-1。如果任何参数的值为NULL，那么FileRead()函数返回NULL。
```



用法



```plain
当指定文件以行模式（Line Mode）打开时，FileRead()函数一次读取一行数据

并把它保存到参数variable中，然后跳过行结束符（回车换行符，操作系统不同，使用的字符也不同），把文件指针移动到下一行的起始位置。

当文件以流模式（Stream Mode）打开时，FileRead()函数或一直读取到文件结尾，或读取32,765字节的数据，决定于两者哪个数据长度更短些。
```



（4）、FileClose



功能：



```plain
关闭先前用FileOpen()函数打开的文件。
```



语法：



```plain
FileClose ( fileno )
```



参数：



```plain
fileno：integer，指定要关闭文件的文件句柄，该句柄使用FileOpen()函数打开文件时得到
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。

如果fileno参数的值为NULL，那么FileClose()函数返回NULL。
```



（5）、FileExists



功能：



```plain
检查指定的文件是否存在。
```



语法：



```plain
FileExists ( filename )
```



参数：



```plain
filename：string类型，指定要检查存在性的文件的文件名，其中可以包含路径
```



返回值：



```plain
返回值：Boolean。 
如果指定文件存在时返回TRUE，不存在时返回FALSE。
如果filename参数的值为NULL，那么FileExists()函数返回NULL。
```



用法



```plain
如果filename参数指定的文件被另一个应用加锁锁住，那么FileExists()函数也将返回FALSE。
```



（6）、FileDelete



功能：



```plain
删除指定的文件。
```



语法：



```plain
FileDelete ( filename )
```



参数：



```plain
filename：string类型，指定要删除文件的文件名，其中可以包含路径
```



返回值：



```plain
返回值：Boolean。
函数执行成功时返回TRUE，发生错误时返回FALSE。
如果filename参数的值为NULL，那么FileDelete()函数返回NULL。
```



（7）、FileLength



功能：



```plain
得到指定文件的长度（以字节为单位）
```



语法：



```plain
FileLength ( filename )
```



参数：



```plain
filename：string类型，指定要得到其长度的文件的文件名，其中可以包含路径
```



返回值：



```plain
返回值：Long。

函数执行成功时返回指定文件的长度（以字节为单位）。

如果指定的文件不存在，函数返回-1。

如果filename参数的值为NULL，那么FileLength()函数返回NULL。
```



（8）、FileSeek



功能：



```plain
将文件指针移动到指定位置。读写文件时相应函数会自动移动文件指针。
```



语法：



```plain
FileSeek ( fileno, position, origin )
```



参数：



```plain
fileno：integer类型，指定文件句柄（由FileOpen()函数得到）

position：long类型，指定相对于origin参数指定位置的新位置偏移量，以字节为单位

origin：SeekType枚举类型，指定从哪里开始移动文件指针，即指针移动的基准。有效取值为：

FromBeginning! - 缺省值，从文件开头移动指针；

FromCurrent! - 从当前位置移动文件指针；

FromEnd! - 从文件结尾处移动文件指针
```



返回值：



```plain
返回值：Long。

函数执行成功时返回指针移动后的指针位置。

如果任何参数的值为NULL，那么FileSeek()函数返回NULL。
```



（9）、GetFileOpenName



功能：



```plain
显示打开文件对话框，让用户选择要打开的文件。
```



语法：



```plain
GetFileOpenName(title,pathname,filename{,extension{,filter}})
```



参数：



```plain
title：string类型，指定对话框的标题

pathname：string类型变量，用于保存该对话框返回的文件路径及文件名

filename：string类型变量，用于保存该对话框返回的文件名

extension：string类型，可选项，使用1到3个字符指定缺省的扩展文件名 

filter：string类型，可选项，其值为文件名掩码，指定显示在该对话框的列表框中供用户选择的文件名满足的条件（比如*.*，*.TXT，*.EXE等）
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1；当用户单击了对话框上的“Cancel”按钮时函数返回0；发生错误时返回-1。
如果任何参数的值为NULL，那么GetFileOpenName()函数返回NULL。
```



用法



```plain
filter参数的格式为：description,*. ext缺省值为："All Files (*.*),*.*"其中，description说明扩展名的意义，比如“所有文件”、“文本文件”等。

你可以根据需要指定在打开文件对话框中显示的文件名类型。

当需要指定多种文件类型时，各类型之间使用逗号分隔

例如："PIF 文件, *.PIF, 批处理文件, *.BAT"需要注意的是，该函数只是得到一个文件名，而并没有打开文件，需要打开文件时，依然需要使用FileOpen()函数。
```



（10）、GetFileSaveName



功能：



```plain
显示保存文件对话框，让用户选择要保存到的文件。
```



语法：



```plain
GetFileSaveName(title,pathname,filename{,extension{,filter}})
```



参数：



```plain
title：string类型，指定对话框的标题

pathname：string类型变量，用于保存该对话框返回的文件路径及文件名

filename：string类型变量，用于保存该对话框返回的文件名

extension：string类型，可选项，使用1到3个字符指定缺省的扩展文件名

filter：string类型，可选项，其值为文件名掩码，指定显示在该对话框的列表框中供用户选择的文件名满足的条件（比如*.*，*.TXT，*.EXE等）
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1；当用户单击了对话框上的“Cancel”按钮时函数返回0；发生错误时返回-1。

如果任何参数的值为NULL，那么GetFileSaveName()函数返回NULL。
```



用法



```plain
filter参数的格式为：description,*. ext缺省值为："All Files (*.*),*.*"其中，description说明扩展名的意义，比如“所有文件”、“文本文件”等。

你可以根据需要指定在打开文件对话框中显示的文件名类型。当需要指定多种文件类型时，各类型之间使用逗号分隔

例如："PIF 文件, *.PIF, 批处理文件, *.BAT"需要注意的是，该函数只是得到一个文件名，而并没有打开文件，需要打开文件时，依然需要使用FileOpen()函数。
```



# 十一、库管理



（1）、LibraryCreate



功能：



```plain
创建一个空的PowerBuilder应用库，并可根据需要在创建应用库的同时添加库注解
```



语法：



```plain
LibraryCreate ( libraryname{, comments } )
```



参数：



```plain
libraryname：string类型，指定要创建应用库的名称，可以带上路径，不带路径时在当前目录下创建应用库 

comments：string类型，可选项，指定要创建的应用库的注解
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。

如果任何参数的值为NULL，LibraryCreate()函数返回NULL。
```



用法



```plain
LibraryCreate()函数在指定路径下创建一个空的PowerBuilder应用库（PBL）。
如果在指定应用库名称时没有指定文件的扩展名，那么该函数自动加上扩展名.PBL。
```



（2）、LibraryDelete



功能：



```plain
删除应用库库文件或应用库中的数据窗口对象。
```



语法：



```plain
LibraryDelete ( libraryname{, objectname, objecttype } )
```



参数：



```plain
libraryname：string类型，指定库名，可以带上路径，不带路径时在系统搜索路径下查找应用库

objectname：string类型，可选项，指定要从库中删除的数据窗口对象的名称

objecttype：LibImportType类型，可选项，指定要删除对象的类型，目前仅支持ImportDataWindow!
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，LibraryDelete()函数返回NULL。
```



用法



```plain
执行LibraryDelete()函数时，如果未指定后两个参数，那么该函数删除指定的应用库；
如果指定了后两个参数，那么该函数删除指定应用库中指定的数据窗口对象。
LibraryDelete()函数只能删除应用库中的数据窗口对象，如果想删除其它对象
那么只能在PowerBuilder开发环境中使用库管理画笔（Library Painter）来实现了。
```



（3）、 LibraryDirectory



功能：



```plain
得到应用库中指定对象的信息列表，内容包括对象名称、最近修改日期和时间、以及对象的注释。
```



语法：



```plain
LibraryDirectory ( libraryname, objecttype )
```



参数：



```plain
libraryname：string类型，指定PowerBuilder应用库的名称，如果名称中未指定路径，那么该函数根据操作系统标准的文件搜索路径查找指定文件 

objecttype：LibDirType枚举类型，指定希望函数列出的对象类型，有效取值请参看用法。
```



返回值：



```plain
返回值String。

函数执行成功时返回一个字符串，每个对象占用一行，行中各信息之间使用Tab字符（~t）分隔。行中信息格式为：对象名~t修改日期/时间~t注释~n发生错误时函数返回空字符串（""）。

如果任何参数的值为NULL，LibraryDirectory()函数返回NULL。
```



用法



```plain
LibraryDirectory()函数的objecttype参数是个LibDirType枚举类型的量，其有效取值为

DirAll!得到所有对象的信息

DirApplication!得到应用对象的信息

DirDataWindow!得到所有数据窗口对象的信息

DirFunction!得到所有函数对象的信息

DirMenu!得到所有菜单对象的信息

DirPipeline!得到所有数据管道对象的信息

DirProject!得到工程对象的信息

DirQuery!得到所有查询对象的信息

DirStructure!得到所有结构对象的信息

DirUserObject!得到所有用户对象的信息

DirWindow!得到所有窗口对象的信息使用

LibraryDirectory()函数得到指定对象的名称、修改日期/时间以及可能的注释后，应用程序既可以使用Pos()函数进行定位和字符串分割，也可以使用数据窗口的ImportString()函数将结果显示在数据窗口中。
```



（4）、LibraryExport



功能：



```plain
从指定应用库中以对象的语法定义格式卸出对象
```



语法：



```plain
LibraryExport ( libraryname, objectname, objecttype )
```



参数：



```plain
libraryname：string类型，指定要移出对象的应用库的名称，如果名称中未指定路径，那么该函数根据操作系统标准的文件搜索路径查找指定文件
objectname：string类型，指定要移出对象的名称
objecttype ：LibExportType枚举类型，指定要移出对象的类型，具体取值请参看用法
```



返回值：



```plain
返回值String。
函数执行成功时返回指定对象的语法，该语法与使用库管理画笔（Library Painter）移出对象时的语法相同，区别在于LibraryExport()函数省略了移出语法的头部。
如果发生错误，则函数返回空字符串（""）。
如果任何参数的值为NULL，LibraryExport()函数返回NULL。
```



用法



```plain
LibraryExport()的objecttype参数的可能取值为： 

ExportApplication!应用对象

ExportDataWindow!数据窗口对象

ExportFunction!函数对象

ExportMenu!菜单对象

ExportPipeline!数据管道对象

ExportProject!工程对象

ExportQuery!查询对象

ExportStructure!结构对象

ExportUserObject!用户对象

ExportWindow!窗口对象
```



（5）、LibraryImport



功能：



```plain
将以语法格式表示的数据窗口对象装入指定的应用库中
```



语法：



```plain
LibraryImport(libraryname,objectname,objecttype,syntax,errors{,comments } )
```



参数：



```plain
libraryname：string类型，指定要移入对象的应用库的名称，如果名称中未指定路径，那么该函数根据操作系统标准的文件搜索路径查找指定文件

objectname：string类型，指定要移入的数据窗口对象的名称 

objecttype：LibImportType枚举类型，指定要移入对象的类型，目前该函数只支持ImportDataWindow!，表示只能向应用库中移入数据窗口对象

syntax：string类型，指定要移入数据窗口对象的语法

errors：string类型变量，用于在发生错误时保存出错信息

comments：string类型，可选项，用于指定移入对象的注解
```



返回值：



```plain
返回值Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，LibraryImport()函数返回NULL。
用法当应用程序在运行过程中动态创建数据窗口对象后，可以使用LibraryImport()函数把动态数据窗口对象的定义保存到应用库中，以后就可以直接使用该对象了。
```



# 十二、打印



（1）、Print



功能：



```plain
以当前字体在打开的打印作业中打印一行或多行文本
```



语法：



```plain
Print(printjobnumber,{tab1,}string{,tab2})
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号 

tab1：Integer类型，可选项，指定文本开始打印的位置，在开始打印字符串之前将打印光标移动到该位置，从打印区的左边界开始计算，以千分之一英寸为单位。

如果打印光标已经位于指定位置、或打印光标已经超过了指定位置、或省略了该参数，那么，Print()函数从打印光标的当前位置开始打印

string：string类型，指定要打印的字符串。如果字符串中包括回车换行字符（~r~n），那么该字符串将被分成多行输出，但是，除第一行之外，其它行忽略tab1参数指定的起始打印位置

tab2：Integer类型，可选项，指定字符串打印结束后打印光标移动到的位置，从打印区的左边界开始计算，以千分之一英寸为单位。

如果打印光标已经超过了指定位置，那么Print()函数忽略该参数，打印光标位于已打印字符串的尾部。如果省略了该参数，Print()函数把打印光标移动到下一行的起始位置。
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。

如果任何参数的值为NULL，Print()函数返回NULL。

用法

在打印作业中，PowerBuilder使用打印光标来跟踪打印位置。打印光标保存了即将打印区域左上角的坐标。

使用Print()函数打印文本后，PowerBuilder自动更新打印光标。

PowerBuilder使用行距来决定打印出的两行文本之间的距离，行距与字符的高度成比例，缺省的行距是字符高度的1.2倍。

使用PrintSetSpacing()函数可以改变行距。

当Print()函数在下一行打印输出时，它把打印光标的x坐标设置为0、y坐标增加当前行距指示的数值。

由于每打印一行时Print()函数都自动调整打印光标的y坐标位置，因此，该函数会自动处理分页，因此，应用程序没有必要调用PrintPage()函数进行分页。

打印区由纸张的物理尺寸和边界空白决定，PrintSend()函数能够发送具体打印机的ESC控制序列，使用这个函数可以改变边界空白的大小。

另外，在打印开始之前，使用PrintDefineFont()和PrintSetFont()函数可以改变Print()使用的字体。
```



（2）、PrintBitmap



功能：



```plain
在打印区域的指定位置打印位图
```



语法：



```plain
PrintBitmap ( printjobnumber, bitmap, x, y, width, height )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

bitmap：string类型，指定要打印的位图文件的文件名

x：integer类型，指定位图起始打印位置的x坐标，以千分之一英寸为单位

y：integer类型，指定位图起始打印位置的y坐标，以千分之一英寸为单位

width：integer类型，指定位图的打印宽度，以千分之一英寸为单位。如果该参数的值指定为0，那么按图像的原始宽度打印

height：integer类型，指定位图的打印高度，以千分之一英寸为单位。如果该参数的值指定为0，那么按图像的原始高度打印
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。

如果任何参数的值为NULL，PrintBitmap()函数返回NULL。

用法执行PrintBitmap()函数后，打印光标的位置不变，依然停留在执行该函数前的位置上。
```



（3）、PrintCancel



功能：



```plain
取消用PrintOpen()函数启动的打印作业
```



语法：



```plain
PrintCancel ( printjobnumber )
```



参数：



```plain
printjobnumber：要取消的打印作业的作业号
```



返回值：



```plain
返回值：Integer。 

函数执行成功时返回1，发生错误时返回-1。

如果参数printjobnumber的值为NULL，PrintCancel()函数返回NULL。
```



用法



```plain
PrintCancel()函数取消指定的打印作业，删除相应的打印池文件，关闭打印作业，所以，应用程序执行了PrintCancel()函数之后，不需要再执行PrintClose()函数关闭打印作业了
```



（4）、PrintClose



功能：



```plain
关闭打印作业并把打印页面发送到打印机上
```



语法：



```plain
PrintClose ( printjobnumber )
```



参数：



```plain
printjobnumber：要关闭的打印作业的作业号
```



返回值：



```plain
返回值Integer。函数执行成功时返回1，发生错误时返回-1。 

如果参数printjobnumber的值为NULL，PrintClose()函数返回NULL。
```



用法



```plain
应用程序使用PrintOpen()函数启动打印作业后，必须使用PrintClose()在完成打印任务后关闭打印作业，或根据需要使用PrintCancel()函数取消打印作业
```



（5）、PrintDataWindow



功能：



```plain
打印数据窗口控件的内容，用该函数可以在一个打印作业中打印多个数据窗口控件的内容，每个都从新的一页开始打印
```



语法：



```plain
PrintDataWindow ( printjobnumber, dwcontrol )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号 

dwcontrol：要打印其内容的数据窗口控件名或子数据窗口控件名
```



返回值：



```plain
返回值Integer。函数执行成功时返回1，发生错误时返回-1。

如果参数printjobnumber的值为NULL，PrintDataWindow()函数返回NULL。
```



用法



```plain
应用程序通过多次执行PrintDataWindow()函数可以在一个打印作业中一次打印多个数据窗口的内容，并且每个数据窗口都从新的一页开始打印。

当数据窗口的表现风格为RichTextEdit时，数据窗口中的每一行都在新的一页上开始打印。

需要注意的是，PrintDataWindow()函数在打印数据窗口时使用数据窗口本身定义的字体以及风格，使用PrintDefineFont()和PrintSetFont()函数为当前作业定义的字体不起作用。
```



（6）、PrintDefineFont



功能：



```plain
定义打印作业使用的字体，对每个打印作业PowerBuilder支持八种字体。
```



语法：



```plain
PrintDefineFont(printjobnumber,fontnumber,facename,height,weight,fontpitch,fontfamily, italic,underline)
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

fontnumber：指定赋给当前定义字体的编号，有效值在1到8之间 

facename：string类型，指定字体名称，该字体应该是你的打印机支持的字体，比如“宋体”

height：Integer类型，使用正值指定字体的高度，以千分之一英寸为单位；使用负值指定字体点数，比如，-18代表18点。一般来说，使用点数更精确些

weight：指定字体的磅数，正常字体为400磅，粗体为700磅

fontpitch：FontPitch枚举类型，指定字体标准。有效取值为：

Default! - 缺省值；

Fixed! - 固定形式；

Variable! - 可变形式

fontfamily：FontFamily枚举类型，指定字体系列。有效取值为：AnyFont!、Decorative!、Modern!、Roman!、Script!、Swiss!

italic：boolean类型，指定是否使用斜体样式。有效取值为：TRUE - 使用斜体样式；FALSE - 不使用斜体样式。缺省值为FALSE

underline：boolean类型，指定是否加下划线。有效取值为：TRUE - 加下划线；FALSE - 不加下划线。缺省值为FALSE
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回1，发生错误时返回-1。

如果任何参数的值为NULL，PrintDefineFont()函数返回NULL。

用法在一个打印作业中，应用程序能够最多同时定义8种字体。

当应用程序需要使用更多的字体时，可以在使用了某个字体号输出内容后使用PrintDefineFont()函数将该字体号对应的字体更换为其它字体。
```



（7）、PrintLine



功能：



```plain
在当前打印页上绘出指定厚度的一条线
```



语法：



```plain
PrintLine ( printjobnumber, x1, y1, x2, y2, thickness )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

x1：integer类型，指定直线起点的x坐标，以千分之一英寸为单位

y1：integer类型，指定直线起点的y坐标，以千分之一英寸为单位

x2：integer类型，指定直线终点的x坐标，以千分之一英寸为单位

y2：integer类型，指定直线终点的y坐标，以千分之一英寸为单位

thickness：integer类型，指定直线的厚度，以千分之一英寸为单位
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。如果任何参数的值为NULL，PrintLine()函数返回NULL。
```



用法



```plain
应用程序执行了PrintLine()函数后，该函数并不改变打印光标的位置
```



（8）、PrintOpen



功能：



```plain
启动打印作业并返回作业号
```



语法：



```plain
PrintOpen ( { jobname } )
```



参数：



```plain
jobname：string类型，可选项，指定要打开打印作业的名称，该名称将显示在打印管理器窗口中
```



返回值：



```plain
返回值Long。
函数执行成功时返回打印作业号，发生错误时返回-1。
如果任何参数的值为NULL，PrintOpen()函数返回NULL。
```



用法



```plain
应用程序执行PrintOpen()函数后，启动新的打印作业并走纸到下一页，同时将打印机缺省字体设置为该打印作业的字体。

打印光标的位置位于打印区的左上角。

其它同组的打印函数使用PrintOpen()函数返回的作业号来标识作业。

需要注意的是，使用PrintOpen()函数打开打印作业、使用同组的其它函数完成打印任务后，必须使用PrintClose()关闭打印作业，或根据需要使用PrintCancel()函数取消打印作业。
```



（9）、PrintOval



功能：



```plain
在指定位置以指定线宽绘制椭圆或圆
```



语法：



```plain
PrintOval ( printjobnumber, x, y, width, height, thickness )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

x：integer类型，指定椭圆或圆外形框左上角的x坐标，以千分之一英寸为单位

y：integer类型，指定椭圆或圆外形框左上角的y坐标，以千分之一英寸为单位

width：integer类型，指定椭圆或圆外形框的宽度，以千分之一英寸为单位

height：integer类型，指定椭圆或圆外形框的高度，以千分之一英寸为单位

thickness：integer类型，指定椭圆或圆外边线的厚度，以千分之一英寸为单位
```



返回值：



```plain
返回值Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintOval()函数返回NULL。
```



用法



```plain
应用程序执行了PrintOval()函数后，该函数并不改变打印光标的位置。
PrintOval()函数绘出的椭圆或圆是实心的，也就是说，执行该函数后，椭圆或圆下面的文字或图像将完全被覆盖。
如果想在椭圆或圆中输出文字或图形，那么应用程序应该首先绘制椭圆或圆，然后使用其它函数在椭圆或圆中输出文字或图形。
```



（10）、PrintPage



功能：



```plain
将当前页发送给打印机或打印池并在当前打印作业中启动一个新的打印页
```



语法：



```plain
PrintPage ( printjobnumber )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintPage()函数返回NULL
```



（11）、PrintRect



功能：



```plain
在指定位置以指定线宽打印矩形
```



语法：



```plain
PrintRect ( printjobnumber, x, y, width, height, thickness )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

x：integer类型，指定矩形左上角的x坐标，以千分之一英寸为单位

y：integer类型，指定矩形左上角的y坐标，以千分之一英寸为单位

width：integer类型，指定矩形的宽度，以千分之一英寸为单位

height：integer类型，指定矩形的高度，以千分之一英寸为单位

thickness：integer类型，指定矩形边线的厚度，以千分之一英寸为单位
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintRect()函数返回NULL。
```



用法



```plain
应用程序执行了PrintRect()函数后，该函数并不改变打印光标的位置。
PrintRect()函数绘出实心的矩形，也就是说，执行该函数后，矩形下面的文字或图像将完全被覆盖。
如果想在矩形中输出文字或图形，那么应用程序应该首先绘制矩形，然后使用其它函数在矩形中输出文字或图形。
```



（12）、PrintRoundRect



功能：



```plain
在指定位置以指定线宽打印圆角矩形
```



语法：



```plain
PrintRoundRect(printjobnumber,x,y,width,height,xradius,yradius,thickness)
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

x：integer类型，指定圆角矩形左上角的x坐标，以千分之一英寸为单位

y：integer类型，指定圆角矩形左上角的y坐标，以千分之一英寸为单位

width：integer类型，指定圆角矩形的宽度，以千分之一英寸为单位

height：integer类型，指定圆角矩形的高度，以千分之一英寸为单位

xradius：integer类型，指定圆角矩形圆角部分的x半径，以千分之一英寸为单位

yradius：integer类型，指定圆角矩形圆角部分的y半径，以千分之一英寸为单位

thickness：integer类型，指定圆角矩形边线的厚度，以千分之一英寸为单位
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintRoundRect()函数返回NULL。
```



用法



```plain
应用程序执行了PrintRoundRect()函数后，该函数并不改变打印光标的位置。

PrintRoundRect()函数绘出实心的圆角矩形，也就是说，执行该函数后，圆角矩形下面的文字或图像将完全被覆盖。

如果想在圆角矩形中输出文字或图形，那么应用程序应该首先绘制圆角矩形，然后使用其它函数在圆角矩形中输出文字或图形。
```



（13）、PrintScreen



功能：



```plain
在打印作业中打印屏幕图像
```



语法：



```plain
PrintScreen ( printjobnumber, x, y {, width, height } )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

x：integer类型，指定要打印屏幕图像左上角在打印页上的x坐标，以千分之一英寸为单位

y：integer类型，指定要打印屏幕图像左上角在打印页上的y坐标，以千分之一英寸为单位

width：integer类型，可选项，指定屏幕图像的打印宽度，以千分之一英寸为单位。如果省略了该参数，那么PowerBuilder按屏幕的原始宽度打印屏幕图像。如果指定了该参数，必须同时指定height参数

height：integer类型，可选项，指定屏幕图像的打印高度，以千分之一英寸为单位。如果省略了该参数，那么PowerBuilder按屏幕的原始高度打印屏幕图像
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintScreen()函数返回NULL。
```



（14）、PrintSend



功能：



```plain
直接向打印机发送任意字符串，通常用于发送打印机的控制代码
```



语法：



```plain
PrintSend ( printjobnumber, string {, zerochar } )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

string：string类型，指定发送到打印机的字符串。在该字符串中，使用非打印字符的ASCII码值表示非打印字符

zerochar：integer类型，可选项，指定在string参数中用于表示数值0的ASCII码值。有效取值在1到255之间
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintSend()函数返回NULL。
```



用法



```plain
应用程序使用PrintSend()函数可以直接向打印机发送控制序列（换码序列），比如，设置打印文字的浓淡、打印页的四周空白等。

不同类型的打印机使用不同的控制序列，你需要翻一翻你的打印机手册。

由于PowerBuilder使用数值0（即ASCII码为0的字符）结束每个字符串，因此，如果打印控制序列中包含了数值0，应用程序需要使用其它字符在参数string中替代数值0，并用zerochar参数指明这个替代字符。

一般来说，应该选择一个打印机控制序列中不使用的字符作为0值字符的替代字符。

通常情况下，按下述次序组织打印作业：

1. 使用PrintOpen()函数打开打印作业

2. 使用PrintSend()函数设置打印机特性，比如打印方向、四周空白等

3. 使用PrintDefineFont()和PrintSetFont()函数设置该打印作业使用的字体

4. 使用该组的其它函数打印输出文字或图形5. 执行PrintClose()函数关闭打印作业
```



（15）、PrintSetFont



功能：



```plain
设置当前打印作业使用的字体
```



语法：



```plain
PrintSetFont ( printjobnumber, fontnumber )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号 

fontnumber：指定该打印作业使用字体的字体编号，该编号与PrintDefineFont()函数中定义的编号应该对应，字体编号的有效取值在1到8之间，0表示使用打印机的缺省字体
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回当前字体的高度，发生错误时返回-1。
如果任何参数的值为NULL，PrintSetFont()函数返回NULL。
```



（16）、PrintSetSpacing



功能：



```plain
设置行间距因子，打印函数将使用该因子来决定行间距
```



语法：



```plain
PrintSetSpacing ( printjobnumber, spacingfactor )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

spacingfactor：指定行间距因子，用字符高度的倍数表示，缺省值为1.2
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintSetSpacing()函数返回NULL。
```



用法



```plain
在PowerBuilder应用程序中，行间距与字符的高度成正比，缺省值为字符高度的1.2倍。

当Print组函数生成新行时，系统自动把打印光标的x坐标位置设置为0，y坐标位置在原有基础上增加当前行距值。

使用PrintSetSpacing()函数可以改变当前打印作业的行距。
```



（17）、PrintSetup



功能：



```plain
打开打印机设置对话框
```



语法：



```plain
PrintSetup ( )
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，PrintSetup()函数返回NULL。
```



用法



```plain
当系统中安装了多种打印机时，在Windows 95中PrintSetup()函数打开如图2-1所示的对话框，单击“Setup”按钮设置打印机各种特性。

如果系统中只有一个打印机，则直接打开该打印机的打印设置对话框。

需要注意的是，在Windows95和Windows NT 3.51以后的版本中，使用PrintSetup()函数设置的打印机设置只对当前应用起作用，并不影响其它应用的打印机设置。

对Windows 3.1来说，使用PrintSetup()函数设置的打印机设置影响系统中的所有应用
```



（18）、PrintText



功能：



```plain
在指定位置打印一行文本
```



语法：



```plain
PrintText ( printjobnumber, string, x, y {, fontnumber } )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

string：string类型，指定要打印的文本

x：integer类型，指定文本开始打印位置的x坐标，以千分之一英寸为单位

y：integer类型，指定文本开始打印位置的y坐标，以千分之一英寸为单位

fontnumber：可选参数，指定打印文本使用的字体号，该编号由PrintDefineFont()函数确定。省略该参数时，以打印作业的当前字体打印文本
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回文本打印后打印光标的x位置，即参数x的值加上打印文本的宽度。
发生错误时返回-1。
如果任何参数的值为NULL，PrintText()函数返回NULL。
```



（19）、PrintWidth



功能：



```plain
确定一个字符串在指定打印作业中按当前字体所占的宽度，以千分之一英寸为单位
```



语法：



```plain
PrintWidth ( printjobnumber, string )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号

string：string类型，指定要决定其打印宽度的字符串
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回按当前字体计算的字符串打印宽度，以千分之一英寸为单位，发生错误时返回-1。
如果任何参数的值为NULL，PrintWidth()函数返回NULL。
```



（20）、PrintX



功能：



```plain
返回打印光标的x坐标位置
```



语法：



```plain
PrintX ( printjobnumber )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回打印光标的x坐标位置，以千分之一英寸为单位，发生错误时返回-1。
如果任何参数的值为NULL，PrintX()函数返回NULL。
```



（21）、PrintY



功能：



```plain
返回打印光标的y坐标位置
```



语法：



```plain
PrintY ( printjobnumber )
```



参数：



```plain
printjobnumber：用PrintOpen()函数打开的打印作业号
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回打印光标的y坐标位置，以千分之一英寸为单位，发生错误时返回-1。
如果任何参数的值为NULL，PrintY()函数返回NULL。
```



# 十三、窗口



（1）、Open



功能：



```plain
打开窗口。

该函数有两种语法格式：
语法一、打开编程时已知数据类型的窗口对象；
语法二、打开程序运行后才能确定数据类型的窗口对象。
```



语法：



```plain
语法一、Open ( windowvar {, parent } )
语法二、Open ( windowvar, windowtype {, parent } )
```



参数：



```plain
语法一、
windowvar：要打开窗口的窗口名，可以使用窗口画笔定义的窗口对象名，也可以使用该窗口对象的某个变量。
Open()函数把打开窗口的引用放置到windowvar变量中
parent：可选项，指定要打开窗口的父窗口，要打开窗口成为父窗口的子窗口，只有当要打开窗口需要成为某个窗口的子窗口时才需要指定该参数。
如果应用程序使用Open()函数打开某个子窗口或弹出窗口而又省略了该参数，那么当前活动窗口成为被打开窗口的父窗口

语法二、
windowvar：指定窗口变量名，Open()函数把打开窗口的引用放置到该变量中
windowtype：string类型，指定要打开窗口的数据类型，该参数指定的窗口数据类型必须与windowvar参数的类型相同或是windowvar类型的后继对象
parent：可选项，指定要打开窗口的父窗口，要打开窗口成为父窗口的子窗口，只有当要打开窗口需要成为某个窗口的子窗口时才需要指定该参数。
```



返回值：



```plain
语法一、
返回值：Integer。函数执行成功时返回1，发生错误时返回-1。如果任何参数的值为NULL，Open()函数返回NULL。 

语法二、
返回值：Integer。函数执行成功时返回1，发生错误时返回-1。如果任何参数的值为NULL，Open()函数返回NULL。
```



（2）、Close



功能：



```plain
关闭窗口并释放窗口以及窗口上的控件所占据的内存。
```



语法：



```plain
Close(windowname)
```



参数：



```plain
windowname：要关闭窗口的名称
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果参数windowname的值为NULL，Close()函数返回NULL。
```



用法



```plain
应用程序使用Open()或其它Open簇函数打开窗口后，不需要窗口时，可以使用Close()关闭窗口并释放窗口以及窗口上所有控件占据的内存。

Close()函数的执行过程为：如果要关闭窗口的CloseQuery和/或Close事件已经编写了事件处理程序，那么执行这些事件处理程序，从屏幕上删除要关闭的窗口、关闭窗口、之后执行调用Close()函数语句后面的语句。

当窗口被关闭后，应用程序就不能再访问已经关闭窗口的属性、实例变量、对象函数、以及窗口上的控件了。

如果关闭窗口后应用程序依然访问上述特性，那么将引发运行错误。

当然，应用程序也可以阻止窗口被关闭，方法很简单，只要在欲阻止关闭窗口的CloseQuery事件处理程序中使用RETURN语句返回1即可，格式为：RETURN1
```



（3）、OpenWithParm



功能：



```plain
带参数打开窗口，与打开窗口的Open()函数相似，OpenWithParm()有两种语法格式：

语法一、带参数打开编程时已知数据类型的窗口对象；
语法二、带参数打开程序运行后才能确定数据类型的窗口对象。
```



语法：



```plain
语法一、
OpenWithParm(windowvar,parameter{,parent}) 

语法二、
OpenWithParm(windowvar,parameter,windowtype{,parent})
```



参数：



```plain
语法一、

windowvar：要打开窗口的窗口名，可以使用窗口画笔定义的窗口对象名，也可以使用该窗口对象的某个变量。Open()函数把打开窗口的引用放置到windowvar变量中

parameter：指定要传递给打开窗口的数据，该数据保存在Message对象的属性中，parameter参数的数据类型必须是下述三种类型之一：String、Numeric、PowerObject

parent：可选项，指定要打开窗口的父窗口，要打开窗口成为父窗口的子窗口，只有当要打开窗口需要成为某个窗口的子窗口时才需要指定该参数。如果应用程序使用Open()函数打开某个子窗口或弹出窗口而又省略了该参数，那么当前活动窗口成为被打开窗口的父窗口

语法二、

windowvar：指定窗口变量名，Open()函数把打开窗口的引用放置到该变量中

parameter：指定要传递给打开窗口的数据，该数据保存在Message对象的属性中，parameter参数的数据类型必须是下述三种类型之一：String、Numeric、PowerObject

windowtype：string类型，指定要打开窗口的数据类型，该参数指定的窗口数据类型必须与windowvar参数的类型相同或是windowvar类型的后继对象

parent：可选项，指定要打开窗口的父窗口，要打开窗口成为父窗口的子窗口，只有当要打开窗口需要成为某个窗口的子窗口时才需要指定该参数。如果应用程序使用Open()函数打开某个子窗口或弹出窗口而又省略了该参数，那么当前活动窗口成为被打开窗口的父窗口
```



返回值：



```plain
语法一、
返回值：Integer。函数执行成功时返回1，发生错误时返回-1。如果任何参数的值为NULL，OpenWithParm()函数返回NULL。

语法二、
返回值：Integer。函数执行成功时返回1，发生错误时返回-1。如果任何参数的值为NULL，OpenWithParm()函数返回NULL。
```



用法



```plain
消息对象Message有三个属性用于存储OpenWithParm()函数传递给打开窗口的数据。根据parameter参数数据类型的不同，该参数的值保存在Message对象的不同属性中。
```



（4）、CloseWithReturn



功能：



```plain
关闭窗口并将返回值保存在Message对象中，该函数只能对响应窗口使用
```



语法：



```plain
CloseWithReturn ( windowname, returnvalue)
```



参数：



```plain
windowname：要关闭窗口的名称

returnvalue：指定关闭窗口时保存到Message对象中的值，调用CloseWithReturn()函数的代码段通过查看Message对象属性的值得到关闭窗口时被关闭窗口传递的值。

returnvalue参数必须是下述三种类型之一：String、Numeric、PowerObject
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果参数任何的值为NULL，CloseWithReturn()函数返回NULL。
```



（5）、OpenSheet



功能：



```plain
在MDI框架窗口中打开MDI子窗口，并在指定菜单中创建选择该子窗口的菜单项
```



语法：



```plain
OpenSheet(sheetrefvar{,windowtype},mdiframe{,position{,arrangeopen}})
```



参数：



```plain
sheetrefvar：指定要作为工作表打开的窗口名

windowtype：string类型，可选项，指定要打开窗口的类型（也就是窗口画笔中保存的窗口对象名）

mdiframe：指定要放置工作表的MDI框架窗口名

position：可选参数，指定所打开的工作表的名称作为一个菜单项显示在第几个菜单标题下面，缺省时，被放在倒数第二个菜单标题下，原因是，大多数商业软件的最后两个菜单标题是Window和Help，把工作表的名称放到Window菜单标题中用于选择工作表窗口是个合情合理的选择

arrangeopen：ArrangeOpen枚举类型，可选参数，但如果选用了此参数，那么position参数也必须同时指定。arrangeopen参数告诉系统如何显示打开的工作表
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果参数任何的值为NULL，OpenSheet()函数返回NULL。
```



用法



```plain
arrangeopen参数的可能取值为：Cascaded!
把一个工作表放在另一个的上面，每个都向右下方偏移一点，这样所有工作表的标题栏用户都能看到。该值是OpenSheet()函数的缺省选择。
Layered!将工作表显示在客户区的左上角，并最大化工作表，使其充满MDI框架窗口的整个客户区。
Original!操作动作与Cascaded!参数相同，只是不放大窗口，而以窗口定义时的大小显示。
```



（6）、OpenSheetWithParm



功能：



```plain
在MDI框架窗口中打开MDI子窗口，同时把参数保存在Message对象中进行传递。
```



语法：



```plain
OpenSheetWithParm(sheetrefvar,parameter{,windowtype},mdiframe{,position{,arrangeopen}}
```



参数：



```plain
sheetrefvar：指定要作为工作表打开的窗口名

parameter：指定要传递给打开工作表的数据，该数据保存在Message对象的属性中， parameter参数的数据类型必须是下述三种类型之一：String、Numeric、PowerObject

windowtype：string类型，可选项，指定是要打开窗口的类型（也就是窗口画笔中保存的窗口对象名）

mdiframe：指定要放置工作表的MDI框架窗口名

position：可选参数，指定所打开的工作表的名称作为一个菜单项显示在第几个菜单标题下面，缺省时，被放在倒数第二个菜单标题下，原因是，大多数商业软件的最后两个菜单标题是Window和Help，把工作表的名称放到Window菜单标题中用于选择工作表窗口是个合情合理的选择

arrangeopen：ArrangeOpen枚举类型，可选参数，但如果选用了此参数，那么position参数也必须同时指定。arrangeopen参数告诉系统如何显示打开的工作表
```



返回值：



```plain
返回值：Integer。函数执行成功时返回1，发生错误时返回-1。如果参数任何的值为NULL，OpenSheet()函数返回NULL。
```



用法



```plain
arrangeopen参数的可能取值为：Cascaded!
把一个工作表放在另一个的上面，每个都向右下方偏移一点，这样所有工作表的标题栏用户都能看到。该值是OpenSheet()函数的缺省选择。
Layered!将工作表显示在客户区的左上角，并最大化工作表，使其充满MDI框架窗口的整个客户区。
Original!操作动作与Cascaded!参数相同，只是不放大窗口，而以窗口定义时的大小显示。
```



# 十四、国际化



（1）、Reverse



功能：



```plain
颠倒字符串中字符次序
```



语法：



```plain
Reverse ( string )
```



参数：



```plain
string：要颠倒字符次序的字符串
```



返回值：



```plain
返回值：String。 
函数执行成功时返回颠倒字符次序后的字符串，如果发生错误，那么返回空字符串（""）。
```



用法



```plain
Reverse()函数将一个字符串中最后一个字符放置到另一个字符串的第一个字符位置、倒数第二个字符放置在另一个字符串的第二个字符位置，以此类推
```



（2）、ToAnsi



功能：



```plain
将Unicode字符转换成ANSI字符。
```



语法：



```plain
ToAnsi ( string )
```



参数：



```plain
string：要进行转换的Unicode编码的字符串
```



返回值：



```plain
返回值：Blob。
函数执行成功时返回指定字符串对应的ANSI编码的blob类型数据，发生错误时返回空值（NULL）。
```



（3）、ToUnicode



功能：



```plain
将ANSI字符转换成Unicode字符。
```



语法：



```plain
ToUnicode( blob)
```



参数：



```plain
blob：要进行转换的ANSI编码的blob类型数据
```



返回值：



```plain
返回值：String。
函数执行成功时返回指定字符串对应的Unicode编码的字符串，发生错误时返回空字符串。
```



# 十五、其他



（1）、IntHigh



功能：



```plain
得到Long型值的高位字
```



语法：



```plain
IntHigh ( long )
```



参数：



```plain
long：long型值或变量
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回参数long的高位字，发生错误时返回-1。
如果参数long的值为NULL，IntHigh()函数返回NULL。
```



用法



```plain
IntHigh()函数通常用于分解外部C或C++语言函数的返回值和Windows消息。
```



（2）、IntLow



功能：



```plain
得到Long型值的低位字
```



语法：



```plain
IntLow ( long )
```



参数：



```plain
long：long型值或变量
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回参数long的低位字，发生错误时返回-1。
如果参数long的值为NULL，IntLow()函数返回NULL。
```



用法



```plain
IntLow()函数通常用于分解外部C或C++语言函数的返回值和Windows消息。示例请参看IntHigh()函数。
```



（3）、IsValid



功能：



```plain
检查对象变量是否已经实例化，即实例变量的值是否是个有效的对象句柄。
```



语法：



```plain
 IsValid ( objectname )
```



参数：



```plain
objectname：要检测的对象名
```



返回值：



```plain
返回值：Boolean。
如果指定对象已经创建了对象实例，那么IsValid()函数返回TRUE，否则返回FALSE。
如果参数objectname的值为NULL，IsValid()函数返回NULL。
```



（4）、 KeyDown



功能：



```plain
检查用户是否按了键盘上指定的键
```



语法：



```plain
KeyDown ( keycode )
```



参数：



```plain
keycode：KeyCode枚举类型或integer类型，指明要检测的按键或某个键的ASCII值
```



返回值：



```plain
返回值：Boolean。

如果用户按了keycode参数指定的按键，函数返回TRUE，否则返回FALSE。

如果参数keycode的值为NULL，KeyDown()函数返回NULL。
```



用法



```plain
KeyDown()函数通常在某个事件的事件处理程序中调用，它并不指明用户键入了哪个字符，而是说明当前事件（即事件处理程序中调用KeyDown()函数的事件）发生时用户正按着哪个按键。

一般来说，应用程序在窗口的Key事件或控件的按键事件中调用KeyDown()函数，以检测用户是否按了某个特殊键。

对控件来说，PowerBuilder没有定义预定义的Key事件，这也没有关系

如果在控件得到焦点后希望应用程序检测用户的按键，只要对该控件定义一个用户事件，并把pbm_keydown （其它控件）或pbm_dwnkey（数据窗口控件）映射到该用户事件上即可。
```



（5）、MessageBox



功能：



```plain
显示一个消息对话框
```



语法：



```plain
MessageBox(title,text{,icon{,button{,default}}})
```



参数：



```plain
title：string类型，指定消息对话框的标题

text：指定消息对话框中显示的消息，该参数可以是数值数据类型、字符串或boolean值

icon：Icon枚举类型，可选项，指定要在该对话框左侧显示的图标

button：Button枚举类型，可选项，指定显示在该对话框底部的按钮

default：数值型，可选项，指定作为缺省按钮的按钮编号，按钮编号自左向右依次计数，缺省值为1，如果该参数指定的编号超过了显示的按钮个数，那么MessageBox()函数将使用缺省值
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回用户选择的按钮编号（例如1、2、3等），发生错误时返回-1。
如果任何参数的值为NULL，MessageBox()函数返回NULL。
```



用法



```plain
当你的应用程序需要显示一段简短信息（比如显示出错、警告等信息）时，没有必要自己从头创建窗口、安排控件，使用MessageBox()函数既简单又方便。

用户只有响应该窗口后，程序才能继续运行下去。

MessageBox()函数的icon参数指定显示在窗口中的图标，它是枚举类型，可能取值为： 

图标 Information! StopSign! Exclamation! Question! None! 

无图标其中Information!是Icon参数的缺省值。

Button参数指定在窗口中显示哪些按钮，有效取值为：

OK!“确定”按钮

OKCancel!“确定”、“取消”按钮

YesNo!“是”、“否”按钮 

YesNoCancel!“是”、“否”、“取消”按钮

RetryCancel!“重试”、“取消”按钮

AbortRetryIgnore!“终止”、“重试”、“忽略”按钮
```



（6）、PixelsToUnits



功能：



```plain
将像素值转换为PowerBuilder单位PBU
```



语法：



```plain
PixelsToUnits ( pixels, type )
```



参数：



```plain
pixels：integer类型，指定要转换为PowerBuilder单位的像素数

type：ConvertType枚举类型，指定按哪个方向进行转换。有效取值为：

XPixelsToUnits! - 按水平方向转换像素；

YPixelsToUnits! - 按垂直方向转换像素
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回pixels参数指定像素数按指定方向转换成的PowerBuilder单位数，发生错误时返回-1。
如果任何参数的值为NULL，PixelsToUnits()函数返回NULL。
```



用法



```plain
窗口中水平方向和垂直方向相同的像素数表示的距离并不相同。

如果你使用水平方向和垂直方向相同的像素数绘制一个方框，那么你会看到，该方框不是正方形而是个矩形，而使用PBU计量的相同单位数将绘出正方形。

因此，在进行单位转换时，需要指明按那么方向进行转换。
```



（7）、PopulateError



功能：



```plain
以应用程序定制的错误号和错误信息填充Error对象，该函数不触发应用对象的SystemError事件。
```



语法：



```plain
PopulateError ( number, text )
```



参数：



```plain
number：integer类型，指定要保存到Error对象number属性中的值

text：string类型，指定要保存到Error对象text属性中的值
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
```



用法



```plain
当应用程序需要根据变量的当前取值来定制Error对象时，可以使用PopulateError()函数来填充Error对象的number和text属性，同时该函数根据上下文自动填充Error对象的其它属性。

定制了Error对象后，应用程序可以使用不带参数的SignalError()函数触发应用对象的SystemError事件。

这样，在SystemError事件的事件处理程序中可以编写处理定制错误和系统错误的通用代码。

如果应用程序没有对SystemError事件编写事件处理程序，那么SignalError()函数什么也不做。
```



（8）、RGB



功能：



```plain
将代表红、绿、蓝三原色的三个整数组合成一个表示颜色的长整数
```



语法：



```plain
RGB ( red, green, blue )
```



参数：



```plain
red：integer类型，指定颜色中的红色分量强度，有效值在0到255之间

green：integer类型，指定颜色中的绿色分量强度，有效值在0到255之间

blue：integer类型，指定颜色中的蓝色分量强度，有效值在0到255之间
```



返回值：



```plain
返回值：Long。
函数执行成功时返回由指定分量确定的颜色，用长整数表示。
发生错误时返回-1。如果任何参数的值为NULL，RGB()函数返回NULL。
```



用法



```plain
RGB()函数使用下述公式计算表示颜色的长整数：65536 * Blue+ 256 * Green+ Red

其中，Blue代表蓝色分量，Green代表绿色分量，Red代表红色分量。

各分量中，数值越小，亮度越低，数值越大，亮度越高。

例如，RGB ( 0, 0, 0 )为黑色（亮度最低），RGB ( 255, 255,255 )为白色（亮度最高）。
```



（9）、SetNull



功能：



```plain
将指定变量的值设置为NULL。这里的变量可以是除数组、结构、自动实例化对象之外的任何数据类型。
```



语法：



```plain
SetNull ( anyvariable )
```



参数：



```plain
anyvariable：要将其值设置为NULL的变量
```



返回值：



```plain
返回值：Integer。
函数执行成功时返回1，发生错误时返回-1。
如果任何参数的值为NULL，SetNull()函数返回NULL。
```



用法



```plain
PowerBuilder应用程序在说明变量时，并不自动地将其初值设置为NULL，而是根据类型的不同而设置不同的初值，比如，数值类型的变量自动初始化为0，字符串型变量自动初始化为空字符串（""）。

因此，如果需要将某个变量的值设置为NULL，就需要使用SetNull()函数来完成任务了。

一般来说，NULL值往往应用在数据库值未确定的列上。
```



（10）、SetPointer



功能：



```plain
设置鼠标指针。
```



语法：



```plain
SetPointer ( type )
```



参数：



```plain
type：Pointer枚举类型，指明要设置为哪种鼠标指针
```



返回值：



```plain
返回值：Pointer。
返回更换前的鼠标指针，以便于应用程序恢复原有指针。
如果参数type的值为NULL，SetPointer()函数返回NULL。
用法type参数的可能取值为：Arrow!、Cross!、Beam!、HourGlass!、SizeNS!、SizeNESW!、SizeWE!、SizeNWSE!、UpArrow!。
```



（11）、SignalError



功能：



```plain
以编程方式触发应用对象的SystemError事件。
```



语法：



```plain
SignalError ( { number }, { text } )
```



参数：



```plain
number：integer类型，可选项，指定出错编号，该编号将保存到Error对象的number属性中

text：string类型，可选项，指定出错信息，该信息将保存到Error对象的text属性中
```



返回值：



```plain
返回值：Integer。函数执行成功时返回1，发生错误时返回-1。
```



用法



```plain
SignalError()函数通常用于测试应用程序的出错处理代码，它以人工方式产生错误，以此模拟应用程序运行过程中可能出现的错误。

我们知道，应用程序本身产生错误的条件往往不容易在测试时遇到。

当应用程序使用PopulateError()函数定制了Error对象后，可以以不带参数的方式调用SignalError()函数，由该函数触发应用对象的SystemError事件。

如果我们在调用SignalError()函数时指定了参数number和text，那么SignalError()函数将根据上下文填充Error对象的所有属性，然后触发应用对象的SystemError事件。

如果应用程序没有对应用对象的SystemError事件编写事件处理程序，那么SignalError()函数什么也不做。
```



（12）、UnitsToPixels



功能：



```plain
将PowerBuilder单位（PBU）转换为像素
```



语法：



```plain
UnitsToPixels ( units, type )
```



参数：



```plain
units：integer类型，指定要转换为像素的PowerBuilder单位（PBU）数
type：ConvertType枚举类型，指定按哪个方向进行转换。有效取值为：XUnitsToPixels! - 按水平方向转换PBU；YUnitsToPixels! - 按垂直方向转换PBU
```



返回值：



```plain
返回值：Integer。

函数执行成功时返回units参数指定PBU数按指定方向转换成的像素数，发生错误时返回-1。如果任何参数的值为NULL，UnitsToPixels()函数返回NULL。
```



用法



```plain
窗口中水平方向和垂直方向相同的像素数表示的距离并不相同。
如果你使用水平方向和垂直方向相同的像素数绘制一个方框，那么你会看到，该方框不是正方形而是个矩形，而使用PBU计量的相同单位数将绘出正方形。
因此，在进行单位转换时，需要指明按那么方向进行转换。
```