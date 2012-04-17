# title

Implements the _title_ command.
<pre>
:title New window title
</pre>

## Command
```
:upgrade {"type":"upgrade","name":"youtube","markup":"","style":"","script":"(function() {\nchat.os.addInputHandler( renderTitle, 5 );\nfunction renderTitle( message, next ) {\n    if (message.type != 'title' ) return next();\n    document.title = message.text;\n    }\n})();\n"}
```

## Script
```javascript
(function() {
	chat.os.addInputHandler( renderTitle, 5 );
	function renderTitle( message, next ) {
    	if (message.type != 'title' ) return next();
    	document.title = message.text;
    }
})();
```
