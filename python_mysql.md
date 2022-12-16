
# 方案1: mysql 官方
MySQL Connector/Python Developer
mysql connector python 

#### msi安装包是一种方案
不含c扩展


#### 二进制包是另一个中方案
包含c扩展
c扩展和纯python实现是两种二进制分发的
c扩展实现里面包名含cext
c扩展的二进制版本会和本地已经安装的c客户端库(mysql server安装包内)链接
对于版本还没有静态链接的, 你必须先安装mysql server


#### 1. 安装这个
https://dev.mysql.com/downloads/connector/python/
安装位置 
J:\Program Files (x86)\MySQL\MySQL Connector Python 8.0\

#### 2. pip 安装包
pip install mysql-connector-python

安装这个
https://cdn.mysql.com//Downloads/Connector-C++/mysql-connector-c++-8.0.31-winx64.msi

安装这个
https://cdn.mysql.com//Downloads/Connector-Python/mysql-connector-python-8.0.31-windows-x86-64bit.msi

PyMySQL
mysqlclient
mysql
mysql-connctor
mysql-connector-python

