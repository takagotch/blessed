### blessed
---
https://github.com/chjj/blessed

```
npm install blessed

telnet localhost 2300

tput.js setaf 2
tput.js sgr0
echo "$(tput.js setaf 2)Hello World$(tput.js sgr0)"
```

```js
var blessed = require('blessed');
var screen = blessed.screen({
  smartCSR: true
});
screen.title = 'my window title';

var box = blessed.box({
  top: 'center',
  left: 'center',
  width: '50%',
  height: '50%',
  content: 'Hello {bold}world{/bold}',
  tags: true,
  border: {
    type: 'line'
  },
  style: {
    fg: 'white',
    bg: 'magenta',
    border: {
      fg: '#f0f0f0'
    },
    hover: {
      bg: 'green'
    }
  }
});
screen.append(box);

var icon = blessed.image({
  parent: box,
  top: 0,
  left: 0,
  type: 'overlay',
  width: 'shrink',
  height: 'shrink',
  file: __dirname + '/my-program-icon.png',
  search: false
});
box.on('click', function(data){
  box.setContent('{center}Some different {red-fg}content{/red-fg}.{/center}');
  screen.render();
});

box.key('enter', funciton(ch, key){
  box.setContent('{right}Even different {black-fg}content{/black-fg}.{/right}\n');
  box.setLine(1, 'bar');
  box.insertLine(1, 'foo');
  screen.render();
});
screen.key(['escape', 'q', 'C-c'], function(ch, key){
  return process.exit(0);
});
box.focus();
screen.render();

table.setData([
  [ 'Animals', 'Foods' ],
  [ 'Elephant', 'Apple' ],
  [ 'Birds', 'Orange' ]
]);

table.setData([
  [ 'Animals', 'Foods' ], 
  [ 'Elephant', 'Apple' ],
  [ 'Bird', 'Orange' ]
]);

var layout = blessed.layout({
  parent: screen,
  top: 'center',
  left: 'center',
  width: '50%',
  height: '50%',
  border: 'line',
  style: {
    bg: 'red',
    border: {
      fg: 'blue'
    }
  },
  
  renderer: function(coords) {
    var self = this;
    
    var width = coords.xl - coords.xi
      , height = coords.yl - coords.yi
      , xi = coords.xi
      , xl = coords.xl
      , yi = coords.yi
      , yl = coords.yl;
      
    var rowOffset = 0;
    
    var rowIndex = 0;
    
    return function iterator(el, i) {
      el.shrink = true;
      
      var last = self.getLastCoords(i);
      
      if (!last) {
        el.position.left = 0;
        el.position.top = 0;
      } else {
        el.position.left = last.xl -xi;
        
        if (el.position.left + el.width <= width) {
          el.position.top = rowOffset;
        } else {
          rowOffset += self.children.slice(rowIndex, i).reduce(function(out, el){
            if (!self.isRendered(el)) return out;
            out = Math.max(out, el.lpos.yl - el.lpos.yi);
            return out;
          }, 0);
          rowIndex = i;
          el.position.left = 0;
          el.position.top = rowOffset;
        }
      }
      
      if (el.position.top + el.height > height) {
      }
    };
  }
});

for (var i = 0; i < 10; i++) {
  blessed.box({
    parent: layout,
    width: i % 2 === 0 ? 10 : 20,
    height: i % 2 === 0 ? 5 : 10,
    border: 'line'
  });
}

box.setContent('hello {red-fg}{green-bg}world{/bold}{/green-bg}{/red}');
box.setContent('hello {red-fg}{green-bg}world{/}');
box.setContent('hello {red-fg}{green-bg}{bold}world{/}');
box.setContent('hello {#ff000-fg}{#00ff00-bg}{/}');
box.setContent('hello {bold}world{/bold}');
box.setContent('hello\n'
  + '{right}world{/right}\n'
  + '{center}foo{/center}\n'
  + 'left{|}right');

box.setContent('here is an escaped tag: ' + blessed.escaped('{bold}{/bold}'));
box.setContent('here is an escaped tag: {open}bold{close}{open}/bold{close}');
{bold}{/bold}

box.on('click', function(mouse){
  box.setContent('You clicked ' + mouse.x + ', ' + mouse.y + '.');
  screen.render();
});
box.on('element click', function (el, mouse) {
  box.setContent('You clicked '
    + el.type + ' at ' + mouse.x + ', ' + mouse.y + '.');
  screen.render();
  if (el === box) {
    return false;
  }
});

var box = blessed.box({
  left: 'center',
  top: 'center',
  bg: 'yellow',
  width: '%50',
  height: '%50'
});

console.log(box.left);
console.log(box.top);

console.log(box.alert);
console.log(box.atop);

box.setContent('Hello {#0feqab-fg}world{/}.');
screen.render();

var screen = blessed.screen({
  cursor: {
    artificial: true,
    shape: 'line',
    blink: true,
    color: null
  }
});

var screen = blessed.screen({
  cursor: {
    artificail: true,
    shape: {
      bg: 'red',
      fg: 'white',
      bold: true,
      ch: '#'
    },
    blink: true
  }
});

var blessed = require('blessed');
var telnet = require('telnet2');
telnet({ tty: true }, function(client){
  client.on('term', function(teminal){
    screen.terminal = terminal;
    screen.render();
  });
  
  client.on('size', function(width, height){
    client.columns = width;
    client.rows = height;
    client.emit('resize');
  });
  
  var screen = blessed.screen({
    smartCSR: true,
    input: client,
    output: client,
    terminal: 'xterm-256color',
    fullUnicode: true
  });
  
  client.on('close', function(){
    if (!screen.destroyd){
      screen.destroy();
    }
  });

screen.key(['C-c', 'q'], funciton(ch, key){
  screen.destroy();
});

screen.on('destroy', function(){
  if (client.writable) {
    client.destroy();
  }
});

screen.data.main = blessed.box({
  parent: screen,
  left: 'center',
  top: 'center',
  width: '%80',
  height: '%90',
  border: 'line',
  content: 'Welcome to my server. Here is your own private session.'
});

screen.render();
}).listen(2300);

var screen = blessed.screen({ terminal: 'windows-ansi' });

var blessed = require('blessed');
var tput = blessed.tput({
  terminal: 'xterm-256color',
  extended: true
});
process.stdout.write(tput.setaf(4) + 'Hello' + tput.sgr0() + '\n');

var blesse = require('blessed')
  , program = blessed.program();
  
program.key('q', function(ch, key) {
  program.clear();
  program.disableMouse();
  program.showCursor();
  program.normalBuffer();
  process.exit(0);
});

program.on('mouse', function(data){
  if (data.action === 'mousemove') {
    program.move(data.x, data.y);
    program.bg('red');
    program.write('x');
    program.bg('!red');
  }
});
program.alternateBuffer();
program.enableMouse();
program.hideCursor();
program.clear();

program.move(1, 1);
program.bg('black');
program.write('Hello', 'blue fg');
program.setx((program.cols / 2 | 0) - 4);
program.down(5);
program.write('Hi again!');
program.bg('!black');
program.feed();
```


```
{
  fg: 'blue',
  bg: 'black',
  border: {
    fg: 'blue'
  },
  scrollbar: {
    bg: 'blue'
  },
  focus: {
    bg: 'red'
  },
  hover: {
    bg: 'red'
  }
}

style: {
  fg: 'blue',
  bg: 'black',
  bold: true,
  underline: false,
  blink: false,
  inverse: false,
  inverse: false,
  invisible: false,
  transparent: false,
  border: {
    fg: 'blue',
    bg: 'red'
  },
  scrollbar: {
    bg: 'blue'
  },
  focus: {
    bg: 'red'
  },
  hover: {
    bg: 'red'
  }
}

```
