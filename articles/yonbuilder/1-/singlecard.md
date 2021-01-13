# 1 业务场景

本章节我们将开发供应商银行账户节点，样式为单表列表卡片样式。主要目的是让学员了解线上开发过程，如何通过线上提供的函数实现业务功能开发。

功能核心业务功能说明

1、 供应商银行账号展现方式为列表卡片，可以录入供应商银行账号；

2、 新增默认值“是否默认”为“是”，“账户状态”为“冻结”；

3、 保存前检查是否已存在默认账号，如果当前供应商已经存在默认账号，则提示仅仅可以设置一个默认账号不允许保存；

4、 添加“冻结”按钮，设置“账户状态”字段为“冻结”；

节点最终效果如下图

![](/assets/image009danka.jpg)

**列表界面样式**

![](/assets/image011danka.jpg)

**新增界面**

![](/assets/image013danka.jpg)

**新增保存后界面**

# 2 数据建模

## 2.1 新建枚举

枚举定义：

账户状态 custaccstatus 字符

<table>

 <tr>

 <td>枚举值</td>

 <td>名称</td>

 <td>说明</td>

 </tr>

 <tr>

 <td>1</td>

 <td>正常</td>

 <td></td>

 </tr>

 <tr>

 <td>2</td>

 <td>冻结</td>

 <td></td>


 </tr>

 <tr>

 <td>3</td>

 <td>封存</td>

 <td></td>

 </tr>

</table>


在数据建模-枚举页签中，点击新增枚举

![](/assets/image016danka.jpg)

录入数据并保存

![](/assets/image018danka.jpg)

枚举定义：

账户类型 personbank 字符

<table>

 <tr>

 <td>枚举值</td>

 <td>名称</td>

 <td>说明</td>

 </tr>

 <tr>

 <td>1</td>

 <td>个人</td>

 <td></td>

 </tr>

 <tr>

 <td>2</td>

 <td>企业</td>

 <td></td>

 </tr>

</table>

同样方式新建枚举账户类型

![](/assets/image021danka.jpg)

是否枚举

<table>

 <tr>

 <td>枚举值</td>

 <td>名称</td>

 <td>说明</td>

 </tr>

 <tr>

 <td>Y</td>

 <td>是</td>

 <td></td>

 </tr>

 <tr>

 <td>N</td>

 <td>否</td>

 <td></td>

 </tr>

</table>

![](/assets/image025danka.jpg)

## 2.2 新建数据模型

1、 在数据建模页面，点击新增实体

![](/assets/image027danka.jpg)

界面核心功能描述如下

➢ 实体包括实体名称、编码、父实体、描述信息、引用接口等 

实体名称/编码：必填，不可重复 

父实体：可选项，下拉选择，可选当前应用已发布的实体名称； 

描述信息：可选项，对实体进行简要描述 

引用接口：可选项，接口包括审批、业务流、交易类型、树型结构等；

➢ 实体的属性： 

属性编码/名称：可手动修改，首次编辑属性名称时编码会生成对应的拼音字段； 

属性类型：默认类型为文本，可根据需要进行重新选择； 

单选引用：当类型为单选引用时，可选实体范围：平台已发布参照、当前租户已购买应用的参照、协同表单发布的参照、自建应用中发布的参照等；

单选：配置枚举，可选的枚举范围为：平台已发布枚举和租户自建枚举； 

表字段名：不可编辑，系统自动生成； 

唯一：可选，勾选后该属性字段名不可重复； 

标签：可多选，从参照中选择，无默认值，从右侧操作面板中进行操作。

![](/assets/image029danka.jpg)

系统属性：包括基类属性+特性的属性两部分内容，作为系统属性显示在“系统属性”页签，仅查看，不提供编辑和删除功能。系统属性与勾选的引用接口有关，根据选择的接口分成基础可选项、审批、业务流、交易类型等八种，每一种下面包含多个系统属性，可以展开查看。

2、 实体录入基本信息如下

编码：supplierbankaccXX

名称：供应商银行账户XX

数据库表：train_supplierbankaccXX

引用接口：主组织 档案状态

配置完成后如下图

![](/assets/image029danka.jpg)

实体属性字段如下

<table>

 <tr>

 <td>字段编码</td>

 <td>字段名称</td>

 <td>类型</td>

 <td>数据库列名</td>

 </tr>

 <tr>

 <td>code</td>

 <td>供应商账号</td>

 <td>文本</td>

 <td>code</td>

 </tr>

 <tr>

 <td>name</td>

 <td>供应商户名</td>

 <td>文本</td>

 <td>name</td>

 </tr>

 <tr>

 <td>banktype</td>

 <td>银行类别</td>

 <td>单选引用：银行类别</td>

 <td>banktype</td>

 </tr>

 <tr>

 <td>supplier</td>

 <td>所属供应商</td>

 <td>单选引用：</td>

 <td>supplier</td>

 </tr>

 <tr>

 <td>personbank</td>

 <td>账户类型</td>

 <td>单选：账户类型</td>

 <td>personbank</td>

 </tr>

 <tr>

 <td>taxno</td>

 <td>税号</td>

 <td>文本</td>

 <td>shuihao</td>

 </tr>

 <tr>

 <td>isdefault</td>

 <td>是否默认账户</td>

 <td>单选：是否</td>

 <td>isdefault</td>

 </tr>

 <tr>

 <td>custaccstatus</td>

 <td>账户状态</td>

 <td>单选：账户状态</td>

 <td>custaccstat</td>

 </tr>

 <tr>

 <td>memo</td>

 <td>说明</td>

 <td>文本</td>

 <td> memo</td>

 </tr>

 <tr>

 <td>files</td>

 <td>附件</td>

 <td>附件</td>

 <td>files</td>

 </tr>

</table>


1、 添加常规属性

![](/assets/image034danka.jpg)

2、 配置参照

![](/assets/image036danka.jpg)

银行类别

![](/assets/image038danka.jpg)

供应商

添加我们创建的供应商

![](/assets/image040danka.jpg)

完成后如下图

![](/assets/image042danka.jpg)

3、 添加枚举

选择“单选”，同时选择上步骤添加的枚举“账户状态”。

![](/assets/image044danka.jpg)

是否默认值

![](/assets/image046danka.jpg)

账户类型

![](/assets/image048danka.jpg)

最终效果如下

![](/assets/image050danka.jpg)

![](/assets/image052danka.jpg)

4、添加附件

![](/assets/image054danka.jpg)

5、 大文本

![](/assets/image056danka.jpg)

最终效果如下图

![](/assets/image058danka.jpg)

保存后点击发布

![](/assets/image060danka.jpg)

# 3 页面建模

页面建模提供应用的功能页面设计器、组合页面设计器、报表设计器，支持不同功能业务页面的设计，同时支持前后端扩展，实现单据页面、画布页面、业务事件的构建和交互驱动过程的个性化扩展。

切换到页面建模页签

![](/assets/image062danka.jpg)

## 3.1 新建页面

单据设计器提供7种预置模板和多种布局容器和组件，支持表格、表单、网格、树等多种页面的组装能力： 预置模板：提供单表、单卡、左树右表、左树右卡、树形表、一主多子、主子孙表7个常用模板。 点击新增页面，选择“单卡”

![](/assets/image064danka.jpg)

点击下一步，填写页面名称，勾选“生成参照”，选择元数据为上步骤生成的“供应商银行账号”

![](/assets/image066danka.jpg)

点击完成，生成页面，如下图，下一步可以对界面进行业务配置。

![](/assets/image068danka.jpg)

为了参照生效需要发布参照。

![](/assets/image070danka.jpg)

## 3.2 页面布局说明

新建好的页面，我们可以打开设计器，配置界面显示效果

![](/assets/image072danka.jpg)

模板由三个区域构成：组件区、设计区和属性区。 

组件区：提供构成页面的元素，包括布局容器、数据容器、工具栏、按钮控件、基础控件、业务控件、协作控件等。 

设计区：单据页面的设计区域。包括卡片头部按钮区、卡片底部按钮区、数据显示区域等，根据需要来设计。 

属性区：选中的页面元素的属性设置区域。 布局容器：构成页面布局的元素，系统提供了网格、卡片组和多页签三种布局容器，容器支持样式包括大小和位置，背景图边框颜色等属性设置；布局容器中拖入组件控件来实现单据页面的组装。

数据容器： 

工具栏：定义单据页面中的操作按钮区域及按钮区域的样式。 

按钮控件：定义单据页中按钮区域中的按钮，包括按钮和下拉按钮两个控件，可定义按钮类型、规格类型及单击按钮的动作，包括 新增、编辑、删除、提交、撤回、启用、停用等。 

基础控件：定义单据页面的基础控件，包括本框、多行文本、富文本、多语文本、手机、电话、邮箱、证件号、数值、金额、选项、开关、日期框、日期时间、时间框、评分、地图定位、图片上传等。 

业务控件：定义单据页面中需要的业务类控件，包括附件管理、参照框、自动编码、下推按钮、打印、描述信息等。 

协作控件：与协作套件相关的控件，包括协作套件和沟通套件。 

其他：包括自定义控件，即用户可通过关联扩展组件或配置关联属性的方式来定义系统中不存在的控件使用。

## 3.3 列表界面配置

### 3.3.1 调整查询区

#### 3.3.1.1 业务需求

当前节点查询区按照下述配置

✓ 常用查询条件：组织、账户状态、所属供应商、供应商银行账号、供应商户名、银行类别、账户类型、启用；

候选条件：说明、税号、是否默认账户；

✓ 配置组织为必输项；

✓ 账户状态、账户类型可多选；

✓ 启用默认值为启用；

#### 3.3.1.2 配置实现

1、 组织配置必输

![](/assets/image074danka.jpg)

2、 配置默认值

![](/assets/image076danka.jpg)

3、 字段调整宽度

税号配置宽度

完成后保存

#### 3.3.1.3 应用效果

回到列表，点击预览

![](/assets/image078danka.jpg)

![](/assets/image080danka.jpg)

配置完成后效果如下图

![](/assets/image082danka.jpg)

### 3.3.2 界面样式调整

1、 调整字段顺序

最终显示效果

![](/assets/image084danka.jpg)

## 3.4 卡片界面配置

### 3.4.1 业务需求

卡片页面为浏览和编辑功能，界面需求描述如下：

1、 按照需求调整界面样式，按业务分区；

2、 配置启用、账户状态字段不可编辑；

3、 配置说明字段显示大文本；

4、 添加账户类型默认值为“企业”；

### 3.4.2 配置实现

1、 调整界面分区结构

1) 修改表单名称为“基本信息”

![](/assets/image086danka.jpg)

2) 添加分区 

a) 添加供应商信息

![](/assets/image088danka.jpg)

b) 附件拖拽到新分区

新建后修改容器名称，同时拖拽供应商、税号字段到当前容器

![](/assets/image090danka.jpg)

可以修改附件的标题，效果如下图

![](/assets/image092danka.jpg)

2、 配置不可编辑

![](/assets/image094danka.jpg)

3、 配置默认值

![](/assets/image096danka.jpg)

### 3.4.3 应用效果

列表新增时界面样式

![](/assets/image098danka.jpg)

录入数据后

![](/assets/image100danka.jpg)

保存后

![](/assets/image102danka.jpg)

## 3.5 界面交互功能配置

常见界面交互，如根据某字段取值，配置哪些字段是否可编辑态或者默认值等，可通过此功能来实现。

### 3.5.1 业务场景

需求：账户类型如果为“个人”，则税号“不可编辑”

### 3.5.2 配置实现

选中卡片容器，下方“交互规则”

![](/assets/image104danka.jpg)

点击添加

![](/assets/image106danka.jpg)

配置规则

![](/assets/image108danka.jpg)

点击保存

![](/assets/image110danka.jpg)

### 3.5.3 应用效果

列表页面点击新增

![](/assets/image112danka.jpg)

选择类别为个人

![](/assets/image114danka.jpg)

## 3.6 添加字段

### 3.6.1 业务场景

模型、页面建立好后，发现少了一些业务字段，此时可能会添加对应的业务字段

需求：在当前页面上添加账户开立日期、登记日期，类型为“日期”；

### 3.6.2 配置实现

1、 数据建模添加字段

opendate账户开立日期/ inputdate登记日期

![](/assets/image116danka.jpg)

保存后点击发布

![](/assets/image118danka.jpg)

2、 列表界面添加字段

![](/assets/image120danka.jpg)

找到左侧表格区域

![](/assets/image122danka.jpg)

点击字段设置

![](/assets/image124danka.jpg)

拖拽字段到容器中

![](/assets/image126danka.jpg)

调整位置保存后预览效果如下图

![](/assets/image128danka.jpg)

3、 卡片界面添加字段

选中基本信息页签，点击字段设置

![](/assets/image130danka.jpg)

同上拖拽后效果如下图

![](/assets/image132danka.jpg)

拖拽显示顺序

![](/assets/image134danka.jpg)

保存后效果如下图

![](/assets/image136danka.jpg)

## 3.7 查询方案

### 3.7.1 查询方案配置

用户界面打开后，可以配置不同的查询方案

![](/assets/image138danka.jpg)

点击添加方案

![](/assets/image140danka.jpg)

添加查询条件

![](/assets/image142danka.jpg)

还可以针对查询条件直接配置默认值

### 3.7.2 应用效果

![](/assets/image144danka.jpg)

# 4 函数式在线脚本

基于应用构建平台的脚本引擎，支持用户完成自定义逻辑的脚本编写；类型分为前端脚本和后端脚本，无论前端还是后端脚本都是以JS为语言规范，其中操作元数据是以平台提供的YonSQL对数据进行操作，YonSQL支持SQL95标准规范与绝大部分SQL编写方式。 函数式在线脚本分为前端函数、后端函数、API函数。

➢ 前端脚本：可用于控件状态控制、控件赋值、简单数据计算、openAPI调用；

对于原有功能的扩展，也可以在页面初始化中绑定；

➢ 可用于后端数据计算、业务调用、数据实体赋值、openAPI调用；

## 4.1 业务场景

1、 关键字段默认值赋值

新增时账户状态默认为“正常”，登记日期默认为“当前日期”；

2、 保存前校验

登记日期>账户开立日期

3、 值选择前事件

如果账户类型为“个人”，则税号不可编辑

4、 值改变后事件

供应商改变后，税号清空

## 4.2 前端函数

前端函数一般做一些设置默认值，或者校验。对于原有功能的扩展，请在页面初始化中绑定。

触发前事件，一般可以通过使用beforeXXX的方式实现

### 4.2.1 页面初始化

在页面初始化界面，可以在页面刚打开的时点，注册前端函数，添加前端事件监听。

#### 4.2.1.1 设置默认值

需求：新增设置账户状态默认为“正常”， 登记日期默认为“当前日期”

1、 如果函数为当前节点使用，可以新建目录，将函数放置在创建的目录，创建目录位置如下图

![](/assets/image146danka.jpg)

点击新增

![](/assets/image148danka.jpg)

点击确定

![](/assets/image150danka.jpg)

我们可以直接在函数里编写脚本，点击“设计”，出现函数脚本编辑器，如下图

![](/assets/image152danka.jpg)

脚本实现

判断是否新增状态，如果为新增态则设置日期为当前日期，需要对日期做格式化

`function (event) {


 var viewModel = this;


 let mode = viewModel.getParams().mode;


// 卡片详情页面才显示冻结、解冻按钮


if (mode.toLocaleLowerCase() == 'add') {


 var formatDate = function (date) {
 
var y = date.getFullYear();
 
var m = date.getMonth() + 1;


 m = m < 10 ? '0' + m : m;
 
var d = date.getDate();
 
d = d < 10 ? ('0' + d) : d;


 return y + '-' + m + '-' + d;


 };
viewModel.get('inputdate').setValue(formatDate(new Date()));


viewModel.get('custaccstatus').setValue("1");


}


}`

保存成功后在下面节点可看到函数

![](/assets/image155danka.jpg)

配置完成后可看到目录，打开卡片页面

![](/assets/image157danka.jpg)

点击设置，可以看到刚创建的目录，选择我们刚创建好的脚本

![](/assets/image159danka.jpg)

点击确认后效果如下图

![](/assets/image161danka.jpg)

应用效果

![](/assets/image163danka.jpg)

#### 4.2.1.2 保存前校验

注册到页面初始化前端函数

`function (event) {

 var viewModel = this; 

//设置保存前校验 

viewModel.on("beforeSave", function(args){ 

var inputdate = viewModel.get('inputdate').getValue(); 

var opendate = viewModel.get('opendate').getValue(); 

//判断 dateA 是否大于 dateB，为 true，登记日期应该大于开立日期 

const isAfterDate = (inputdate, opendate) => inputdate > opendate; 

if(!isAfterDate(inputdate,opendate)){ 

cb.utils.alert('登记日期必须大于账户开立日期');

 return false; 

} 

}) 

} 
`

应用效果如下：保存后提示

![](/assets/image166danka.jpg)

### 4.2.2 值改变后事件

值改变后事件

1、 函数界面新增前端函数

![](/assets/image168danka.jpg)

确定后点击设计

![](/assets/image170danka.jpg)

右侧可以切换数据模型，选择对应字段配置

2、 界面添加函数，设置赋值为空

`viewModel.get('taxno').setValue(""); `

3、 配置

在卡片页面，校验数据，参照值改变后，点击设置

![](/assets/image173danka.jpg)

录入供应商税号后，切换供应商会自动清空税号。

### 4.2.3 前端调试

在页面打开后打开F12下方Console找到对应位置，可以在对应的代码上做调试

![](/assets/image175danka.jpg)

录入数据后

![](/assets/image177danka.jpg)

## 4.3 后端函数

后端函数是规则链中的（注意区分），前端函数不要去调用后端函数。只能调用API函数

### 4.3.1 业务场景

需求：保存前校验当前供应商默认账户是否唯一

### 4.3.2 新建后端函数

找到函数-后端，点击新增函数

![](/assets/image179danka.jpg)

点击确定后，效果如下图，可以开始编辑后端函数

![](/assets/image181danka.jpg)

### 4.3.3 调用查询函数

1、 获取数据

let data=JSON.parse(param.data); //可获取查询条件，当前保存前可以获取业务数据

var {isdefault,supplier,id} = data;

2、 点击检查查询可以插入简单查询SQL

![](/assets/image183danka.jpg)

我们需要修改查询的库表，右侧选择对应的模型为当前节点的数据模型

点击uri可以获取当前对应的后台表

![](/assets/image185danka.jpg)

点击后效果如下

![](/assets/image187danka.jpg)

3、 调用查询API

**ObjectStore.queryByYonQL**

![](/assets/image189danka.jpg)

4、 最终代码

`let AbstractTrigger = require('AbstractTrigger'); 

class MyTrigger extends AbstractTrigger { 

execute(context,param){ 

// let data=JSON.parse(param.data); 

let data=param.data[0]; 

var {isdefault,supplier,id} = data; 

var sql ="select id from GT4066AT1.GT4066AT1.supplierbankacc where supplier='"+supplier+"' and isdefault='Y' and id!='"+id+"'" 

//如果当前设置了 default 

if(isdefault=="Y"){ 

let resp = ObjectStore.queryByYonQL(sql); 

resp.map((v)=>{ 

if (v.id!==null) { 

throw new Error('当前供应商唯一默认账户已存在，请检查！'); 

} 

}); 

} 

return {}; 

} 

} 

exports({"entryPoint":MyTrigger}); 

`
### 4.3.4 函数调用

找到保存按钮，点击保存按钮，上面切换动作页签

![](/assets/image192danka.jpg)

点击动作的“编辑”功能

![](/assets/image194danka.jpg)

会加载保存动作的所有后台业务规则，我们在保存前可以添加在上一步骤开发的后台函数：保存前校验因为我们需要在保存前做校验，所以调整动作执行顺序，拖拽函数到保存前动作，配置完成后点击保存即可。

![](/assets/image196danka.jpg)

### 4.3.5 后端函数调试

打开后端函数，点击右上角测试

![](/assets/image198danka.jpg)

点击复制，复制句柄

按照上述说明，在业务单据卡片页面上点击shift+D输入上面复制的句柄。这样在做保存操作时，会自动跳转到调试页面。

![](/assets/image200danka.jpg)

 在打开界面后，按照说明点击Alt+Shift+D

![](/assets/image202danka.jpg)

点击单步调试可以在右侧看到变量信息

![](/assets/image204danka.jpg)

### 4.3.6 应用效果

点击保存时，如果已经录入默认账户

![](/assets/image206danka.jpg)

## 4.4 API函数

专属云版本API函数主要用于提供给前端函数调用，暂不提供API发布功能。

### 4.4.1 业务场景

我们在选择了供应商档案参照后，会校验供应商档案状态是否为启用。

思路：

1、 配置参照选值后监听，传入供应商ID，需要调用服务查询；

2、 提供API函数：使用YonSQL查询正确数据，并把结果返回前端；

3、 前端弹出提示框并处理数据；

### 4.4.2 API函数定义

注意要修改YonSQL中的模型编码，尽量从右侧拖拽

![](/assets/image208danka.jpg)

完整函数代码如下

`let AbstractAPIHandler = require('AbstractAPIHandler'); 

class MyAPIHandler extends AbstractAPIHandler { 

execute(request){ 

var supplier = request.supplier; 

var sql='select id from GT1AT1.GT1AT1.supplyhx where id = "'+supplier+'" and enable=1 '; 

var rst = ObjectStore.queryByYonQL(sql); 

var id = ""; 

if(rst!=null&&rst.length>0){ 

id = rst[0].id; 

} 

return {"id":id,"request":request}; 

} 

} 

exports({"entryPoint":MyAPIHandler}); 
`

### 4.4.3 前端函数调用API函数

1、 调用时首先获取API函数ID，点击刚创建的API函数，找到上面的ID

![](/assets/image211danka.jpg)

2、 新建前端函数：供应商参照值改变后，首先获取

![](/assets/image213danka.jpg)

`function (event) { 

var viewModel = this; 

//选择数据后，根据选择到的数据 

var supplier=viewModel.get('supplier').getValue(); 

var supplier_name=viewModel.get('supplier_name').getValue(); 

if(supplier!=null&&supplier!=""){ 

cb.rest.invokeFunction("b7208601327a49a1a12ec28fb215abe3", {"supplier":supplier}, 

function(err, res) { 

var id = res.id; 

if(id===""){ 

cb.utils.alert("供应商银行账户非启用状态，请检查!"); 

viewModel.get('supplier_name').setValue(""); 

viewModel.get('supplier').setValue(""); 

} 

}) 

} `


### 4.4.4 前端函数注册

![](/assets/image216danka.jpg)

点击确定后，点击设计器上的“保存”。

### 4.4.5 应用效果

停用一条供应商档案数据，在供应商银行账户的参照中选择数据，会弹出提示。

![](/assets/image218danka.jpg)

# 5 典型业务功能

## 5.1 按钮功能开发

以冻结功能为例，学习如何在线上通过前后端函数定义完成按钮功能。

### 5.1.1 前端添加按钮

效果如下图

![](/assets/image220danka.jpg)

### 5.1.2 API函数定义
`
let AbstractAPIHandler = require('AbstractAPIHandler'); 

class MyAPIHandler extends AbstractAPIHandler { 

execute(request){ 

var data = request.data; 

data.custaccstatus = "2"; 

ObjectStore.updateById("GT1AT1.GT1AT1.supplierbankacchx",data); 

var sql = "select * from GT1AT1.GT1AT1.supplierbankacchx where id='"+data.id+"' "; 

var retobj = ObjectStore.queryByYonQL(sql); 

if(retobj!=null){ 

return {"data":retobj[0]}; 

}else{ 

return {"data":data}; 

} 

} 

} 

exports({"entryPoint":MyAPIHandler}); 

`

配置完成后

![](/assets/image224danka.jpg)

### 5.1.3 前端函数

新建前端函数：

![](/assets/image226danka.jpg)

调用后端函数更新后，需要重新查询最新数据并返回给model

同样注意要替换下面代码的funid

`function (event) { 

var viewModel = this; 

var data = viewModel.getAllData(); 

//账户状态 

var custaccstatus = viewModel.get('custaccstatus').getValue(); 

//校验 

if(custaccstatus!="1"){ 

cb.utils.alert("只有状态为正常的单据才可以冻结！") 

}else{ 

cb.rest.invokeFunction("cf25efd0870c4fdc949a506084516dcd", {"data": data},function(err, res){ 

var data = res.data; 

if(data!=null) 

viewModel.setData(data); 

}); 

} 

} `


### 5.1.4 配置动作执行函数

![](/assets/image230danka.jpg)

### 5.1.5 应用效果

单据初始态

![](/assets/image232danka.jpg)

点击冻结，更新状态为“冻结”

![](/assets/image234danka.jpg)

再次点击冻结时

![](/assets/image236danka.jpg)

### 5.1.6 练习

自行完成解冻功能

# 6 附录

## 6.1 常用后端持久化API

ObjectStore对应API

1、 新增 

a) 单条新增

<table>

 <tr>

 <td>方法：</td>

 <td colspan="2"> insert(URI,object,billNum)</td>

 </tr>

 <tr>

 <td>描述：</td>

 <td colspan="2">保存实体，默认自动生成主键、审计信息</td>

 </tr>

 <tr>

 <td>入参：</td>

 <td colspan="2"></td>

 </tr>

 <tr>

 <td>名称</td>

 <td>含义</td>

 <td>示例</td>

 </tr>

 <tr>

 <td>URI</td>

 <td>实体统一资源标识符</td>

 <td>developplatform.AX000888.PX012991</td>

 </tr>

 <tr>

 <td>object</td>

 <td>实体对象，支持包含子实体，包含子实体时基于主子表关系值</td>

 <td>{name:"qqq",bustype:"1639837036187904",item41d:"45gty",isWfControlled:"1",verifystate:"0",returncount:"0",

pX000008_tabpane0List:[{hasDefaultInit:true,item20l:"www"},{hasDefaultInit:true,item20l:"mmm"}]}</td>

 </tr>

 <tr>

 <td>billNum</td>

 <td>表单编码</td>

 <td>f6f7e02c</td>

 </tr>

 <tr>

 <td>返回值：</td>

 <td>该实体对象</td>

 <td></td>

 </tr>

</table>

`var object = {name:"qqq",bustype:"1639837036187904",item41d:"45gty",isWfControlled:"1", verifystate:"0",returncount:"0",pX000008_tabpane0List:[{hasDefaultInit:true,item20l:"www"}, {hasDefaultInit:true,item20l:"mmm"}]}; var res = ObjectStore.insert("developplatform.AX000003.PX000008",object,'f6f7e02c'); `

`//JavaScript 对象的 JSON 串示例 

{ 

"name":"qqq", 

"bustype":"1639837036187904", 

"item41d":"45gty", 

"isWfControlled":true, 

"verifystate":0, 

"returncount":0, 

"pX000008_tabpane0List":[ 

{ 

"hasDefaultInit":true, 

"item20l":"www",

"id":"20bdd921c3234673a04d3219d5129021", 

"meta_fk":"fdccf0cd1a7b472fa0db47c66632bc79", "pubts":"Mar 13, 2020 5:04:26 PM" 

}, 

{ 

"hasDefaultInit":true, 

"item20l":"mmm", 

"id":"eef6430c6bac4b2892d019a80a2cf5a1", 

"meta_fk":"fdccf0cd1a7b472fa0db47c66632bc79", 

"pubts":"Mar 13, 2020 5:04:26 PM" 

}

 ], 

"id":"fdccf0cd1a7b472fa0db47c66632bc79", 

"creator":"xxx", 

"creationtime":"Mar 13, 2020 5:04:31 PM",

 "modifier":"xxx", 

"modifiedtime":"Mar 13, 2020 5:04:31 PM", 

"pubts":"Mar 13, 2020 5:04:31 PM"

 } `


b) 批量新增

<table>

 <tr>

 <td>方法：</td>

 <td colspan="2">insertBatch(URI,object List,billNum)</td>

 </tr>


 <tr>

 <td>描述：</td>

 <td colspan="2">批量保存实体，默认自动生成审计信息</td>

 </tr>

 <tr>

 <td>入参：</td>

 <td colspan="2"></td>

 </tr>

 <tr>

 <td>名称</td>

 <td>含义</td>

 <td>示例</td>

 </tr>

 <tr>

 <td>URI</td>

 <td>实体统一资源标识符</td>

 <td>developplatform.AX000888.PX012991</td>

 </tr>

 <tr>

 <td>objectList</td>

 <td>实体对象列表，支持包含子实体，包含子实体时基于主子表关系值</td>

 <td>[{name:"qqq",bustype:"1639837036187904",item41d:"45gty",isWfContr
olled:"1",verifystate:"0",returncount:"0",
pX000008_tabpane0List:[{hasDefaultInit:true,item20l:"www"},{hasDefa
ultInit:true,item20l:"mmm"}]},
{name:"www",bustype:"1639837036187904",item41d:"45gty",isWfCont
rolled:"1",verifystate:"0",returncount:"0",
pX000008_tabpane0List:[{hasDefaultInit:true,item20l:"rrr"},{hasDefaultI
nit:true,item20l:"ttt"}]}];</td>

 </tr>

 <tr>

 <td>billNum</td>

 <td>表单编码</td>

 <td>f6f7e02c</td>

 </tr>

<tr>

 <td>返回值：</td>

 <td  colspan="2">新增的多个实体对象</td>

 </tr>


</table>

2、 更新

a) 基于ID更新

![](/assets/image242danka.jpg)

b) 批量更新

![](/assets/image244danka.jpg)

## 6.2 动作规则清单

列表页（voucherlist、treelist）

![](/assets/image246danka.jpg)


卡片页（voucher、treevoucher）

![](/assets/image248danka.jpg)