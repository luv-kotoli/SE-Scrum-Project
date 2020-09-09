### 项目名 ： Scrum Board
### 项目架构： 三层BS架构
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
      
      3. 对于每个角色：在项目中的每一个角色都可以查看项目的进度，但对于项目每个部分的操作权限/编辑权限不同
         1. Product Owner， PO 
            + PO可以在主界面通过添加按钮添加User Story，在弹出的窗口中，可以对User Story的预计时间，功能描述进行编辑，添加之后User Story被放入Product Backlog。
            + PO可以通过拖动Product Backlog中的User Story来改变User Story的放置顺序，以代表User Story的优先级。
            + PO可以通过点击接收（Accept）按钮与拒绝（Reject）按钮来决定是否接受用户提出的需求，并在点击Reject后弹出窗口，写明拒绝的理由。
         
         2. Client
            + Client可以通过主界面向PO提交新需求，添加方式可以类似PO添加User Story的方式。需求提交后，此需求只显示在PO的Product Backlog中，并在需求后显示接收（Accept）与拒绝（Reject）两个按钮
         
         3. Scrum Master， SM
            + SM可以在Home界面创建一个新的组件Sprint，在创建时设置其起止时间
            + SM可以将Product Backlog中的User Story拖入/复制进To Do List中，但不可更改Product Backlog中的User Story顺序（优先级）
            + 每天早晨站立会议结束后，SM负责将前一日的每个User Story的进度更新到Sprint中
         
         4. Scrum Team， ST
            + ST可以将To Do List中的User Story拖入当前的Sprint中，并点击User Story旁的Start按钮表示任务开始，同时此User Story会更新到In Progress List中
            + 每天早晨站立会议结束后，对于在自己项目中出现的Bug，通过添加一个Bug Story添加到当前的Sprint，并且同时此Bug Story会更新到In Progress List中
            + 每天早晨站立会议结束后，如果有需要对项目进行的环境优化、项目部署准备等项目外Story，通过添加一个Technical Story到这个Sprint。**这些Story并不会对Sprint的进度造成影响，也不会被更新到In Progress List中
         
        
