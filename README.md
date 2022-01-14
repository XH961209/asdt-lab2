# asdt-lab2
高级软件开发技术实验二作业
## 项目介绍  
[asdt-lab2](https://github.com/XH961209/asdt-lab2) 包含三个子项目 [EmployeeManagement](https://github.com/XH961209/EmployeeManagement), [UserManagement](https://github.com/XH961209/UserManagement) 和 [TaskManagement](https://github.com/XH961209/TaskManagement)  
三个子项目分别是员工管理系统、用户管理系统和任务管理系统，asdt-lab2主要包含一个将所有子系统进行容器化的docker-compose.yml文件  
## 系统容器化运行
### 运行环境
安装有Docker和Git的任意环境
### 容器化运行
首先同步各子模块的最新代码:  
`git submodule update --init`  
然后启动各容器:  
`docker-compose up`  
启动后，当前shell窗口将显示各容器的标准输出，需打开一个新的shell以执行下述操作  
通过`docker ps`可以看到，一共启动了6个容器，关于这些容器的说明如下表  
|容器名|作用|备注|
|:---:|---|---|
|asdt-lab2_kafka_1|kafka容器，其中运行了kafka server||
|asdt-lab2_zookeeper_1|zookeeper容器，其中运行了zookeeper server|zookeeper主要用来存放kafka产生的一些元数据，可不必关注|
|asdt-lab2_employee_1|员工管理系统容器，其中运行了员工管理系统，包括员工管理系统的redis数据库||
|asdt-lab2_user_1|用户管理系统容器，其中运行了用户管理系统，包括用户管理系统的redis数据库||
|asdt-lab2_task_1|任务管理系统容器，其中运行了任务管理系统，包括任务管理系统的redis数据库||
|asdt-lab2_management_1|系统管理容器，在该容器内通过curl调用各系统的rest api、查看各系统的redis数据库、查看kafka||
### 通过curl调用各系统的rest api
首先进入asdt-lab2_management_1容器:  
`docker exec -it asdt-lab2_management_1 /bin/bash`  
在该容器内进行以下调用:  
|系统功能|调用方法|参数含义|
|:----:|-------|------|
|注册新员工|curl -i -H "Content-Type: application/json" -X POST -d '{"number":"NUMBER","name":"NAME","department":"DEPARTMENT","email":"EMAIL>"}' http://employee_server:5000/employee/api/register|NUMBER: 工号; NAME: 姓名; DEPARTMENT: 部门; EMAIL: 邮箱|
|登录用户系统|curl -i -H "Content-Type: application/json" -X POST -d '{"name":"NAME", "password":"PASSWD"}' http://user_server:5000/user/api/login|NAME: 用户名, 是注册员工时的工号; PASSWD: 密码, 注册时系统会返回一个初始密码|
|获取任务系统报表|curl -i -H "Content-Type: application/json" -X POST http://task_server:5000/task/api/get_report||
|更新密码|curl -i -H "Content-Type: application/json" -X POST -d '{"name":"NAME", "old_password":"OLD_PASSWD", "new_password":"NEW_PASSWD"}' http://user_server:5000/user/api/update_password|NAME: 用户名, 指工号; OLD_PASSWD: 旧密码; NEW_PASSWD: 新密码|
|更换部门|curl -i -H "Content-Type: application/json" -X POST -d '{"name":"NAME", "password": "PASSWD", "department":"DEPARTMENT"}' http://user_server:5000/user/api/reset_department|NAME: 用户名, 指工号; PASSWD: 密码; DEPARTMENT: 要更换的部门|
### 查看各系统redis数据库内容
首先进入asdt-lab2_management_1容器:  
`docker exec -it asdt-lab2_management_1 /bin/bash`  
进入某系统redis数据库cli:  
`redis-cli -h SYSTEM_NAME`  
SYSTEM_NAME是系统名，员工系统、用户系统和任务系统的SYSTEM_NAME分别是employee_server, user_server和task_server  
### 查看kafka内容
当前asdt-lab2_management_1容器中还未安装java，无法访问kafka，待完善
