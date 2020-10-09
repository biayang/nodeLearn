# 在node js中输出excel文件 

## 简单教程链接如下
https://segmentfault.com/a/1190000020142427

__在代码中引入模块__
```
const fs = require('fs');
const nodeXlsx = require('node-xlsx');
```
__数据填充__
```
	const mainData = [['指标', '结果']];
	const mainSheet = { name: 'main', data: mainData };

	mainData.push(
		['subject', output['subject']],
		['activeBet', output['activeBet']],
		['activeTotalBet', output['activeTotalBet']],
		['loopCount', output['loopCount']],
		['TotalCost', output['TotalCost']],
		['TotalWin', output['TotalWin']],
		[],
		['RTP', output['RTP']],
		['Base RTP', output['Base RTP']],
		['Base Win', output['Base Win']],
		['Base Hits', output['Base Hits']],
		['Base Hit Frequency', output['Base Hit Frequency']],
		[],
		['FreeSpin RTP', output['FreeSpin RTP']],
		['FreeSpin Win', output['FreeSpin Win']],
		['FreeSpin Number', output['FreeSpin Number']],
		['FreeSpin Trigger Frequency', output['FreeSpin Trigger Frequency']],
		['FreeSpin Retrigger Frequency', output['FreeSpin Retrigger Frequency']],
		[],
		['JackPot HIT', output['JackPot HIT']],
		['JackPot RTP', output['JackPot RTP']],
		['JackPot RTP In Base', output['JackPot RTP In Base']],
		['JackPot RTP In Free', output['JackPot RTP In Free']],
		['', '次数', 'RTP'],
		['JackPot Mini', output['JackPot Level Count'][1], output['JackPot Map'][1]],
		['JackPot Minor', output['JackPot Level Count'][2], output['JackPot Map'][2]],
		['JackPot Major', output['JackPot Level Count'][3], output['JackPot Map'][3]],
		['JackPot Grand', output['JackPot Level Count'][4], output['JackPot Map'][4]],
	);

	const symbolSheet = { name: 'symbol', data: data.symbolData };
	const wildSheet = { name: 'wild', data: data.wildData };
```

__生成excel文件__
```
fs.writeFileSync(`./simulationRes/simRes-${Date.now()}-${output['subject']}.xlsx`, nodeXlsx.build([mainSheet, symbolSheet, wildSheet]));
```
