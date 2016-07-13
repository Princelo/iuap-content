# 开发工具使用

## 开发工具使用手册 ##



### 1.开发环境 ###



#### 1.1 开发工具简介 ####



iUAP Studio是一个简单易用的基于Eclipse开发平台的web项目开发工具。工具集成了eclipse j2ee版本的大部分插件，大大降低了学习成本，并基于iUAP开发平台量身定做了很多实用功能，为WEB应用开发者提供便捷的可视化建模开发，包括快速生成代码块、提供界面友好的可扩展可定制的代码提示窗口、html标签扩展、JS第三方语法支持、页面模式和向导、组件仓库的管理、快速代码生成引擎以及元数据模型设计发布等功能。



#### 1.2 iuap_quickstart工程简介 ####



iuap_quickstart工程是iUAP开发平台的实例工程，该工程基于iUAP开发框架进行基本业务逻辑的编写,实现了完整的增删改查逻辑，并在具体的示例页面上加以展示。可以帮助业务开发人员快速的完成对平台基本功能的了解和使用。工程中包含了完整的iUAP基础组件和前后端框架，开发人员在iUAP Studio中可以通过新建iUAP项目来创建，并在此基础上进行开发。



### 2.开发流程 ###



#### 2.1 环境配置 ####



##### 2.1.1 JDK配置 #####



开发工具默认JDK位于安装目录下的Runtime目录。 在IDE中，选择窗口->首选项->JAVA->已安装的JRE，可以看到目前IDE中使用的JAVA环境。如果不使用默认的JDK，可手动添加本地JDK，勾选即可。



![]((./image/Jdk.png)





##### 2.1.2 Maven配置 #####



开发环境的maven位于iUAP开发工具包的DevTool\repository\Maven\Maven3.2.2目录下，也可以自定义使用本地maven。以默认maven为例，首先要设置maven的环境变量，在系统变量中添加环境变量MAVENHOME,该变量指向目录DevTool\repository\Maven\Maven3.2.2，然后在Path变量中加入路径%MAVENHOME%\bin。 maven环境变量配置好以后，我们要在IDE中配置maven的配置文件的路径，在IDE的菜单栏中选择窗口->首选项->Maven->User Settings，将标签页的Global Settings和User Settings改为开发工具包内maven的配置文件的地址  





![]((./image/Mavensetting.png)

  



#### 2.2 新建项目 ####



在IDE菜单栏中选择新建->iUAP项目，点击下一步，进入新项目的配置页面。 输入项目名称建立新项目 如图所示：  



<center>

![]((./image/iwebproject.png)

</center> 



点击完成，稍等片刻，IDE在完成maven库的更新下载以及工程编译的进度读条后，这时工作空间中会建立一个新的iUAP工程。



#### 2.3 建模过程 ####



###### 2.3.1 实体类层编写 ######



iUAP开发工具可使用三种方式快速生成javabean实体类。

1. 工具使用JPA插件，通过数据表的方式自动建立实体类，首先建立好数据库、实体表、以及数据库连接，在工程上右键选择JPA tools，从数据表反向生成Entity。  
![]((./image/iwebJPA.png)   
![]((./image/iwebJPA2.png)
2. 通过元数据设计器设计元数据模型，并生成java源代码
3. 通过代码快速生成向导，选择适用的模版类型生成相应格式的javaBean。





选择生成字段以及包名等，工具自动生成注解，生成实体类如下：   



		@Entity

		@Table(name="example_demo")

		@NamedQuery(name="Demo.findAll", query="SELECT d FROM Demo d")

		public class Demo implements Serializable {

		    private static final long serialVersionUID = 1L;

		

		    @Id

		    private long id;

		

		    @NotBlank(message="测试编码不能为空!")

		    private String code;

		

		    private String memo;

		

		    private String name;

		

		    private String isdefault;

		

		    public Demo() {

		    }

		

		    public long getId() {

		        return this.id;

		    }

		

		    public void setId(long id) {

		        this.id = id;

		    }

		

		    public String getCode() {

		        return this.code;

		    }

		

		    public void setCode(String code) {

		        this.code = code;

		    }

		

		    public String getMemo() {

		        return this.memo;

		    }

		

		    public void setMemo(String memo) {

		        this.memo = memo;

		    }

		

		    public String getName() {

		        return this.name;

		    }

		

		    public String getIsdefault() {

		        return isdefault;

		    }

		

		    public void setIsdefault(String isdefault) {

		        this.isdefault = isdefault;

		    }

		

		    public void setName(String name) {

		        this.name = name;

		    }

		

		}

 



##### 2.3.2 数据模型引入 #####



开发工具中的数据模型有很多用途，比如绑定控件替换参数，一键生成数据绑定配置文件，页面模式化向导等。 这里的数据模型的概念实际上是基于JavaBean实体类的xml文件，以.model为后缀名。iEOP开发工具提供两种方式生成数据模型。   

一是通过数据模型向导直接新建模型。右键工程，选择新建->其他。在向导页中选择iEOP->数据模型。下一步输入模型的名称以及位置，点击完成后，通过model编辑器完成模型的录入。 如图所示：   



<center>

![]((./image/model1.png)   



![]((./image/model.png)  



![]((./image/model2.png)  



![]((./image/model3.png)   



</center>  



二是通过绑定实体类，自动生成数据模型。 初始步骤同上，在输入模型名称后点击下一步，进入属性配置页面。 选择需要的实体类以及属性后，点击完成即可生成与实体类对应的模型文件。  



生成的模型文件如下所示：   



		<?xml version="1.0" encoding="UTF-8"?>

		<model xmlns="http://www.yonyou.com/uap/DataModel" className="uap.web.example.entity.Demo" id="Demo" name="Demo">

		  <attributes>

		    <attribute id="id" name="id" type="long"/>

		    <attribute id="code" name="code" type="String"/>

		    <attribute id="memo" name="memo" type="String"/>

		    <attribute id="name" name="name" type="String"/>

		    <attribute id="isdefault" name="isdefault" type="String"/>

		  </attributes>

		</model>



#### 2.4 新建页面 ####
右键点击工程根目录或者在工具栏中选择新建->iUAP页面，进入iUAP页面新建向导。 

页面统一建在工程下的src/main/webapp/pages目录下。 填写页面名称后，可以选择是否使用数据模型，如果不勾选数据模型，则可以点击完成，会创建仅包含基础js框架的页面。 若勾选，则点击下一步，进入数据模型绑定页。

下拉框中选择上一步创建的数据模型，并勾选用到的属性。用户可以通过勾选“选择”按钮使用多个数据模型，点击完成即可创建使用数据模型的html和js页面。



#### 2.5 数据绑定 ####



在有些情况下，可能不是要创建整个功能页面，而是在页面中添加一些功能控件，完成数据操作。 比如上图中的列表控件和表单控件。如果要单独添加这些控件如何做呢，这就需要用到控件的数据绑定。我们这里提供了目前最常用的两种控件模板，表格和表单。



以表单为例，默认使用web页面编辑器打开html页面文件。在左侧工具箱中选择iEOP数据控件下的表单项，双击打开数据配置页，关联上面创建的数据模型，点击完成即可在html中插件相关代码，如图所示：   



<center>

![]((./image/editor.png)   



![]((./image/codeinsert.png)  

  

</center>  



完成html代码创建后，并不意味着可以和后台数据做关联，数据还需要采用knockout的方式进行双向绑定，所以我们需要支持创建这种数据绑定js文件，



选中工程， 右键新建，在向导页中选择iEOP->数据绑定向导。 下一步选择js文件的位置，这里js文件一般需要与相应的html文件放在同一级目录下并且命名一样。下一步选择数据模型及其属性，点击完成即可创建JS文件。这里的js文件作为中间层，提供前台控件和后台数据的绑定机制。 如图所示：  



<center>

![]((./image/bind.png)   



![]((./image/bind2.png)  



![]((./image/bind3.png)  



![]((./image/bind4.png)  

  

</center>  





创建出来的js文件如下所示：  



<center>

![]((./image/bind4.png)   



</center>  



#### 2.6 示例工程运行调试 ####



webexample是平台基本开发功能的演示示例。 在调试运行工程之前，先运行DevTool\bin目录下的startpgsql.bat、startredis.bat、startzookeeper.bat启动PostgreSQL、Redis和Zookeeper



示例工程通过jetty的方式进行运行调试，在webexample工程项目的\src\test\java\uap\web\XXX文件夹下有对应的QuickStartXXX类，运行该类就能启动项目进行调试。webexample项目调试效果如下图：  



<center>

![]((./image/run.png)   



</center>  



### 3 代码提示 ###



#### 3.1 标签助手 ####



在“web页面编辑器”中，键入“<”即可开启智能提示助手，准确的提示出过滤后所有的标签，如图：  



<center>

![]((./image/assistant.png)   



</center>  





提示框左侧是经过过滤后的标签列表，右侧是当前标签对应的种类，适用浏览器版本，描述，备注以及示例，一目了然，方便快捷。 输入数字快捷键可以更加方便的把对应标签插入html当前位置。



#### 3.2 代码块 ####



在html中直接输入触发字符可提示代码块。 代码块是常用的代码组合，比如在js中输入$，回车，则可以自动输入document.getElementById(id)。 再举例，在HTML中输入i，回车，可以得到input button标签。  



<center>

![]((./image/assistant2.png)   



</center> 



如图，提示框左侧是过滤后的代码块列表，右侧是当前代码块的触发字符，来源，以及模板代码。



#### 3.3 Emmet支持 ####



web页面编辑器内嵌了emmet（即zencoding）插件。输入div#id1，按下tab，可以自动生成。Emmet的详细语法请查阅其官方网站emmet.io。  





#### 3.4 JQuery支持 ####



web页面编辑器内嵌了jquery插件，可以提示jquery语法。提示效果如下：  



<center>

![]((./image/jquery.png)   



</center> 



#### 3.5 标签和代码块智能提示配置 ####



标签可通过在窗口->首选项->iEOP->Html标签扩展里面进行编辑，可创建自定义标签提示。  



<center>

![]((./image/tagconfig.png)   



![]((./image/snippet.png)   



</center> 



高亮处为代码定义主体。 第一行单引号内为代码块显示标题，第二行trigger为代码块触发字符，第三行expansion为代码块主体。若想添加新的代码块，复制此处，粘贴在下行，并修改相应代码即可。


### 4 元数据设计器###
#### 4.1 产品概述
模型设计器作为实体模型、数据库模型的定义以及代码生成和脚本生成的工具，为业务系统中的领域模型的建立和基础代码的产生提供了一个完整的平台。业务分析和设计人员在建立领域模型时，其模型元素和模型设计器的实体操作等模型保持一致的描述方式，以保证领域模型顺利的建立和代码的顺利生成。
#### 4.2 关键特性
系统提供实体模型、数据库模型等定义功能

提供版本控制和权限特性

提供模型的代码生成和数据库表的脚本生成功能
#### 4.3 环境配置
从组件仓库下载元数据依赖的组件（maven依赖）。

<center>
![]((./image/metadata23.png)

![]((./image/metadata24.png)
</center> 
安装完成后，确保maven项目pom.xml文件有元数据组件。

如下代码段：

	<dependency>
      <groupId>com.yonyou.iuap</groupId>
	  <artifactId>metadata-jdbc</artifactId>
	  <version>2.0.1-SNAPSHOT</version>
	</dependency>
#### 4.4 界面功能分布
根据界面功能分布，MDP模型设计器有5个重要的组成部分，分别是元数据管理器、画布、工具面板、属性面板和模型视图。

<center>
![]((./image/metadata16.png)
</center> 

##### 4.4.1 元数据管理器
元数据管理器是提供元数据的相关管理工具，它支持元数据的创建、数据库导入实体组件、导入元数据bmf文件及删除元数据文件同时方便查看所有模型资源以及公共资源, 使我们能更清楚、更直观地查看。
管理器的文件系统结构是按树形方式展开，反映组件的树型组织关系：
<center>
![]((./image/metadata25.png)

</center> 
###### 4.4.1.1 新建实体组件
创建元数据bmf文件。
<center>
![]((./image/metadata26.png)
</center>
###### 4.4.1.2 数据库导入实体组件
支持从数据导入实体组件。
<center>
![]((./image/metadata27.png)
</center>
###### 4.4.1.3 导入模型文件
支持导入元数据bmf文件。
###### 4.4.1.4 删除
删除元数据bmf文件
##### 4.4.2 画布
模型设计器是一个图形化的工具，画布工具便于使用者进行类图建模的绘制。使用者从工具面板中拖动相应元素到画布类图中创建实体、枚举、值对象等。并可对类图中的对象进行直接增、删、改操作。

并且在画布类图中，选定类图中对象后点击鼠标右键，可以进行导入属性、发布元数据、发布元数据（忽略版本）、删除发布元数据、生成java源代码、导出pdm(.xml)文件等功能。上述操作的详细说明将在元数据典型应用章节中进行阐述。
##### 4.4.3 工具面板
实体组件工具面板上用户通过拖拽的方式，在画布上创建实体组件、创建枚举、创建业务接口、创建注释以及创建关联关系。
##### 4.4.4 属性面板
属性面板主要是在设计修改模型时，为使用者提供实时查性和设置当前所选定对象的基本属性的工具。

在面板的右上角有快捷应用功能按钮 ![]((./image/metadata22.png)， 如下是对各按钮功能的描述：

![]((./image/metadata21.png)[属性视图图钉功能]，选中后，固定当前选择对象，在使用者点击其它对象时，属性视图不随之改变；

![]((./image/metadata18.png)[显示类别]，选中后，属性视图将按属性类型的方式排列展示；

![]((./image/metadata19.png)[显示高级属性]，选中后，属性视图将显示高级属性；

![]((./image/metadata20.png)[恢复缺省值]，选中后，恢复当前选择对象的属性的缺省值。
##### 4.4.5 模型视图
在模型视图界面中可以对实体若干属性进行新增、修改和删除操作，还可以实现业务和属性映射。介绍实体属性时会具体说明。
#### 4.5 创建组件
##### 4.5.1 创建实体
###### 4.5.1.1 实体属性
实体可以有若干属性和操作，还可以实现接口。

<center>
![]((./image/metadata1.png)

</center>     
具体实体各属性

实体中属性的设置要点如下：

类型样式：目前支持Single、REF、LIST三种。

SINGLE 单一样式，最终的类型就是原始数据类型。

REF 引用样式，只用于实体，值对象，设置为引用样式，便可以得到引用类型。

LIST 列表样式类最终的类型为List<数据类型> 集合类型。

类型：可以自行选择，当建立实体间关系时，也会自动设置；主键一定要设置为ID类型。

目前元数据支持如下基本类型：String, Integer, BigInteger, MEMO, Double, Boolean, Date, Timestamp, Time, BigDecimal, ID, Money, BLOB, CLOB,CUSTOM,MULTILANGTEXT,IMAGE,FREEDOM,CONVERSIONRATE等。

字段名称：生成数据库表列的名称。

隐藏： 是否隐藏。

空：是否可以为空。

扩展标签：
1）cacheable标识此实体进行缓存处理。
2）自由配置供二次开发使用。
###### 4.5.1.2 实体的特性
实体的特性是从各种各样不同的实体中提取出来的一些共同的有特点的属性，比如说单据主实体上一定会有单据号，单据日期等。利用实体的特性，可以方便地构造出具有某些属性的实体，降低开发人员的工作量。

开发人员有两种方式来得到实体的特性：

1.可以通过修改iUAP Studio\iuap\metadata\Features文件夹下的xml文件来增加新的特性，其中特性文件名为Features_模块名；

2.开发人员亦可通过导出特性的方法来导出特性，过而获得特性。

<center>
![]((./image/metadata2.png)

导出特性 点击后可以进入如下界面：

![]((./image/metadata3.png)

特性界面

其中特性名称为该特性的显示名称。点击next后会进入选择要导出的特性的界面，选择要导出的特性，点击完成。

![]((./image/metadata4.png)

选择特性

</center>    
###### 4.5.1.3 实体间关系
目前元数据的关系支持关联、组合。

关联，属性的类型样式是REF，在代码中生成的是一个String。

组合，属性的类型样式是LIST，在代码中生成的是一个list集合。

<center>
![]((./image/metadata11.png)

实体间关系

</center>

设置关系的注意事项：

关系中必须设置源属性。

设置了关系后，属性的类型便会发生变化，但删除关系后，属性的类型不会恢复，务必要检查。另外，修改过带有关系的属性后，需要重新设置关系（即重新拉线）。

注意：对于组合关系，子实体中不需要指向主实体的外键属性，这是业务模型而不是数据库模型，在元数据发布时会自动在数据库中为子表加上外键。外键列的名称就是源属性（在上图中即为“订单”实体中的“订单明细”属性）对应的字段名称，所以建议将源属性对应的字段名称设为所期望的子表对应主表的外键名称。

如果实体是从PDM导入的，则务必按照注意事项修改模型。

<center>
![]((./image/metadata12.png)

简单实体

</center>

简单VO简部全部为简单字段，与其它实体无任何关系，该实体除了客户类型为枚举类型，其它字段均为基本类型，和其它实体没有任何关系。

这是最简单的一种类型，依照实体默认产生数据库表,表名可以在设计器上指定，字段和实体属性保持一致即可，字段名也可以在设计器上设置。

<center>
![]((./image/metadata13.png)

一对一关联

</center>

一个实体一对一关联了另一个实体，且在产生的JAVA类里关联源字段为字符串类型，而不是被关联实体的类型，我们把这种关联称之为关联，称关联源字段的数据类型为引用类型。

比如客户关联了地区，客户里有一个字段叫[客户所在地区]，称为关联源字段，如果是引用关联，则产生的客户JAVA类里，关联源字段为String类型，记录的是地区的主键ID。

<center>
![]((./image/metadata14.png)

一对多组合

</center>

对于一对多组合，保存时除了保存主实体，还要保存被组合的子实体，删除时也一起删除，查询时提供全部查询和只查主实体对象。
##### 4.5.2 创建业务接口
<center>
![]((./image/metadata5.png)

业务接口

</center>
在设计器上，业务接口只能增加属性，相应会生成get方法，比如增加一个name属性，会生成一个getName()方法，方法的返回值可以自由选择。实际上，如果希望灵活运用业务接口，你可以摆脱设计器的限制，你在设计器上设计出一个业务接口，生成代码后，可以给业务接口增加任何方法，当然实现类也由你自己实现，此时只一通过元数据来管理你的业务接口而已。

业务接口的实现类可以分为三种情况，优先级从高到低排列如下：

1.实体和特定业务接口连线上的实现类

<center>
![]((./image/metadata6.png)

实体实现接口连线

</center>

2.实体上注册的实现类

<center>
![]((./image/metadata7.png)

实体注册实现类

</center>

3.业务接口上注册的实现类

<center>
![]((./image/metadata8.png)

业务接口注册实现类

</center> 

<center>
![]((./image/metadata9.png)

根据映射关系自动生成

</center> 
##### 4.5.3 创建枚举
<center>
![]((./image/metadata10.png)

创建枚举类型

</center>

创建一个枚举类型时，要注意以下几点：

枚举类型必须设置返回值类型，当前支持String和Integer两种

#### 4.5 元数据典型应用
##### 4.5.1 元数据发布
元数据发布的最小单元是组件。选中某个组件，或者在画布中点击右键，即可发布元数据。

元数据发布分为两种发布方式：1.发布元数据。2.发布元数据（忽略版本）。

<center>
![]((./image/metadata15.png)

发布元数据

</center>

注意事项：

必须保存后才能发布

发布时会一起发布被依赖的组件，支持双向依赖，循环依赖。

如果发布元数据时忽略版本，则完全以本地的模型文件为准，可能造成库中新版本的模型被覆盖，非特殊情况不推荐使用。
##### 4.5.2 删除发布的元数据
删除已发布在数据库中的元数据。
##### 4.5.3 导出java代码
发布元数据后，在设计器上右键->导出java源代码可以导出java代码
##### 4.5.4 导出sql脚本
发布元数据后，在设计器上右键->导出sql脚本

脚本带有实体建表语句及扩展表建表语句（ext_+原实体表名）。
##### 4.5.5 导出PDM文件
如果当前文件夹下有同名的pdm，会分析PDM文件中的外键信息.并添加到新生成的PDM文件中。

### 5. 模版引擎
iUAP-Studio 提供模版引擎同时支持预置模版和用户自定义模版。模版引擎让用户不仅仅是使用者，还是创造者，赋予用户自主优化开发过程的能力。 
#### 5.1 代码块/控件模版
studio初始安装后，打开html页面，左侧工具栏
#### 5.2 页面模版
#### 5.3 代码生成模版



### 6. 组件仓库