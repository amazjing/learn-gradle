# learn_gradle
gradle视频地址：https://www.bilibili.com/video/BV1yT41137Y7?spm_id_from=333.337.search-card.all.click&vd_source=ee45326176d5e9ebbb3efde5d57924f2



## 1. Gradle 入门

### 1.1 Gradle 简介

Gradle 是一款 Google 推出的**基于 JVM、**通用灵活的**项目构建工具，**支持 Maven，JCenter 多种第三方仓库;支持传递性 依赖管理、废弃了繁杂的 xml 文件，转而使用**简洁的**、**支持多种语言**(例如：java、groovy 等)的 **build 脚本文件**。 官网地址: https://gradle.org/

![image-20220905201542833](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905201542833.png)

**学习 Gradle 的原因：**

1. 目前已经有相当一部分公司在逐渐使用Gradle作为项目构建工具了。 
2. 作为Java开发程序员,如果想下载Spring、SpringBoot等Spring家族的源码，基本上基于Gradle构建的。

**总之，虽然目前市面上常见的项目构建工具有 Ant、Maven、Gradle，主流还是 Maven，但是未来趋势 Gradle**。



### 1.2 常见的项目构建工具

Ant: 2000 年 Apache 推出的纯 Java 编写构建工具，通过 xml[build.xml]文件管理项目

- 优点：使用灵活，速度快(快于 gradle 和 maven)， 
- 缺点：Ant 没有强加任何编码约定的项目目录结构,开发人员需编写繁杂 XML 文件构建指令,对开发人员是一个挑战。

 Maven: 2004 年 Apache 组织推出的再次使用 xml 文件[pom.xml]管理项目的构建工具。

- 优点: 遵循一套约定大于配置的项目目录结构，使用统一的 GAV 坐标进行依赖管理,**侧重于包管理**。 
- 缺点：项目构建过程僵化,配置文件编写不够灵活、不方便自定义组件,构建速度慢于 gradle。

Gradle: 2012 年 Google 推出的基于 Groovy 语言的全新项目构建工具，集合了 Ant 和 Maven 各自的优势。

- 优点：集 Ant 脚本的灵活性+Maven 约定大于配置的项目目录优势,支持多种远程仓库和插件**,侧重于****大项目构建**。 
- 缺点：学习成本高、资料少、脚本灵活、版本兼容性差等。

![image-20220905201758857](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905201758857.png)



### 1.3 Gradle安装

#### 1.3.1 Gradle 安装说明

SpringBoot 官方文档明确指出,目前 SpringBoot 的 Gradle 插件需要 gradle6.8 版本及以上，所以我们这里选择 7.x 版本。 

![image-20220905201902679](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905201902679.png)

其中 SpringBoot 与 Gradle 存在版本兼容问题，Gradle 与 Idea 也存在兼容问题，所以考虑到 java 程序员会使用 SpringBoot， 所以要选择 6.8 版本及高于 6.8 版本的 Gradle,那么相应的 idea 版本也要升级,不能太老哦。 

**具体参考文档:**https://docs.spring.io/spring-boot/docs/2.5.0/gradle-plugin/reference/htmlsingle/#getting-started 

**查看当前IDEA支持的gradle版本**：

找到自己的IDEA安装目录，例如：D:\Java\IDEA\IntelliJ IDEA 2021.3.3\plugins\gradle\lib，这里的对应的就是当前版本的gradle版本





#### 1.3.2 安装 JDK

要求 Jdk 为 1.8 或者 1.8 版本以上。【自行百度安装】



#### 1.3.3 下载并解压到指定目录

下载地址：https://gradle.org/install/

![image-20220905203346819](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905203346819.png)



我的IDEA是2021.3的版本的，对应的gradle版本是7.1.1，所以这里下载的是7.1.1版本的gradle

![image-20220905203919900](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905203919900.png)





下载之后，解压到指定目录：D:\Java\gradle\gradle-7.1.1



#### 1.3.4 配置环境变量

在系统环境变量中，新建`GRADLE_HOME`

![image-20220905204552201](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905204552201.png)

在Path中增加变量

![image-20220905204804606](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905204804606.png)

**特别注意**：这里我们接着再配置一个**GRALE_USER_HOME环境变量**:

![image-20220905205447390](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905205447390.png)

**GRALE_USER_HOME** **相当于配置** **Gradle** **本地仓库位置和** **Gradle Wrapper** **缓存目录。** 



**执行命令验证是否配置成功：**

```
gradle -v
```

![image-20220905205017185](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905205017185.png)





#### 1.3.5 Gradle 项目目录结构

Gradle 项目默认目录结构和 Maven 项目的目录结构一致,都是基于约定大于配置【Convention Over Configuration】。 其完整项目目录结构如下所示：

![image-20220905205740231](http://typora-imagelist.oss-cn-qingdao.aliyuncs.com/image-20220905205740231.png)



**小提示：**

1. 只有war工程才有webapp目录，对于普通的jar工程并没有webapp目录 

2. gradlew与gradlew.bat执行的指定wrapper版本中的gradle指令,不是本地安装的gradle指令哦。

