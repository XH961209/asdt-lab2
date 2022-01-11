# asdt-lab2
高级软件开发技术实验二作业
## 项目介绍  
[asdt-lab2](https://github.com/XH961209/asdt-lab2)包含三个子项目(EmployeeManagement, UserManagement, TaskManagement)，其github链接分别为  
asdt-lab2:    
EmployeeManagement: https://github.com/XH961209/EmployeeManagement   
UserManagement: https://github.com/XH961209/UserManagement   
TaskManagement: https://github.com/XH961209/TaskManagement   
三个子项目分别是员工管理系统、用户管理系统和任务管理系统，本项目主要包含一个将所有子系统进行容器化的docker-compose.yml文件  
## 系统容器化运行
### 运行环境
安装有Docker和Git的任意环境
### 容器化运行
首先同步各子模块的最新代码:  
`git submodule update --init`  
然后启动各容器:  
`docker-compose up`  
通过`docker ps`可以看到，一共启动了6个容器，关于这些容器的说明如下表所示:  

