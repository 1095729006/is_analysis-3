
|学号|班级|姓名|
|:-------:|:-------------: | :----------:|
|201510414307|软件(本)15-3|李龙飞|

# 实验四：图书管理系统的顺序图

### 1借书用例

### 1.1借书用例PlantUML源代码
 <pre> 
@startuml
actor manager

manager->图书管理系统:login()
activate 图书管理系统

图书管理系统->借书界面:menu()
deactivate 图书管理系统

借书界面->borrow:borrow()
activate 借书界面
deactivate 借书界面
actor reader
borrow->reader:getredersinfor()获取读者信息
activate borrow
activate reader

reader->borrow:returnvalid()返回是否符合借书条件
deactivate reader
borrow->item:getitem()获取书目信息
deactivate borrow

borrow->reseration:checkreseration()查看图书是否被预定
activate reseration
reseration->borrow :getnoreseration()
activate borrow
deactivate reseration

borrow->books:create(borrowInfor)
activate books
deactivate books
deactivate borrow
borrow->借书界面:借书完成
@enduml
 </pre>


### 1.2借书用例顺序图
![borrow](borrow.png)


### 1.3借书用例图说明
<pre>
login()登陆系统，borrow()读者借书，gettitle（）获取书目信息，getreaders()获取读者信息，是否满足借书要求
getreservation()检查书记是否借出，checkreseration()图书是否被预定，create(borrowInfor)建立借书信息
读者将书记给管理员登记，满足借书条件则借出成功
</pre>


### 2还书用例

### 2.1还书用例PlantUML源代码
<pre>
@startuml
actor reader
actor manager

reader->manager:提交
activate reader
manager->图书管理系统:login()
activate manager

deactivate reader
图书管理系统->还书界面:menu()
activate 还书界面
deactivate manager
deactivate 还书界面

还书界面->borrowInfor:输入编码或扫码
activate 还书界面
activate borrowInfor
deactivate 还书界面
 deactivate borrowInfor

borrowInfor->item:getitem()
activate borrowInfor
activate item
deactivate borrowInfor
deactivate item

item->还书界面:confirm
activate 还书界面
activate item
deactivate 还书界面
deactivate item

还书界面->item:update()
activate 还书界面
activate item
deactivate 还书界面
deactivate item

还书界面->borrow:update()
activate 还书界面
activate borrow
deactivate 还书界面
deactivate borrow

borrow->还书界面:还书完成
activate borrow
activate 还书界面
@enduml
</pre>


### 2.2还书用例顺序图
![borrow](return.png)


### 2.3还用例图说明
login()登陆系统，getitem()取得书条目信息，update()更新书籍信息何借阅信息
还书步骤：读者将书籍给管理员登记，查看图书完好后管理员通过扫码或输入编码进
行登记，跟新相关信息，还书成功


### 3罚款用例

### 3.1罚款用例顺序图PlantUML源码
<pre>
@startuml
actor manager

manager->borrowInfor:查询显示
activate manager
activate borrowInfor
deactivate manager
deactivate borrowInfor

borrowInfor->borrow:显示超时未还书籍
activate borrow
activate borrowInfor
deactivate borrow
deactivate borrowInfor

actor reader
borrowInfor->reader:提示罚款金额
activate reader
activate borrowInfor
deactivate reader
deactivate borrowInfor

reader->manager:提交罚款
activate reader
activate manager
deactivate reader
deactivate manager

manager->borrowInfor:update()更新信息
activate manager
activate borrowInfor
deactivate reader
deactivate manager

manager->borrow:update()更新信息
activate manager
activate borrow
deactivate manager
deactivate borrow
@enduml
</pre>


### 3.2罚款用例顺序图
![fine](fine.png)


###3.3罚款用例顺序图说明
管理员扫描书籍，发现超时记录，则按罚款规则进行计费，读者需要交付罚款，更新借阅信息

### 4游客注册登陆用例
### 4.1游客注册登录用例PlaneUML源码
<pre>
@startuml

actor visitor
visitor->注册界面:访问
activate visitor
activate 注册界面
deactivate visitor

注册界面->登陆界面:regist()
activate 登陆界面
deactivate 注册界面

登陆界面->图书管理系统:login()
activate 图书管理系统
deactivate 图书管理系统
deactivate 登陆界面
@enduml
</pre>
###4.2用例顺序图
![regist](regist.png)
###4.3用例顺序图说明
<pre>未注册用户无法进新借书操作，通过注册可以进入图书管理系统，</pre>

### 5.预定图书用例

### 5.1预定图书用例顺序图PlaneUML源码
<pre>
@startuml

actor reader
reader->图书管理系统:login()
activate 图书管理系统

图书管理系统->预定图书界面:menu()
activate 预定图书界面
deactivate 图书管理系统

预定图书界面->reseration:checkreseration()
activate reseration
reseration->预定图书界面:getinfor()
deactivate 预定图书界面
deactivate reseration

预定图书界面->books:create(reserationInfor)
activate 预定图书界面
activate books
books->预定图书界面:预定成功
deactivate 预定图书界面
deactivate books

@enduml
</pre>
###  5.2预定图书用例顺序图
![reserve](reserve.png)

### 5.3 预定图书用例顺序图说明
<pre>预定图书为reader客户端的操作 可不经过图书管理员，login()登陆验证，
checkreseration()查看图书是否已被预定，getinfor()显示图书信息，
create(reaseration)创建图书预定</pre>

### 6取消预定图书用例

### 6.1取消预定图书顺序图planeUML源码
<pre>
@startuml

actor reader

reader->图书管理系统:login()
activate 图书管理系统

图书管理系统->取消预定界面:menu()
activate 取消预定界面
deactivate 图书管理系统

取消预定界面->reseration:查看预定信息
deactivate 取消预定界面
activate reseration

reseration->取消预定界面:返回取消预定的信息
activate 取消预定界面
deactivate reseration
deactivate 取消预定界面

取消预定界面->books:update()
activate 取消预定界面
activate books
books->取消预定界面:取消预约成功
deactivate 取消预定界面
deactivate books


@enduml
</pre>
### 6.2取消预定图书顺序图p
![disreseration](disreseration.png)
### 6.3取消图书预定顺序图说明
<pre>取消图书预定为reader客户端的操作，login()登陆系统，menu()菜单选项
查看预订信息，取消预定的图书，update()更新图书信息</pre>

### 7.编辑图书信息用例
### 7.1编辑图书信息用例顺序图planeUML源码
<pre>

@startuml
actor reader

reader->图书管理系统:login()
activate reader
deactivate reader
图书管理系统->查看图书信息界面:menu()
activate 图书管理系统
activate 查看图书信息界面
deactivate 图书管理系统
deactivate 查看图书信息界面

查看图书信息界面->books:lookinfor(bookid)
activate 查看图书信息界面
activate books
deactivate 查看图书信息界面
deactivate books

books->查看图书信息界面:返回图书信息
activate books
activate 查看图书信息界面
deactivate books
deactivate 查看图书信息界面

查看图书信息界面->修改图书信息界面:查找图书id或书名
activate 查看图书信息界面
activate 修改图书信息界面
deactivate 查看图书信息界面
deactivate 修改图书信息界面

修改图书信息界面->books:update()
activate 修改图书信息界面
activate books
deactivate 修改图书信息界面
deactivate books

books->查看图书信息界面:返回
activate books
activate 查看图书信息界面
deactivate books
deactivate 查看图书信息界面

@enduml
</pre>
### 7.2 编辑图书信息顺序图

![editbook](editbook.png)
### 7.3编辑图书信息顺序图说明
<pre>
该操作为管理员操作，login()登陆系统，menu()菜单选择，lookinfor(bookid)
查找图书，update()更新图书信息
</pre>

