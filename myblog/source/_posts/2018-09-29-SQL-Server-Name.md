---
title: SQL Server 服务器名
date: 2018-09-29 09:09:16
tags: SQL
categories:
---
在SQL Server 2005/2008安装后，即记录了计算机名做为 "sql server服务器名".
当修改计算机名时， 需要修改sql server中对应的服务器名， 否则将影响“发布/订阅”，“镜像集群”等功能。

-- 检查SQL Server中的“服务器名[/命名实例名]”, 和当前真实的“计算机名[/命名实例名]”。如果修改了计算机名，则这两者即会不一致。

select @@serverName,  serverproperty('serverName') 
-- 将"服务器名", 修改为正确的计算机名
EXEC sp_dropserver '服务器名[/命名实例名]';           -- 即旧的计算机名
GO
EXEC sp_addserver '计算机名[/命名实例名]', 'local'; -- 即新的计算机名
go
-- 重启SQL Server