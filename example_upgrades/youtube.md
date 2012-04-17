# youtube

Implements the _youtube_ command.
<pre>
:youtube url
</pre>
This upgrade requires the _panes_ upgrade. When a user enters the youtube command,
all participants will open a new pane that embeds a YouTube video.

## Command
```
:upgrade {"type":"upgrade","name":"youtube","markup":"","style":"youtube-pane-body img {\ndisplay: block;\nwidth: 80%;\nmargin: 10px auto;\n}\n","script":"(function() {\n  function hash(str) {\n      for (var i=0,h=0,l=str.length; i<l; i++) h = (((h<<5)-h)+str.charCodeAt(i))|0; \n      return Math.abs(h); \n    }\n\n  chat.os.addInputHandler( renderYouTube, 5 );\n\n  function renderYouTube( message, next ) {\n    if ( message.type != 'youtube' ) return next();\n    return chat.os.pane( 'youtube-'+hash(message.text), message.text, render);\n\n    function render( id, type, div ) {\n      if ( type != 'open' ) return;\n      var iframe = document.createElement('iframe');\n      iframe.setAttribute('class', 'youtube-player');\n      iframe.setAttribute('type', 'text/html');\n      iframe.setAttribute('width', '640');\n      iframe.setAttribute('height', '385');\n      iframe.setAttribute('src', message.text);\n      iframe.setAttribute('frameborder', '0')\n      div.appendChild( iframe );\n    }\n  }\n})();\n"}
```

## Style
```css
.youtube-pane-body iframe {
  display: block;
  width: 80%;
  margin: 10px auto;
}
```

## Script
```javascript
(function() {
  function hash(str) {
      for (var i=0,h=0,l=str.length; i<l; i++) h = (((h<<5)-h)+str.charCodeAt(i))|0; 
      return Math.abs(h); 
    }

  chat.os.addInputHandler( renderYouTube, 5 );

  function renderYouTube( message, next ) {
    if ( message.type != 'youtube' ) return next();
    return chat.os.pane( 'youtube-'+hash(message.text), message.text, render);

    function render( id, type, div ) {
      if ( type != 'open' ) return;
      var iframe = document.createElement('iframe');
      iframe.setAttribute('class', 'youtube-player');
      iframe.setAttribute('type', 'text/html');
      iframe.setAttribute('width', '640');
      iframe.setAttribute('height', '385');
      iframe.setAttribute('src', message.text);
      iframe.setAttribute('frameborder', '0')
      div.appendChild( iframe );
    }
  }
})();
```