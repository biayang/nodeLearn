### 如果写了一个脚本，别人也想在本地使用，shell可以用 -d 判断当前路径
```
REPO="/www/slot/deploy/hydra/repo/test-t${ID}/game-server"
if [ -d "/Users/baiyang" ]; then
  REPO="/Users/baiyang/work/code/videoSlotSimulation/game-server"
fi
```
### js 中可以用下列方法
```
const host = 'Lux'

const os = require("os");
if (os.hostname() !== host) {
  console.log(`run in host "${host}" only`);
  return;
}
```
