# **AnneHappy 插件带上对抗插件包**
* 为了保持插件包结构和上游一样方便同步，这个插件包将不会带有nav修改文件和跳舞插件的模型与声音，~~AnneHappy的Nav修改文件请到我的[anne项目](https://github.com/fantasylidong/anne)中下载~~ 新解决方案，到[release页面](https://github.com/fantasylidong/CompetitiveWithAnne/releases)下载整合插件包，里面有
* 当前版本已经是进入stable模式，大部分核心插件更新可以通过join插件自动更新，不用那么频繁检测是否有更新了
* 如果没有数据库，建议下[release页面](https://github.com/fantasylidong/CompetitiveWithAnne/releases)里的norank版本或者nomysql版本
* norank版本是用电信服的rpg插件，只删除了排名，作弊检测和sourcebans插件，缺点就是每次进服务器需要自己设置出门近战，不想自己写了，有需求的写完可以pull request到我的项目里
* nomysql版本是删除了所有和数据库相关的插件


## **AnneHappy 会自动更新的核心插件**
- Path_SM/plugins/optional/AnneHappy/ai_boomer_new.smx"
- Path_SM/plugins/optional/AnneHappy/ai_boomer_2.smx"
- Path_SM/plugins/optional/AnneHappy/ai_charger_2.smx"
- Path_SM/plugins/optional/AnneHappy/AI_HardSI_2.smx"
- Path_SM/plugins/optional/AnneHappy/ai_hunter_new.smx"
- Path_SM/plugins/optional/AnneHappy/ai_smoker_new.smx"
- Path_SM/plugins/optional/AnneHappy/ai_spitter_new.smx"
- Path_SM/plugins/optional/AnneHappy/ai_jockey_new.smx"
- Path_SM/plugins/optional/AnneHappy/ai_jockey_2.smx"
- Path_SM/plugins/optional/AnneHappy/ai_tank_2.smx"
- Path_SM/plugins/optional/AnneHappy/infected_control.smx"
- Path_SM/plugins/optional/AnneHappy/text.smx"
- Path_SM/plugins/optional/AnneHappy/server.smx"
- Path_SM/plugins/optional/AnneHappy/witch_announce.smx"
- Path_SM/plugins/optional/AnneHappy/SI_Target_limit.smx"
- Path_SM/plugins/optional/AnneHappy/l4d_target_override.smx"
- Path_SM/plugins/optional/AnneHappy/l4d2_Anne_stuck_tank_teleport.smx"
- Path_SM/plugins/extend/join.smx"
- Path_SM/plugins/extend/server_name.smx"
- Path_SM/plugins/extend/l4d2_scripted_hud.smx"

## **关于新增模式:**

> **AnneHappy新加模式:**
* **AnneHappy 普通药役模式**
* **Hunters 1vHT模式**
* **AllCharget 牛牛冲刺大赛模式**
* **Witch Party模式** 
* **Alone 单人装逼模式**


---

## **重要内容**
* 其中Anne插件放到了optional/AnneHappy文件夹中，源码位于script/AnneHappy文件夹中
* 其中extend文件夹中的插件为电信服扩展所用，包括帽子、积分和商店娱乐等功能（默认启用）
* 本插件尽量在不影响Zonemod同步上游更新的基础进行更新（方便自己偷懒）
---

## **已知问题:**
* 小刀为TLS更新前的原版小刀
* ~~AnneHappy模式猴子有可能会将生还者传送到虚空【重要问题】，有临时修复，会在0.1s后将虚空的生还者传送回来，如果你找到问题是怎么发生的，请反馈一下，谢谢~~ 基本消失，但是不知道是后面怎么修改修复的
* AnneHappy模式过关统计会把这一章节所有统计信息全部记录，因为对抗模式每回合不会清除统计信息（原来的方式不能正确载入对抗地图和对抗的梯子和nav）【我觉得这是Feature不是Bug，笑，反正普通信息mvp插件能够正常记录了，所以也不准备修改了】
* ~~对抗原生的更换队伍不能用，使用join.smx插件进行换队(!inf !infected 感染 !jg !join 生还 !spec !afk旁观）~~ 已解决
* 删除了zonemod插件包新加的action拓展和l4d2_shove_fix插件，因为会造成药役模式sv剧烈波动，效果虽然不错，但是性能稳定性要求更高，所以删除

## **无数据库服务器安装问题:**
> 由于我的数据库不会对外放开，所以有些插件你需要删除或者自建数据库[数据库脚本在项目内]
- extend/l4d_stats.smx 积分插件，需要数据库，很多插件也依赖这个插件提供的积分，不过后面经过修改，这些依赖于这个积分插件的插件
也能在无积分插件情况下运行了
- chat-processor.smx 聊天语句处理插件，称号插件的前置插件
- extend/hextags.smx 称号插件 其中自定义称号需要rpg插件， 积分插件相互配合才能使用，无积分的情况下你可以直接去configs/hextags.cfg文件内增加自定义称号
- extend/lilac.smx 会保存检测记录到数据库l4d2_stats数据库
- extend/sbpp_******.smx sourcebans插件，方便进行所有服务器封禁
- extend/rpg.smx 商店插件，会自动检测依赖，没数据库也能用，或者你自己改用原来anne的，问题不大
- extend/chatlog.smx 数据库聊天记录插件
- extend/l4d_hats.smx 插件，最新帽子插件修改版，增加了数据库功能和forward处理，无积分插件也能使用，但是需要自己配置好l4d_hats配置
- extend/l4d2_item_hint.smx 标点插件，禁用了一部分功能，增加了光圈标点的聊天栏提示，也需要积分功能搭配限制，无积分插件也能使用
- disabled/specrate.smx 旁观30tick插件，更改后4人旁观数以内，30w积分的玩家也能100tick旁观，超过4人旁观，除管理员外其他旁观玩家一律30tick
- extendd/veterans.smx 时长检测插件，部分依赖于l4d_stats.smx插件的时长信息，能够自定义想玩游戏玩家的时长限制，不满足时长的，只能旁观，join.smx插件依赖这个插件提供是否是steamm组成员的信息
- extend/join.smx 玩家加入离开提示，换队作用，motd展示功能（不是组员会有提示，需要veterans插件作为前置）

## **Issue 发起说明**
请先阅读完README-AnneHappy-zh-cn.md后再发起任何issue
发起issue请进来仔细描述问题，最好能提供错误的log和怎么复现的，拒绝无效Issue
	
## **感谢人员:**

> **Foundation/Advanced Work:**
* morzlee 本分支创建者及维护者
* Caibiiii 原分支创建者
* HoongDou 原分支创建者
* Moyu 原分支创建者

> **Additional Plugins/Extensions:**
* GlowingTree880 特感能力加强的巨大贡献者
* umlka 完美解决了coop_base_versus问题
* fdxx 使用了一部分fdxx的插件

> **Competitive Mapping Rework:**
* Derpduck, morzlee 地图修改

> **Testing/Issue Reporting:**
* Too many to list, keep up the great work in reporting issues!
* 所有电信服玩家，因为没有时间游玩测试，大部分bug都是由他们反馈给我

**注意事项:** 如果你的作品被使用了，而我却忘了归功于你，我真诚地向你道歉。 
我已经尽力将名单上的每个人都包括在内，只要创建一个问题，并说出你所制作/贡献的插件/扩展，我就会确保适当地记入你的名字。
