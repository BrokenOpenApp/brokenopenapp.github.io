---
layout: post
title: Catching JavaScript errors
slug: javascript
created: 2015-06-29 12:00:00
---

For cross platform apps, it's common to run a WebView and code your app in HTML,
CSS and JavaScript.

When doing this, can you catch any JavaScript errors? Turns out you can.

Simply set up a JavaScript to Android bridge:

```
  webView.addJavascriptInterface(new WebViewInterface(), "ACRA");


	public class WebViewInterface  {

		@android.webkit.JavascriptInterface
		public void reportError(String message, String url, Integer lineNumber) {
			ACRA.getErrorReporter().handleException(new RuntimeException(
					"Javascript Error" + message + " in " + url + " on line " + lineNumber
			));
		}

	}
```

Then setup a handler in JavaScript:

```
    <script type="text/javascript">
      window.onerror = function(message, url, lineNumber) {
        ACRA.reportError(message,url,lineNumber);
        return false;
      };
    </script>
    <a onclick="doesnotexist.call(); return false;">Crash me now!</a>
```

And this error will now be logged to your server!

Of course, you can only catch errors from your own web pages with this. There may
be a way to catch errors from any page, but I haven't tested it yet.
