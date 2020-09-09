### 项目名 ： Scrum Board
### 项目架构： 三层BS架构
### 项目目标： 
   1. 构建一个用于Scrum敏捷开发的实用性工具，并且通过对角色种类的管理，确保Client只能与PO之间有交流，PO只能与SM之间有交流，SM可以与PO与ST有交流
   2. 在线编辑软件，将软件开发的进度保存在数据库，用户之间通过特定项目进行连接。
   3. 实现几个常用小工具如燃尽图、User Story时间估算计算器等。

### 主要功能点：
   1. 用户的登录注册功能：主要包括用户的登录注册界面、后端登录注册实现代码以及前后端交互逻辑。
   
   2. 用户权限的管理： 
      + 用户的角色包括四种：客户（client），项目负责人（Product Owner，PO），Scrum经理（Scrum Master，SM），Scrum 团队成员（Scrum Team，ST）
      + 四种角色在注册与登录时无区别，只在进入特定项目后拥有特定的权限
      + 创建一个特定项目的人员被视为PO，PO有权限管理项目所涉及的人员：包括对项目涉及成员的加入（参考GitHub拉人加入Repository的方式），将各个人设定为特定角色（client，SM，ST）。**固定每种角色所具有的权限？**
   
   3. 主要界面功能：
      1. 在未选择项目前：
         + 显示一个空白的欢迎界面，包括页面顶部导航栏与左侧主菜单，可在欢迎那个界面添加项目介绍内容
         + 在顶部导航栏可点击选择项目菜单，在弹出的项目菜单中选择所要编辑的项目，例图如下：（Google Cloud 选择项目界面）
         
      2. 在选择项目之后：
         + 主界面采用多页面显示方式，主要包括**管理项目涉及人员界面（Members）,查看项目的燃尽图界面（Burn-down Chart），主界面（Home）及其他功能
         + 在确定选择项目后，直接显示主界面（Home）的内容
         + 主界面显示多列Srcum所需的组件，包括：Product Backlog, To Do List, In Progress List, Done List等，对于Sprint组件在下面叙述。每个组件在界面内均可拖动（这得算是额外的功能）
         
      3. 主界面组件：对于每个主界面的组件，均带有一个标题栏与内容列表
         + 对于Product Backlog，**只有PO对其拥有修改权限**，包括对User Story优先级的修改、用户需求的接受与否、User Story的添加等等，**应带有一个添加按钮**。
         + 对于To Do List，**只有SM对其具有修改权限**，主要功能为存放即将在Sprint中进行实现的User Story，列表内容来源与从Product Backlog -> To Do List的拖动。
         + 对于In Progress List, **无人对其具有修改权限，且无需修改**，主要功能为显示Sprint中正在进行中的User Story，Bug Story，在Sprint中的Story状态进行变动时，此列表自动更新
         + 对于Done List， **无人对其具有修改权限，且无需修改**， 主要功能为显示已经结束的User Story，Bug Story，在Sprint中的Story状态进行变动时，此列表自动更新
         + 对于Sprint列表，**SM通过其Home界面按钮进行添加，添加时标注Sprint的轮数，起始时间、持续时间（默认为一周）**，主要用来展示在当前Sprint中进行的Story。ST可将To Do List中的User Story拖入Sprint中，并且可以通过Sprint列表上的添加按钮添加Bug Story和Technical Story等。
         + 对于User Story，**最初由PO添加到Product Backlog中**，具有①未开始（To Do）状态，在此状态下，Story右侧会有一个Start按钮，当该Story被拖入Sprint列表中时，Start按钮变得可以点击。②当点击Start按钮后，User Story将变为正在进行状态（In Progress）,Story右侧有一个Finish按钮，右下角显示项目剩余的时间，在剩余时间减到0时，同时与此User Story相关的Bug Story全部被解决，User Story右侧的Finish变为可以点击，点击后此User Story被放入Done List。
         + 对于Bug Story/Technical Story，**由ST在sprint列表中创建**，Bug Story在创建时需附加在当前进行中的User Story上。两种Story创建后立即开始，且没有剩余时间，其中Bug Story会进入In Progress List 而Technical Story不会。
      
   4. 对于每个角色：在项目中的每一个角色都可以查看项目的进度，但对于项目每个部分的操作权限/编辑权限不同
      1. Product Owner， PO 
         + PO可以在主界面通过添加按钮添加User Story，在弹出的窗口中，可以对User Story的预计时间，功能描述进行编辑，添加之后User Story被放入Product Backlog。
         + PO可以通过拖动Product Backlog中的User Story来改变User Story的放置顺序，以代表User Story的优先级。
         + PO可以通过点击接收（Accept）按钮与拒绝（Reject）按钮来决定是否接受用户提出的需求，并在点击Reject后弹出窗口，写明拒绝的理由。
         
      2. Client
         + Client可以通过主界面向PO提交新需求，添加方式可以类似PO添加User Story的方式。需求提交后，此需求只显示在PO的Product Backlog中，并在需求后显示接收（Accept）与拒绝（Reject）两个按钮
         
      3. Scrum Master， SM
         + SM可以在Home界面创建一个新的组件Sprint，在创建时设置其起止时间 **设置一个创建Sprint按钮**
         + SM可以将Product Backlog中的User Story按顺序拖入/复制进To Do List中，不可更改Product Backlog中的User Story顺序（优先级）
         + 每天早晨站立会议结束后，SM负责将前一日的每个User Story的进度更新到Sprint中
         
      4. Scrum Team， ST
         + Sprint准备会议结束，ST中每个人的User Story分配完毕后，ST可以将To Do List中的User Story拖入当前的Sprint中，并点击User Story旁的Start按钮表示任务开始，同时此User Story会更新到In Progress List中。每日站立会议结束后，ST中每个人需要更新自己的User Story，减少所消耗掉的时间，剩余时间标注在Story右下角。
         + 每天早晨站立会议结束后，对于在自己项目中出现的Bug，通过添加一个Bug Story添加到当前的Sprint，并标注此Bug所出现在哪个User Story上。同时此Bug Story会更新到In Progress List中；当此Bug Story 被解决后，点击Bug Story旁的Finish按钮，在弹出窗口中简述解决方案后，此Bug将被放入Done List
         + 每天早晨站立会议结束后，如果有需要对项目进行的环境优化、项目部署准备等项目外Story，通过添加一个Technical Story到这个Sprint。**这些Story并不会对Sprint的进度造成影响，也不会被更新到In Progress List中**
         + 在自己负责的In Progress中的项目结束后，点击User Story旁的Finish按钮。如果与此项目相关的Bug已经全部解决，此User Story会被放入Done List
         
        
