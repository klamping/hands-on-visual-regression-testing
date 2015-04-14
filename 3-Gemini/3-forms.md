# Testing Forms

You can do more with Gemini than just hover over links. Since Gemini ties in to the browser, it can take browser based actions. 

Create a new file called ‘form.js’. In it, define your Gemini tests:
‘test’ 
```
var gemini = require('gemini');

gemini.suite('form actions', function(suite) {
    suite.setUrl('/layout-form.html')
        .setCaptureElements('#form1')
        .capture('plain')
        .capture('with text', function(actions, find) {
            actions.sendKeys(find('#text01'), 'hello gemini');
        });
});
```

Run your tests and view your output. You should see a new folder titled `form actions` and two screenshots, once that’s plain and one with the text you defined.

Take some time to read through [the full tests documentation](https://github.com/bem/gemini/blob/master/doc/tests.md) to discover all Gemini has beneath the hood.