# 1. 专业开发服务

应用构建平台专业版面向的用户群体目前主要是企业租户、生态isv、原厂领域开发团队、专属化项目开发团队，开发场景的诉求均不相同。企业租户只关心自己租户的开发、实施、验证、上线使用；生态isv关心为哪些企业进行定制开发、如何研发生态应用上架到云市场交易；原厂领域开发团队，关心SaaS服务新应用开发、新特性升级、相关缺陷修复，关心开发产出SaaS服务可以支持专属化；专属化项目开发团队，关心基于安装到项目环境上的服务进行项目个性化的开发、验证、上线。

 专业版除了涵盖标准版的全部设计和脚本能力之外，还可以支持开发者自建应用引擎来实现本地源码开发、独立运维部署等企业云服务高级定制能力，专业版的关键特性如下：

 1、涵盖标准版的全部配置、设计和在线脚本能力

 2、脚手架下载、本地源码开发调试

 3、无服务器模式，只需要开发自己的代码，一键部署，无需关心环境搭建和运维

 4、通过数据迁移和流水线上线流程实现多环境下的开发、验证、集成、发布上线的持续交付过程

 5、支持构建产出的应用快速上载到云市场上市交易，实现生态共建

 6、支持开放集成能力的快速连接

 支持自定义组件、函数类型，开发、上传、发布到设计器中使用。

# 2. 核心概念

应用引擎是应用构建、使用的运行时支撑。它开箱即用，开发者只需要关心基于引擎的脚手架快速开发实现自己的业务逻辑和特性，不需关心多环境的搭建、运维，代码部署、多环境间的数据升迁过程均可在应用引擎下快速操作完成。

为标准服务提供隐形的公共引擎，为专业开发服务提供开箱即用的高级定制开发全生命周期管理。

![](/assets/image003.jpg)

专业版中的核心概念是应用引擎，如上高级定制特性便主要是通过自建应用引擎来实现的，通过应用引擎来融合技术中台、开放平台、云市场和应用构建的能力为开发者提供一站式的持续交付体验。

➢ 公共引擎：

用户无需关心代码和部署运维，为非专业开发人员使用，为应用构建标准服务提供默认支撑；应用构建过程统一都是由应用构建平台的公共引擎（公共引擎提供安全的多租户的模型驱动运行时）支撑的，在公共引擎上运行的应用不支持本地开发访问。当开发者有本地开发、独立运维的诉求时，可选择将公共引擎下的应用迁移到自建引擎下实现进一步的定制开发和部署运维。如下：

➢ 自建引擎：
与技术中台的容器、微服务等有机融合，为专业开发人员提供开发运维一体化的全生命周期管理能力，让对性能和安全敏感的企业应用有了保障；

✓ mdd源码扩展开发脚手架下载，支持本地开发调试；

✓ 融合技术中台能力，支持运行资源申请、分配、CICD、微服务注册及治理；

✓ 引擎成员管理，限定引擎的管理和访问权限；

✓ 基于自建引擎的应用构建，支持自定义和管理持久化数据建模的数据表、支持页面模板扩展、自定义页面开发等高级定制扩展；

# 3. 应用引擎构建

 专业开发服务首先要新建应用引擎，在下面

## 3.1 新建引擎

1、 填写编码【要求4位以上】、名称，其余属性先不填写

![](/assets/image005.jpg)

点击保存，引擎初步建立完毕，默认生成的脚手架已经和业务中台对接。

目前提供的专属化版本中，还没有和技术中台对接，所以暂未提供脚手架自动与技术中台流水线对接部署等功能，需要用户自行下载脚手架部署应用引擎的运行环境。

## 3.2 下载脚手架

点击进入引擎详情,点击下载脚手架.

![](/assets/image007.jpg)

完成后解压

![](/assets/image009.jpg)

### 3.3.1 后端项目配置

#### 3.3.1.1 初始化数据库

如果需要用报表和mdd一致，如果没要求可以自建数据库；

需要在库表表里新建db，db的名字必须是：引擎code 加上_db，执行建库初始化脚本，位置在sql/init.sql

![](/assets/image011.jpg)

#### 3.3.1.2 修改配置文件

打开be目录下bootstrap工程的pom.xml文件

1) 修改redisHost变量，在技术中台-应用管理搜索mdd，找到redis配置文件mdd_redis.properties找到redis 
ip/port，copy到redis；

![](/assets/image013.jpg)

2) zk同上步骤一致，application.properties，找到zklock.url

3) db信息在mdd-db.properties

最终配置完成后效果如下图

![](/assets/image015.jpg)

开发环境替换配置文件后，使用mvn package install -Dmaven.test.skip=true -P dev,linux，打出war包，将配置信息写入配置文件。打包完成后在target下找到ROOT.war，这个war包可以部署了。

## 3.4 前后端项目部署

此时我们需要将脚手架部署到服务器上，这样我们在YonBuilder和业务中台的运行态环境才可以使用，此时的项目部署有以下多种场景提供给客户使用。

下面有开发的三种场景：

➢ 流水线部署：直接使用技术中台部署前后端流水线，执行流水线成功后即可。

➢ 如果本机启动调试则可以直接使用MDFApplication启动如果需要部署，则部署到tomcat中，启用后端服务即可。

➢ 服务器部署：如果多人使用此项目开发，则需要一台服务器【可以与业务中台以及YonBuilder网络连通的】，则我们可以把前后端项目打包，把war包部署到tomcat，

### 3.4.1 流水线部署

流水线部署的步骤为：

1、 流水线部署后端项目，保证成功运行；

2、 后端服务配置到前端项目配置文件中，流水线部署前端项目；

3、 开发者开发机器配置hosts；

4、 配置应用引擎界面；

#### 3.4.1.1 部署后端服务

可以直接把代码提交到git，或者上传war包部署，后端打包的Root.war可以直接部署。这里我们先部署后端服务。获取后端服务的地址；

1、 创建流水线

![](/assets/image017.jpg)

2、 点击下一步上传war包，指定资源池

![](/assets/image019.jpg)

➢ 勾选启用微服务

➢ 勾掉创建新应用到根目录

➢ 其他选项使用默认值即可

3、 继续其他配置，完成后效果如下图

![](/assets/image021.jpg)

此时在应用管理

![](/assets/image023.jpg)

 获取后端服务域名地址：traindemo0820-be.dev.pxapp.yyuap.com

#### 3.4.1.2 部署前端服务

1、 修改前端配置文件env.json

修改default和prod的base_url和print_url地址为后端域名

![](/assets/image025.jpg)

2、 压缩前端项目文件夹

将前端项目文件夹直接打包为zip文件

3、 新建流水线

选择node应用，上传应用包

![](/assets/image027.jpg)

启动命令输入 node bin.js，执行npm install要取消勾选

要添加环境变量

![](/assets/image029.jpg)

其余属性按照默认即可。

流水线完成效果

![](/assets/image031.jpg)

在应用管理下看到前后端应用，状态为“健康”。说明此时的前后端应用已经可以使用了。

![](/assets/image034.jpg)

#### 3.4.1.3 配置hosts

如果开发者需要连接此引擎，则需要在本机配置hosts，如上述配置，需要配置host为

  `#5.0.1 环境 IP：技术中台地址 前端域名`

172.20.48.26 traindemo0820.dev.pxapp.yyuap.com

此时，可以访问前端域名看是否可以成功访问。

![](/assets/image036.jpg)

#### 3.4.1.4 填写应用访问地址

在应用引擎填写应用访问地址，点击修改

填写前端域名：http://traindemo0820.dev.pxapp.yyuap.com

后端域名：http://traindemo0820-be.dev.pxapp.yyuap.com

访问地址：http://traindemo0820.dev.pxapp.yyuap.com

![](/assets/image038.jpg)

点击保存即可。

### 3.4.2 开发者本机部署

另外一种场景是开发者本身不配置服务器，直接从本地启动，进行本地调试。也可以直接通过启动前后端项目的方式直接使用。但是要保证本机可以和服务器网络访问联通。

#### 3.4.2.1 启动前端工程

1、 修改配置文件

前端代码evn.json，修改base_url的值调整为【本机IP:8080】，如：

"base_url":"http://10.2.108.44:8080",

2、 在前端开发工具运行执行 node bin.js启动前端工程

#### 3.4.2.2 启用后端工程

在后端开发工具上启动MDFApplication

![](/assets/image041.jpg)

#### 3.4.2.3 配置Hosts

关键说明：

➢ 本机开发环境，ip需要能被服务器回调到，用友网线inode获得ip；

➢ 自己给该引擎起的域名的名称，后面2段需要与业务中台的后面2段的域名保持一致；

如：

10.2.108.44 traindemo.ys0807.com

#### 3.4.2.4 填写应用访问地址

在上述章节，前后端服务器上的后端服务已经成功启动，表示应用引擎所对应的运行环境已经启动成功。测试验证通过之后需要修改引擎的配置。

在应用引擎界面，点击修改。示例如上述启动后端服务器的IP为：10.2.133.43

前端访问地址【服务器】:3003，则填写为http://10.2.133.43:3003

填写后端地址：http://ip【服务器】:8080/，即为http://10.2.133.43:8080；

保存成功后，再在引擎上把访问地址改成域名，域名标准版地址后两位必须一致 XXX.yyuap.com

则修改配置为：

![](/assets/image044.jpg)

最后填写访问地址默认为前端地址，最后效果为：

![](/assets/image046.jpg)

配置完成后就可以在当前应用引擎上添加应用了。

### 3.4.3 服务器部署

1、 前端项目打包；

使用npm run build打包前端代码；

2、 后端项目打包；

使用maven clean package做后端项目打包，打包完成后为XXX.war；

3、 配置tomcat

把war包发布到tomcat的webapps文件夹下，可以把前端打包的文件夹放置到设定文件夹下。启动tomcat

4、 如有需要可以配置nginx

在服务器本机上配置hosts，指定访问的域名，注意后两位必须和业务中台后两位域名保持一致。

# 4. 应用构建

在应用构建节点，可以新建应用了。如何新建应用参考《领域注册及新建应用》文档

![](/assets/image048.jpg)

# 5. 系统管理

系统管理中通过用户管理、角色管理。可以对YonBuilder中的功能做不同维度的授权。

## 5.1 用户管理

用户管理中预置了一部分用户。运维管理者可以通过当前的用户管理中，添加业务中台中的用户，并为其分配对应角色。完成后，用户即可登录YonBuilder。

![](/assets/image050.jpg)

## 5.2 角色管理

角色管理预置了三种角色，可以针对YonBuilder中的权限进行分配；

![](/assets/image052.jpg)

