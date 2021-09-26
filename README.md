# 天目流椰羊AmenomaCocogoat

一个究极缝合怪，拼接了天目Amenoma和椰羊cocogoat，用于对原神圣遗物识别、过滤和自动上锁解锁。

---

# 功能

- 基于Amenoma的圣遗物自动识别
- 基于Cocogoat的圣遗物展示、过滤
- 基于Amenoma的圣遗物自动加锁解锁

# 使用流程

- 使用Amenoma扫描圣遗物。操作与原版相同，使用窗口模式运行原神，进入圣遗物界面，管理员权限启动Amenoma，点击开始扫描等待结束。
- 使用Cocogoat展示处理圣遗物数据。打开Cocogoat，如果已经打开请点击左上角更新圣遗物信息。**未更新前在Cocogoat对圣遗物进行任何操作会导致Amenoma生成的数据被覆盖，请务必更新后操作或运行完毕Amenoma后再打开Cocogoat。** Cocogoat和原版相比是增量更新，原版所有功能。圣遗物界面按钮包括：
  - 更新圣遗物信息：重新读取圣遗物数据，未关闭Cocogoat的情况下运行Amenoma后必选
  - 导出：和Cocogoat相同，可导出莫娜占卜铺、原魔计算器、GOOD数据
  - 操作：下拉菜单包含：全部选择、全部不选、加锁已选、解锁已选。其中在过滤状态下全选只会选中过滤出的圣遗物
  - 过滤：点击展开过滤界面。可设置过滤圣遗物的部位、套装、等级、星级、主词条、副词条，支持多选。关于过滤逻辑见下
  - 添加：原版功能，添加一个新的圣遗物
  - 清空/删除选中：清空所有圣遗物/删除选中圣遗物
  - 识别：Cocogoat的OCR识别，使用识别框，同样支持自动加锁解锁，但是识别速度和准确率比Amenoma略低，不想两个工具切换可以用此
  - 圣遗物：每个圣遗物包含三种操作
    - 右上...：编辑圣遗物，在圣遗物识别出错时可以修改。**由于新增、加锁、解锁均通过OCR识别决定，即使识别错误，如果修改了圣遗物数据会导致无法和识别结果匹配，如果用于加锁解锁请勿修改圣遗物数据。**
    - 右下锁标记：更改圣遗物锁状态，锁定圣遗物或解锁圣遗物。状态会实时更新到存储文件中，供Amenoma自动枷锁解锁
    - 其他位置：点击后即选择/不选择该圣遗物
- 在Cocogoat中调整圣遗物加锁解锁状态后，回到Amenoma，将"获取游戏锁状态并保存"换为"将圣遗物锁同步至游戏"。**进入游戏圣遗物界面，加锁解锁任意圣遗物。如果出现已锁定此装备的弹窗提示，勾选不再提示并关闭弹窗。** 点击开始扫描等待结束。

# 过滤逻辑

过滤界面如下：

WIP

其中部位、套装、等级、星级、主词条为复选菜单，不选时不使用该数据过滤，选择后过滤满足所选项的圣遗物。

对于副词条，有想包含的副词条和不想包含的副词条两种。如果留空则不用于过滤。以想包含的副词条为例：

- 最少包含条数：最少包含多少条所列的副词条。例如选择了攻充爆爆最少条数3，那么这四条中至少包含三条的圣遗物才会被过滤出来
- 添加想包含副词条：按钮位于窗口最下方，点击后添加新的一个副词条筛选数据
- 副词条：包含四部分，副词条名称、判断方式、数值、删除。名称选择副词条名，判断方式有`> < =`等，数值为数值阈值，删除为删除该副词条。**这里名称中的攻击力、防御力、生命值同时指代百分比数据和数字数据，并通过数值栏有无百分号区分。** 例如只想选攻击力百分比，数值需要输入`x%`；想同时包含防御力和防御力百分比，需要写两条`防御力 > 0, 防御力 > 0%`。

不想包含的副词条和上述类似，不同在于：最多包含条数，圣遗物副词条最多只能包含多少条不想包含的副词条。添加不包含副词条，添加新的一条不想包含的副词条。

# 开发

Amenoma和Cocogoat完全独立，均基于原版配置二次开发。二次开发代码分支为[Amenoma-lock](https://github.com/zyr17/Amenoma/tree/lock)和[cocogoat-feat/artifact-lock](https://github.com/zyr17/cocogoat/tree/feat/artifact-lock)。

# 存在问题和待改进

- 由于需要识别圣遗物后才能决定是否加锁解锁，魔改版Amenoma相比原版扫描速度降为原版的约二分之一
- 目前不会保存过滤配置，不同过滤配置需要手动重新输入
- Amenoma和原版相比文件大小大幅上升，正在尝试减小体积
- 未支持中文以外的语言
