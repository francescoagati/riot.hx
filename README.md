# riot.hx

[![Join the chat at https://gitter.im/francescoagati/riot.hx](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/francescoagati/riot.hx?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
haxe wrapper around Riot.js

for install from git
```
haxelib git riot.hx https://github.com/francescoagati/riot.hx.git
```


in you code (see folder test for complete example)

haxe component
```
using riot.RiotTools;

@:tagName('counter')
@:templateFile('templates/counter/counter.html')
@:cssFile('templates/counter/counter.css')
@:autoMount
@:keep
class Component implements riot.IRiotComponent {
  public var view:Dynamic;


  @:bind function incr() {
    view.counter++;
  }

  @:bind function async_incr() {
    haxe.Timer.delay(function() {
      view.counter++;
      update();
    },2000);
  }

  function mount() {
    trace('component mounted on $root()');
    untyped console.log(root());
  }

  public function new(v,opts) {
    bind_view(v);
    view.counter = 0;
    view.on('mount',mount);
  }

}
```
your template riot
```
<button onclick={incr}>incr</button>
<button onclick={async_incr}>async incr</button>
<span class="counter">{counter}</span>
```

your template css injected during the definition of component
```
  .counter {
    background:red;
    color:yellow;
  }
```

in your html page
```
<html>
  <head>
    <script src="http://cdnjs.cloudflare.com/ajax/libs/riot/2.0.15/riot.min.js"></script>

  </head>
  <body>
    <counter></counter>
    <script src="test.js"></script>
  </body>
</html>
```

example with haxe code compiled to javascript
http://jsfiddle.net/ohtfow3z/1/
