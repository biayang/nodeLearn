# 配置
## slot_config目录下
+ `machine_list.json` 中添加机器
+ `subject_tmpl_list` 中添加机器special配置
+ `extra_config` 中可添加复杂的机器权重配置，根据机器实现需求自行决定
## 工程目录/tools目录
- `download_table.json` 中添加reel,pay_line, pay_table等机器相关配置的google doc id
***
# 代码
## game-server/app/slot/
- machine目录下添加新机器类，`SlotMachineMan.js`中添加对应工厂方法
- analyser为结果分析器代码: 
    - `NormalPanelAnalyser` 标准line类型机器结果分析器
    - `HighestWinPanelAnalyser` 第一列包含wild时的line类型机器结果分析器
    - `MultiWayPanelAnalyser`  MultiWay机器结果分析器
    - `DoubleWayMultiWayPanelAnalyser` 左右双向MultiWay机器结果分析器
    - `NewClassicPanelAnalyser` 经典机器结果分析器
    - `HighestClassicPanelAnalyser` wild在第一行的经典机器结果分析器
- extra目录为enter_free协议参数工厂方法
- roomInfo目录为enter_room协议参数工厂方法
- spinInfo目录为SpinPanel的extraInfo的参数工厂方法
- special目录为解析 subject_tmpl_list 中机器special配置 的工厂方法
- store目录为机器存入redis的special data工厂方法        
## SpinPanel字段详解见 game-server/app/slot/entity/SpinPanel.js中
- 需要用户选择Freespin次数的Freespin 需在对应机器的extraInfo中添加isEnterFreeSpin字段标记, 对应的store目录的机器data中也需要添加
- 需要用户触发Claim的Feature 需在对应机器的extraInfo中添加isEnterBonusGame字段标记, 对应的store目录的机器data中也需要添加
- `game-server/app/slot/protocol/C2SClaimFeature.js` 需要Claim的Feature调用该协议
- `game-server/app/slot/protocol/C2SEnterFreeSpin.js` 需要Claim的FreeSpin调用该协议
