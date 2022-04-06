 Dialog组件
 
 setTimeout:
 
 setTimeout()方法设置一个定时器，该定时器在定时器到期后执行一个函数或指定的一段代码。
 
 1、参数:

function:是你想要在到期时间(delay毫秒)之后执行的函数。

code:这是一个可选语法，你可以使用字符串而不是function ，在delay毫秒之后编译和执行字符串 (使用该语法是不推荐的, 原因和使用 eval()一样，有安全风险)。

delay:这是一个可选语法，延迟的毫秒数 (一秒等于1000毫秒)，函数的调用会在该延迟之后发生。如果省略该参数，delay取默认值0，意味着“马上”执行，或者尽快执行。不管是哪种情况，实际的延迟时间可能会比期待的(delay毫秒数) 值长，原因请查看实际延时比设定值更久的原因：最小延迟时间。


2、返回值:

返回值timeoutID是一个正整数，表示定时器的编号。这个值可以传递给clearTimeout()来取消该定时器。

需要注意的是setTimeout()和setInterval()共用一个编号池，技术上，clearTimeout()和 clearInterval() 可以互换。但是，为了避免混淆，不要混用取消定时函数。在同一个对象上（一个window或者worker），setTimeout()或者setInterval()在后续的调用不会重用同一个定时器编号。但是不同的对象使用独立的编号池。


3、例子:
下文的例子在网页中设置了两个简单的按钮，以触发 setTimeout() 和 clearTimeout() 方法：按下第一个按钮会设置一个定时器，定时器在 2s 后显示一个警告对话框，并将此次 setTimeout 的定时器 ID 保存起来，按下第二个按钮可以取消定时器。

HTML
```
<p>Live Example</p>
<button onclick="delayedAlert();">Show an alert box after two seconds</button>
<p></p>
<button onclick="clearAlert();">Cancel alert before it happens</button>
```


JavaScript
```
var timeoutID;

function delayedAlert() {
  timeoutID = window.setTimeout(slowAlert, 2000);
}

function slowAlert() {
  alert('That was really slow!');
}

function clearAlert() {
  window.clearTimeout(timeoutID);
}
```


4、关于"this"的问题
当你向 setTimeout() (或者其他函数)传递一个函数时,该函数中的this指向跟你的期望可能不同，

因为由setTimeout()调用的代码运行在与所在函数完全分离的执行环境上。这会导致，这些代码中包含的 this 关键字在非严格模式会指向 window (或全局)对象，严格模式下为 undefined，这和所期望的this的值是不一样的。

！！！即使是在严格模式下，setTimeout()的回调函数里面的this仍然默认指向window对象， 并不是undefined。


