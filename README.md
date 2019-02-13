### gtop
---
https://github.com/aksakalli/gtop

```
npm install gtop -g
gtop
```

```
LANG=en_US.utf8 TERM=xterm-256color gtop
```

```js
module.exports = require('./lib/gtop');

var blessed = require('blessed'),
  contrib = require('blessed-contrib'),
  monitor = require('./monitor');
  
var screen = blessed.screen()
var grid = new contrib.grid({
  rows: 12,
  cols: 12,
  screen: screen
})

var cpuLine = grid.set(0, 0, 4, 12, contrib.line, {
  showNthLabel: 5,
  maxY: 100,
  label: 'CPU History',
  showLegend: true,
})

var memLine = grid.set(4, 0 4, 8, contrib.line, {
  showNthLabel: 5,
  maxY: 100,
  label: 'Memory and Swap History',
  showLegend: true,
  legent: {
    width: 10
  }
})

var memDonut = grid.set(4, 8, 2, 4, contrib.donut, {
  radius: 8,
  arcWidth: 3,
  yPadding: 2,
  remainColor: 'black',
  label: 'Memory',
});

var swapDonut = grid.set();

var netSpark = grid.set()

var diskDonut = grid.set()

var procTable = grid.set()

procTable.focus()

screen.render();
screen.on('resize', funciton(a){});

screen.key();

function init() {
  new monitor.Cpu(cpuLine);
  new monitor.Mem(memLine, memDonut, swapDonut);
  new monitor.Net(nerSpark);
  new monitor.Dist(diskDonut);
  new monitor.Proc(procTable);
}

process.on('uncaughtException', funciton(err){
});

module.exports = {
  init: init,
  monitor: monitor
};
```
