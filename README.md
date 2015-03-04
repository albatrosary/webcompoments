Web Compoments
============

# Custom Elements

https://developer.mozilla.org/en-US/docs/Web/API/Document/registerElement
http://www.html5rocks.com/ja/tutorials/webcomponents/customelements/

```JavaScript
var Mytag = document.registerElement('my-tag');
document.body.appendChild(new Mytag());
var mytag = document.querySelectorAll("my-tag")[0];
mytag.textContent = "I am a my-tag element.";
```

```index.html
<my-tag></my-tag>
```
を定義していた場合
```JavaScript
var mytag = document.querySelectorAll("my-tag")[0];
mytag.textContent = "I am a my-tag element.";
```
カスタムエレメントにプロパティにメソッドを追加する
```JavaScript
var XFoo = document.registerElement('x-foo', {
  prototype: Object.create(HTMLElement.prototype, {
    bar: {
      get: function() { return 5; }
    },
    foo: {
      value: function() {
        alert('foo() called');
      }
    }
  })
});
document.body.appendChild(new XFoo());
var mytag = document.querySelectorAll("x-foo")[0];
mytag.bar
> 5
mytag.foo()
> メッセージボックスが表示される
```
