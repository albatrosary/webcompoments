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

#### エラーになるカスタムエレメント

```JavaScript
document.registerElement('my-tag');  // OK
document.registerElement('my-t-ag');  // OK
document.registerElement('my-t_ag');  // OK
document.registerElement('mytag');  // NG - see error_log1
document.registerElement('my_tag');  // NG
```

error_log1:
```
DOMException: Failed to execute 'registerElement' on 'Document': Registration failed for type 'mytag'. The type name is invalid.code: 12message: "Failed to execute 'registerElement' on 'Document': Registration failed for type 'mytag'. The type name is invalid."name: "SyntaxError"stack: "Error: Failed to execute 'registerElement' on 'Document': Registration failed for type 'mytag'. The type name is invalid.
↵    at Error (native)
↵    at <anonymous>:2:10
↵    at Object.InjectedScript._evaluateOn (<anonymous>:777:140)
↵    at Object.InjectedScript._evaluateAndWrap (<anonymous>:710:34)
↵    at Object.InjectedScript.evaluate (<anonymous>:626:21)"__proto__: DOMException
```


error_log2:
```
DOMException: Failed to execute 'registerElement' on 'Document': Registration failed for type 'my_tag'. The type name is invalid.code: 12message: "Failed to execute 'registerElement' on 'Document': Registration failed for type 'my_tag'. The type name is invalid."name: "SyntaxError"stack: "Error: Failed to execute 'registerElement' on 'Document': Registration failed for type 'my_tag'. The type name is invalid.
↵    at Error (native)
↵    at <anonymous>:2:10
↵    at Object.InjectedScript._evaluateOn (<anonymous>:777:140)
↵    at Object.InjectedScript._evaluateAndWrap (<anonymous>:710:34)
↵    at Object.InjectedScript.evaluate (<anonymous>:626:21)"__proto__: DOMException
```
