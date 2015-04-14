# Page Actions with Gemini

Capturing simple selectors is nice, but what about all the various states for links and buttons?

Thankfully Gemini allows us to easily chain these together

```
var gemini = require('gemini');

gemini.suite('style-guide', function(suite) {
    suite.setUrl('/style-guide.html')
        .setCaptureElements(['.site-header', '.site-branding'])
        .capture('plain')
        .before(function(actions, find) {
          this.link = find('.site-header ul li');
        })
        .capture('hovered', function(actions, find) {
          actions.mouseMove(this.link);
        })
        .capture('pressed', function(actions, find) {
          actions.mouseDown(this.link);
        })
        .capture('clicked', function(actions, find) {
          actions.mouseUp(this.link);
        });
});
```

Here we defined a `link` that we take actions upon. A list of [all the available actions exists on the Gemini website](https://github.com/bem/gemini/blob/master/doc/tests.md#available-actions).