# Starting with Gemini

Gemini is yet another visual regression tool and is quickly becoming my favorite. It's adaptable (runs via both PhantomJS and Selenium), has very nice documentation, and is built entirely in NodeJS.

Installation is also pretty simple, assuming you have Node and PhantomJS installed.

## Installation

```
npm install -g gemini
```

and then in your project directory

```
npm install gemini
```

## Setting up your config

Similar to Wraith, Gemini requires its own config file. Thankfully it's not much.

To get started, create a `.gemini.yml` file that contains just this:
```
rootUrl: http://localhost:8080/
```

Update the root url as you need, but that's all the config needs for our setup.

## Start a local phantom server

Gemini is built to run via either a Selenium or a PhantomJS server. Since setting up a Selenium server is more complicated, we'll just use Phantom.

Run this command from inside a terminal window:
```
phantomjs --webdriver=4444
```

If done correctly, it should output:
```
PhantomJS is launching GhostDriver…
[INFO  - 2015-04-14T02:23:37.939Z] GhostDriver - Main - running on port 4444
```

## Write your first test

Now that you have your config and Phantom server running, you should write a test to run on it. 

In a new file, add the following:

```
var gemini = require('gemini');

gemini.suite('style-guide', function(suite) {
    suite.setUrl('/style-guide.html')
        .setCaptureElements(['.site-header', '.site-branding'])
        .capture('plain');
});
```

This tells Gemini to go to the style guide url (based on the root url defined earlier). Then it defined the elements to capture screenshots of. Notice how we can list multiple elements.

The last bit tells Gemini to run a simple capture of those elements. 

## Gather your baseline

Now that you have your tests, it's time to gather your baseline. Save your test file as something like `styleguide.js`, then run your screenshot gather referencing that file:

`gemini gather styleguide.js`

You can see your screenshots in the ‘gemini' folder in your project. Notice how despite two selectors being defined, it's a single image. That's because Gemini will capture whatever is needed in order to get both elements in the picture. 

## Run your validation

Now that you've got your baseline, lets see if we can make out tests pass. Run the validation via:

`gemini test styleguide.js`

Hopefully you see:

`Total: 1 Passed: 1 Failed: 0 Skipped: 0`

## Extra Credit

While that default reporter is nice, the HTML reporter works better for me. To use that, add `--reporter html` to your command: 

`gemini test --reporter html styleguide.js`

The open the `gemini-report/index.html` file in a browser for a better overview of the changes. This makes it much easier to go through your results when you have several individual tests.
