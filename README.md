# mongodb-
删除一个集合里的数据
db.集合名.remove({})
删除一个集合
db.集合名.drop()
添加一条记录
db. 集合名 .insert({“name”:”jim”})
新建一条记录
db.c1.save({name:"bob",age:19,sex:"girl"})
删除一个库（得在你需要删除的库下进行）
db.dropDatabase()
数据恢复与备份
• 语法格式
– mongorestore --host IP 地址 --port 端口 -d 数据库名 [ -c 集合名 ] 备份目录名
//备份
[root@host50 ~]# mongodump --host 192.168.4.50 --port 27050 -d studb -c c3 -o /qq      //-o 指定路径名

[root@host50 ~]# mongorestore --host 192.168.4.50 --port 27050 -d studb -c c3 /qq/studb/c3.bson    //恢复
• 查看 bson 文件内容
#bsondump ./dump/bbs/t1.bson
语法格式 3              数据导出
#mongoexport [ --host IP 地址 --port 端口 ]-d 库名 -c 集合名 -q  ‘{ 条件 }’ –f 字段列表  --type=json> 目录名 / 文件名 .json

[root@host50 ~]# mongoexport --host 192.168.4.50 --port 27050 -d studb -c c1 --type=json >/mongodb/c1.mongo


语法格式 1         数据导入
– #mongoimport –host IP 地址 – port 端口  -d 库名 – c 集合名  --type=json  目录名/ 文件名 .json
• 语法格式 2
– #mongoimport –host IP 地址 – port 端口 -d 库名 – c 集合名  --type=csv --headerline [--drop] 目录名/ 文件名 .c
sv
注意:导入数据时库和集合不存在时,会创建库和集合后导入数据反之以追加的方式导入数据到集合里,使用— drop 选项可以删除原有数据后导入新数据 --headerline 忽略标题

[root@host50 ~]# mongoexport  --host 192.168.4.50 --port 27050 -d studb -c c1 -f _id,name --type=csv >/mongodb/c1.csv

csv类型必须指定 -f 字段列表

建库
 db.c2.save({name:"tom",password:"x",uid:8888,gid:9999,comment:"teacher",homedir:"/home/tom",shell:"/bin/bash"})
导出
[root@host50 ~]# mongoexport --host 192.168.4.50 --port 27050 -d studb -c c2 -f name,password,uid,gid,comment,homedir,shell --type=csv > /mongodb/c3.csv

[root@host50 mongodb]# cp /etc/passwd ./
[root@host50 mongodb]# ls
a.json  c1.csv  c3.csv  ca.csv  passwd
[root@host50 mongodb]# sed -i '$r passwd' c3.csv
[root@host50 mongodb]# vim c3.csv 
[root@host50 mongodb]# sed -i 's/:/,/g' c3.csv 

[root@host50 mongodb]# mongoimport --host 192.168.4.50 --port 27050 -d studb -c c3 --headerline --drop --type=csv /mongodb/c3.csv 
