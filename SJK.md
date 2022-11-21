## 1、SqlServer

### （1）、PB连接SqlServer

```sql
string ls_inifile 
ls_inifile = getcurrentdirectory()  + '\pb.ini'

sqlca.dbms = profilestring ( ls_inifile, "database",  "dbms", "mss microsoft sql server")
sqlca.database =  profilestring ( ls_inifile, "database", "database", "")
sqlca.logpass = profilestring ( ls_inifile, "database",  "logpassword", "")
sqlca.servername = profilestring(  ls_inifile, "database", "servername", "")
sqlca.logid =  profilestring ( ls_inifile, "database", "logid", "")
sqlca.autocommit = false
sqlca.dbparm = ""

connect using sqlca;

if  sqlca.sqlcode <> 0 then
 messagebox("数据库连接失败","请与管理员联系。错误号:" + string(sqlca.sqlcode) + "~r~n错误原因:" + sqlca.sqlerrtext)
 return
else
 messagebox("数据库连接成功","现在进入系统...  ...")
end if
```

## 2、mdb

### （1）、直接连接

```sql
string ls_mdbfile
ls_mdbfile = getcurrentdirectory() + '\test.mdb'
sqlmdb = create transaction
sqlmdb.dbms = "odbc"
sqlmdb.autocommit = false
sqlmdb.dbparm = "connectstring='driver=microsoft access  driver (*.mdb);dbq=" + ls_mdbfile + "'"
connect using sqlmdb;
if  sqlmdb.sqlcode <> 0 then
 messagebox("数据库连接失败","请与管理员联系。错误号:" + string(sqlmdb.sqlcode) + "~r~n错误原因:" + sqlmdb.sqlerrtext)
 return
else
 messagebox("数据库连接成功","现在进入系统...  ...")
end if
```

### （2）、带账户密码的连接

```sql
string ls_mdbfile
ls_mdbfile = getcurrentdirectory() + '\test.mdb'
sqlmdb = create transaction
sqlmdb.dbms = "odbc"
sqlmdb.autocommit = false
sqlmdb.dbparm = "connectstring='driver=microsoft access  driver (*.mdb);uid=" + account + ";pwd=" + password + ";dbq=" + ls_mdbfile+  "'"
connect using sqlmdb;
if  sqlmdb.sqlcode <> 0 then
 messagebox("数据库连接失败","请与管理员联系。错误号:" + string(sqlmdb.sqlcode) + "~r~n错误原因:" + sqlmdb.sqlerrtext)
 return
else
 messagebox("数据库连接成功","现在进入系统...  ...")
end if
```