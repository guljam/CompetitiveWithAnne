# **L4D2 AnneHappy Rework Update log**
# **L4D2 AnneHappy Rework 更新记录**

## **更新记录:**

### ** 2022年11月更新记录**
#### 前言
新插件包的目的是为了更快的获取上游更新，降低我的维护成本，当第一版本插件完成后，我的更新就只需要更新特感等功能性插件
其他的插件来源于上游的更新，可以更专注于**摸鱼**
社区插件的更新能够得到马上的同步
#### 插件更新记录
- ai_tank2.sp 增加了梯子检测功能，并且删除了tank后退动作的连跳处理，修复了tank可能会纵云梯大跳的问题
- ai_jockey_new.sp 修复了猴子被推后马上就能通过使用跳跃功能来恢复重新使用技能导致的问题
- infected_control.smx 将5种模式的4种刷特合并为1个插件处理，
					   适配目标选择插件，选择生还者构建刷特坐标系的时候不能选目标已满的玩家
					   特感的生成顺序改为由队列进行处理，解决一波可能刷同样的特感[主要是boomer和spitter]的问题
					   原来的射线刷特方法取消，改为获取"logic_script"的值来判断[也还是射线处理，但是效率比原来快，而且效果更好]
					   检测env_physics_blocker的阻拦属性，原来不能生成的地方现在很大可能也能生成了
					   射线类型改变，由MASK_NPCSOLID_BRUSHONLY类型更改为MASK_PLAYERSOLID，能最大程度上增加可刷特位置
					   修复原来刷特IsPlayerStuck的射线过滤器的bug，会导致新版插件把射线改为MASK_PLAYERSOLID后导致的卡在新加的物件上
					   倒地玩家的视线不会影响特感的传送(相当于倒地生还视线不如狗）
					   增加最大刷特距离的控制
- server.smx 分开为2个插件join.smx 和 server.smx，其中join.smx主要处理加入游戏后换队的问题，server.smx处理Anne等模式下特殊的一些功能
- l4d_target_override.smx 升级为最新版本，增加了targeted功能，能限制生还者被选为目标的数量
- SI_Target_limit.smx 目标选择插件适配新版l4d_target_override插件，自动控制控制型特感选相同生还者为目标的数量
- vote.smx 投票cfg插件增加cvar来控制投票文件
- l4d2_Anne_stuck_tank_teleport.smx 救援关不启用跑男惩罚
- text.smx插件会进行Cvar的检测，一次来避免插件加载顺序导致的无法启动的问题
- rpg.smx 增加皮肤功能，且增加自动检测依赖启用不同功能的能力,修复关闭帽子无法保存到数据库的问题
- specrates, hextags, rpg, l4d_hats,l4d2_item_hint.smx ,veterans增加检测积分插件的功能，没有积分插件也不影响使用
- l4d2_weapon_attributes.smx 增加霰弹枪装填速度的Cvar控制，需要WeaponHandling作为前置插件(加载顺序无影响)
- 对抗插件全部更新最新版本，部分插件改用i18n汉化，英语汉语翻译都有(具体汉化插件和i18n汉化请看项目)
- AnneHappy、AnneHappyPlus枪械uzi削弱
当前版本武器伤害具体如下
[AnneHappy](https://github.com/fantasylidong/CompetitiveWithAnne/blob/master/cfg/vote/weapon/AnneHappy.cfg)
[AnneHappyPlus](https://github.com/fantasylidong/CompetitiveWithAnne/blob/master/cfg/vote/weapon/AnneHappyPlus.cfg)
[ZoneMod](https://github.com/fantasylidong/CompetitiveWithAnne/blob/master/cfg/vote/weapon/zonemod.cfg)

#### 一些重要特感和生还数据：
生还者速度：220
坦克速度： 225
坦克连跳加速度： 60
坦克停止距离： 135
坦克近战攻击距离： 75
小僵尸数量：z_common_limit 24 (大于原AnneHappy的21只，小于zonemod的30只）
被胖子喷产生的小僵尸数量： 1个 13 2个 25 3个35 4个45
尸潮发生时同时存在的小僵尸数量： 45 （大于原AnneHappy的50只，小于zonemod的50只）
其他不太重要数据请在对应模式的shared_cvars.cfg文件
特感增强的数据在对应模式的shared_settings.cfg文件

#### 性能问题
当前刷特版本不多人运动情况下，开20T服务器依旧在90帧以上，最小帧1%也在60帧以上
但是一旦超过4人，20T根本就无法稳定了，8人运动基本在12~14T能基本在90帧以上，最小帧1%在50以上
以上性能测试为r5 3900x 测试，云服高特情况可能还要打个7折起步
综上，正常情况下刷特应该已经不成为性能瓶颈，6人运动腾讯轻量云服12t基本达到瓶颈（预估）

#### 结论
目前版本的难度还是相当大的，4特带一个新手的压力都不小，5特带一个新手难度就比较大了，6特带一个新手不靠卡克基本很难通过c2
所以建议新手玩家多玩玩4，5特之后再去6特混野
各个服主也可以根据自己喜好设置不同的难度，大部分的都可以通过控制Cvar来控制难度
部分可能需要源码的，所有源码也已经开源，其中AnneHappy为主的插件在scripts/AnneHappy/文件夹
拓展性为主的插件在scripts/extend/文件夹
如果发现有问题，请发issue

### 2022年11月6日更新记录
#### 刷特插件infected_control.smx
- 修改传送时生成位置错误的逻辑
- 增加sdkcalls限制[默认5个]，这个参数很多特的时候消耗比较大，谨慎添加更多！这个代表最多5只特感可以进入传送找位流程，以后可能不会单独用sdkcall处理传送，会先处死，然后进入传送队列，放到ongameframe中处理
#### ai_tank_2.smx插件
- tank插件优化了梯子处理逻辑，将在生还者出安全区的时候遍历所有entity找到所有梯子实体，保存好梯子的起始位置，去除高度的影响下来判断距离，距离小于150的就处在梯子附近，tank将无法锁定视角
#### l4d2_Anne_stuck_tank_teleport插件
- 新版本的可见函数对于tank无效，改回原来的逻辑
#### 结构优化
- 多人模式将共用annehappy模式的shared_cvar.cfg和shared_plugins.cfg
- 单人模式将共用alone模式的map_cvar
- 卸载大部分annehappy不需要的插件
- server的网络参数设置将只应用与annehappy比赛模式，对抗的网络参数强制使用cfg/confogl_rates.cfg文件，对抗原来的gamemode参数已经加到confogl_personalize.cfg，原来的对抗模式参数anne.vpk基本已经删除完
#### 特感加智插件
- 特感处于stargger状态下不进行操作
#### server_name插件
- 服务器名插件模式检测更改为对l4d_ready_cfg_name cvar的检测，不再使用sv_tags处理，适配对抗的readyup插件名字设置
#### join插件
- 增加了服务器核心插件自动更新功能，不过还是建议多看看插件包是不是有更新
#### 插件汉化
- 不少插件增加汉化显示
#### 地图修改
- 部分同步上游地图参数导致牢房减弱，修改回来
#### confoglcompmod.smx
- 防打服狗，我在这个插件增加了平时服务器默认隐藏的参数，有人加载模式后就会删除隐藏，如果高防服务器可以修改源码重新编译一下，等打服狗死了我会用自动更新把这个插件修改为正常
- 还有一些小修复，具体看[commit log](https://github.com/fantasylidong/CompetitiveWithAnne/commits/master)
#### advertisement.smx
- 不同模式的广告文本加载不同
#### vote.cfg
- 支持不同模式选用不同的投票cfg文件

### 2022年11月10日更新记录
#### 刷特插件infected_control.smx
- 修复刷特插件传送出现问题
#### ai_tank_2.smx插件
- 修复delete handle产生的报错
- 修改梯子检测方式
#### survivor_mvp
- 删除团灭更换模式
#### userhook.smx
- 拓展测试插件增减usermessage hook 插件
#### confoglcompmod.smx
- 已经取消隐藏的处理
还有一些小修复，具体看[commit log](https://github.com/fantasylidong/CompetitiveWithAnne/commits/master)
#### versus_coop_mode.smx
对抗模式玩战役，完美修复，谢谢[钵钵鸡大佬](https://github.com/umlka/) 倾力支持
PS：这种处理方式相比原来的换成写实处理有以下几点好处
- 永远是对抗模式地图，比如c5m3会一直是pathA，而且对抗的梯子或者nav修复都存在
- hunter的属性会为对抗属性，原来的改为写实处理第二回合会导致hunter变为战役属性，会使hunter特别难爆
- 可以更改回合重启时间，加快坐牢速度（建议改为1，太低了玩家能在包被删除前偷包）
- 回合结算时能看到整章节的数据，谁偷懒一目了然


### 2022年11月17日更新记录
#### 刷特插件infected_control.smx
- 修复一个位置多刷引起的刷很多同种类特感问题，跑男针对模式
#### hitstatic survivor_mvp l4d_stats
- 更改灭团处理方式，新的versus_coop_mode引起
#### l4d2_script_hud 插件
- 如果tank或者witch不生成，不显示他的进度为固定，而是直接不显示，Static改为固定，进度加上%分号
#### ai_jockey_new更新
- 进攻性更强
#### ai_hunter_new更新
- 顺便可以开启无蓄力hunter
#### join插件
- 增加自动更新插件开关
#### SI_Target_limit
- 适配刷特插件的跑男针对
#### L4D2 Weapon Attributes
- 同步上游更新，去除l4d2_smg_reload_tweak.smx
#### 其他 
- 救援关全部关闭流程克，只启用第一个事件克，三方图使用server插件更改，同步上游fix更新，单人模式传送时间改为默认3秒

### 2022年11月30日更新记录
#### mapinfo更改
- 官图增加很多阴间位置tank的流程ban，同步上游对抗的map和stripper更新
#### ai_jockey_2
- 猴子更改为树树子猴子2.0，修了一点bug，削弱了猴子一部分属性
#### ai_boomer_2
- 胖子更改为树树子胖子2.0
#### specrates
- 修复4人旁观情况下30w积分玩家没有100tick旁观问题
#### l4d2_stats
- 修复因提出特感导致的ht血量错误的问题
#### server
- 增加团灭次数显示
#### rpg
- 恢复因新版coop_base_versus模式引起的每回合白嫖资格消失，增加被黑伤害显示插件
#### l4d_boss_vote
- tank位置投票增加限制，8特以下需要团灭5次才能投票（管理员免疫）
#### infected_control
- 刷特插件传送距离改为动态的，防止部分地方600距离找不到刷新位置导致刷特进程卡住

### 2022年12月8日更新记录

#### infected_control插件
- 删除传送最小距离Convar，传送最小距离和生成最小距离一样，为了增加传送进程的特感生成速度，把特感传送当前距离改为每tick增加20距离快速找位置(生成为每tick增加5距离）
- 增加一个Native（float GetNextSpawnTime()），提供下一次特感生成时间，方便其他插件调用
- 修复1vht和witchparty模式可能少特的问题

#### text插件
- 适配新版infected_control插件，增加狡猾tank的开启关闭显示

#### join插件
- 增加踢出家庭共享账户的功能，需要SteamWorks拓展
- 增加大厅自动删除的Convar

#### specrates插件
- 修改旁观插件的分数插件依赖处理不正确的问题

#### ai_jockey_2插件
- 修改jocker2的一些设置，减低向后跳概率，增加高跳概率

#### l4d_boss_vote插件
- 修复9特以上无法投票的功能

#### 其他
增加大量对抗插件的i18n翻译

