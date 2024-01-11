# Maven的使用

## Maven介绍

Maven是一个Java依赖管理工具，是一个Java构建工具为什么要使用Maven：之前在学习Javaweb的时候使用jar包都需要手动的导入，这很麻烦，而且jar包之间的依赖性很难管理，在使用Maven之后可以很好的进行jar包管理，不在需要那么麻烦的jar包管理。

在使用jar包的时候直接书写一段配置就可以将所需要的jar包下载下来，并且如果jar包之间存在依赖关系，那么Maven也会自动的下载所有的jar包

在可视化界面可以直接使用idea进行打包部署，但是在服务器环境下需要使用Maven进行打包部署

## 工作原理

pom.xml：是Maven的核心配置文件，

denpendency：依赖管理模型

plug-in：Maven的插件

## 安装和配置

...

## Maven工程的gavp属性

这四个标识为了给Java工程一个标识：
g：com.[公司].[业务线].[子业务线]，最多四级

artifactID：产品线

v：主版本.次版本.修订号

主：当做了不兼容的api修改，或者增加了能改变产品方向的新功能

p：设置打包方式

