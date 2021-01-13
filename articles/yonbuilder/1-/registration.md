# 1 业务场景

在本章节我们将快速生成两个档案：供应商分类【树卡】、供应商基本档案【树表类型】，同时快速生成参照。

其中供应商分类样式如下

![](/assets/image009-shubiao.jpg)

供应商基本档案左侧为树形结构，引用供应商分类信息。右侧为基本档案信息。当选择左侧数据后，右侧展示为表，显示为当前供应商分类下的供应商数据。界面效果如下图。

![](/assets/image011-shubiao.jpg)

# 2 树形样式

## 2.1 数据建模

在应用构建中点击“新建实体”

![](/assets/image013-shubiao.jpg)

新建供应商分类，填写名称、编码，引用接口为树型结构，因为当前供应商分类也是档案，所以勾选“档案状态”，“ 树型结构”属性，填写表名以及列名。

![](/assets/image015-shubiao.jpg)

编码：supplyclassXX 名称：供应商分类XX 数据库表：train_supplyclassXX

<table>

 <tr>

 <td>字段编码</td>

 <td>字段名称</td>

 <td>类型</td>

 <td>数据库列名</td>

 </tr>

 <tr>

 <td>code</td>

 <td>编码</td>

 <td>文本</td>

 <td>code</td>

 </tr>

 <tr>

 <td>name</td>

 <td>名称</td>

 <td>文本</td>

 <td>name</td>

 </tr>

</table>

保存后必须点击发布

![](/assets/image018-shubiao.jpg)

完成效果如下图

![](/assets/image020-shubiao.jpg)

## 2.2 页面建模

点击新建页面功能

![](/assets/image022-shubiao.jpg)

![](/assets/image024-shubiao.jpg)

点击完成

![](/assets/image026-shubiao.jpg)

预览效果如下

![](/assets/image028-shubiao.jpg)

我们可以调整界面上显示“上级”信息“显示”

![](/assets/image030-shubiao.jpg)

保存

## 2.3 参照发布

供应商分类需要提供参照以供后续业务节点使用，所以我们需要发布参照

![](/assets/image032-shubiao.jpg)

点击发布

![](/assets/image034-shubiao.jpg)

此时可以使用供应商分类的参照了

# 3 树表样式

## 3.1 数据建模

### 3.1.1 新建枚举

新建企业规模枚举

![](/assets/image036-shubiao.jpg)

### 3.1.2 新建模型

1、 新建表实体，属性勾选档案，录入相关属性

![](/assets/image038-shubiao.jpg)

编码：supplyXX 名称：供应商分类XX 数据库：train_supplyXX

具体字段属性如下

<table>

 <tr>

 <td>字段编码</td>

 <td>字段名称</td>

 <td>类型</td>

 <td>数据库列名</td>

 </tr>

 <tr>

 <td>code</td>

 <td>供应商编码</td>

 <td>文本</td>

 <td>code</td>

 </tr>

 <tr>

 <td>name</td>

<td>供应商名称</td>

<td>文本</td>

<td>name</td>

 </tr>

 <tr>

 <td>supplierclass</td>

<td>供应商分类</td>

<td>单选引用：供应商分类</td>

<td>supplierclass</td>

 </tr>

 <tr>

 <td>memcode</td>

 <td>助记码</td>

 <td>文本</td>

 <td>memcode</td>

 </tr>

 <tr>

 <td> phone </td>

<td>电话</td>

<td>文本</td>

<td>phone</td>

 </tr>

 <tr>

 <td>mail</td>

<td>邮箱</td>

<td>文本</td>

<td>mail</td>

 </tr>

 <tr>

 <td>address</td>

 <td>地址</td>

 <td>文本</td>

 <td>address</td>

 </tr>

 <tr>

 <td>contract</td>

 <td>联系人</td>

 <td>文本</td>

 <td>contract</td>

 </tr>

 <tr>

 <td>corpsize</td>

 <td>企业规模</td>

 <td>单选：企业规模</td>

 <td>corpsize</td>

 </tr>

 <tr>

 <td>industry</td>

 <td>企业所属行业</td>

 <td>文本</td>

 <td>industry</td>

 </tr>

 <tr>

 <td>file</td>

 <td>附件</td>

 <td>附件</td>

 <td>file</td>

 </tr>

</table>

特殊字段配置

1) 附件，需要选择类型为“附件”；

2) 添加供应商分类，类型为“单项引用”，选择我们在上面发布的“供应商分类XX”模型

![](/assets/image041-shubiao.jpg)

3) 枚举

模型上字段修改为“单选”，配置创建好的枚举

![](/assets/image043-shubiao.jpg)

配置完成后效果如下图

![](/assets/image045-shubiao.jpg)

最终配置完成效果如下图:

![](/assets/image047-shubiao.jpg)

保存后必须点击发布

![](/assets/image049-shubiao.jpg)

## 3.2 页面建模

### 3.2.1 新建页面

在页面建模页签，点击新建页面

![](/assets/image050-shubiao.jpg)

选择左树右表页面样式

![](/assets/image052-shubiao.jpg)

点击下一步

![](/assets/image054-shubiao.jpg)

➢ 填写页面名称，同时勾选生成参照

➢ 选择树为4.1.2.1章节创建的树模型“供应商分类”；

➢ 表为右侧表需要展示的供应商档案；

➢ 关联关系配置为树表的关联项，供应商档案的供应商分类字段；

配置完成后，点击完成

此时会在当前页签下看到新建的两个页面

![](/assets/image056-shubiao.jpg)

执行数据库建表脚本

![](/assets/image058-shubiao.jpg)

点击左侧打开列表页面

![](/assets/image060-shubiao.jpg)

![](/assets/image062-shubiao.jpg)

点击右上角预览功能，界面上可以直接录入数据，各种操作均可以成功。

![](/assets/image064-shubiao.jpg)

新增效果

![](/assets/image066-shubiao.jpg)

我们可以通过下面步骤对页面进行样式配置

### 3.2.2 页面配置

#### 3.2.2.1 列表配置

列表界面UI展示

![](/assets/image068-shubiao.jpg)

切换到层级区域，可以快速定位控件

![](/assets/image070-shubiao.jpg)

1、查询区配置

![](/assets/image072-shubiao.jpg)

可以通过拖拽字段实现查询区及候选区切换，如将助记码拖拽到下面。启用作为查询条件

![](/assets/image074-shubiao.jpg)

2、调整字段显示属性

表格区域可快速调整字段上下顺序

![](/assets/image076-shubiao.jpg)

左侧字段拖拽

![](/assets/image078-shubiao.jpg)

配置完成后保存

![](/assets/image080-shubiao.jpg)

#### 3.2.2.2 卡片配置

打开卡片页面

![](/assets/image082-shubiao.jpg)

1、 新建分区放置附件

![](/assets/image084-shubiao.jpg)

删除表单名

![](/assets/image086-shubiao.jpg)

拖拽到表单区域

![](/assets/image088-shubiao.jpg)

配置占用三列

![](/assets/image090-shubiao.jpg)

2、 调整字段显示顺序

自行调整，把联系人拖拽到电话前

3、 调整是否修改

![](/assets/image092-shubiao.jpg)

4、 调整业务特性字段

邮箱字段

![](/assets/image094-shubiao.jpg)

电话

![](/assets/image096-shubiao.jpg)

5、 添加默认值

![](/assets/image098-shubiao.jpg)

保存后预览

6、 添加默认值

![](/assets/image100-shubiao.jpg)

### 3.2.3 参照发布

同样，供应商档案需要发布参照，后续业务功能才可以引用

![](/assets/image102-shubiao.jpg)

点击发布，完成后效果如下

![](/assets/image104-shubiao.jpg)

此时两个参照都可以使用了

# 4 应用效果

1、 供应商分类树类型界面效果：

在页面建模下找到列表页面，点击浏览，如下图，可录入数据

![](/assets/image106-shubiao.jpg)

选中根节点，点击新增会自动带出上级分类

![](/assets/image108-shubiao.jpg)

录入后保存

![](/assets/image110-shubiao.jpg)

2、 供应商档案树表类型界面样式

点击浏览列表，左侧会加载出供应商分类信息

![](/assets/image112-shubiao.jpg)

选中左侧分类点击新增时

![](/assets/image113-shubiao.jpg)

保存后效果

![](/assets/image115-shubiao.jpg)

