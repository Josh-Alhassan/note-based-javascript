# JavaScript in HTML

## The `<script>` Element

The primary method of inserting JavaScript into an HTML page is via the `<script>` element. This element was created by Netscape and first implemented in Netscape Navigator 2. It was later added to the formal HTML specification. There are siz attributes for the `<script>` element.

- `async` - Optional: Indicates that the script should begin downloading immediately but should not prevent other acttions on the page such as downloading resources or waiting for other scripts to load. Valid only for external script files.

- `charset` - Optional: The character set of the code specified using the `src` attribute. This attribute is rarely used because most browsers don't honor its value.

- `crossorigin` - Optional: Configres the CORS settings for the associated request; by default, CORS is not used at all. `crossorigin = "anonymous"` will configure the request for the file to not have the credentials play set. `crossorigin = "use-credentials"` will set the credentials flag, menaing the outgoing request will include credentials.

- `defer` - Optional. Indicates that the execution of the script can safely be deferred until after the document's content has been completely parsed and displayed. Valid for only external scripts. Internet Explorer 7 and earlier versions also allow for inline scripts.

- `intergirity` - OPtional: Allows for verification of subresources intergrity (SRI) by checking the retrieved resource against a provided cryptographic signature. If the signature of the retrieved resource does not match that specified by the attribute, the page will error and the scripts will not execute. This is usefful for ensuring that a Content Delivery Network (CDN) is not serving malicious payloads.

- `src` - Optional: Indicates an external file that contains code to be executed.

- `type` - Optional: Indicates the content type of the scripting language being used by the code block. Traditionally, this values has always been `"text/javaScript"`though deprecated. JavaScript files are typically served with `"application/x-javascripyt`. If the value is `module`, the code is treated as an **ES6** module and only then is eligible to use the `import` and `export` keywords.

## Tag Placement

Traditionally, all `<script>` element were placed within the `<head>` element on page, as in this example:

```
<!DOCTYPE html>
<html>
    <head>
        <title> Example HTML Page </title>
        <script src="app1.js"></script>
        <script src="app2.js"></script>
    </head>
    <body>
        <!-- Content Here >
    </body>
</html>
```

The main purpose of this format was to keep external file references, both CSS files and javaScript files, in the same area. However, including all JavaScript files in the `<head>` of a document means that all of the JavaScript code must be downloaded, parsed, and interpreted before the page begins rendering (rendering begins when the browser recieves the opening `<body>` tag). For pages that require a lot of JavaScript code, this can cause noticable delay in a page rendering, during which time the browser will be completely blank. For this reason, modern web applications typically include all JavaScript references in the `<body>` element, after the page content, as shown in this example.

```
<!DOCTYPE html>
<html>
    <head>
        <title> Example HTML Page </title>

    </head>
    <body>
        <!-- Content Here >
        <script src="app1.js"></script>
        <script src="app2.js"></script>
    </body>
</html>
```

Using this approach, the page is completely renderned in the browser before the JavaScript code is processed. The resulting user experience is percieved faster because the amount of time spent on a blank browser window is reduced.

## Deferred Scripts

The purpose of `defer` is to indicate that a script won't be changing the structure of a page as it executes. As such, the script can be run safely after the entire page has been parsed. Setting the `defer` attribute on a `<script>` element signals to the browser that download should begin immediately but execution should be deferred.

```
<!DOCTYPE html>
<html>
    <head>
        <title> Example HTML Page </title>
        <script defer src="app1.js"></script>
        <script defer src="app2.js"></script>
    </head>
    <body>
        <!-- Content Here >
    </body>
</html>
```

The HTML5 specification indicates that scripts will be executed in the order in which they appear.

The `defer` attribute is supported only for external script files.

**Note:** _For XHTML documents, specify the `defer` attribute as `defer = "defer"`. Also, they're other browsers that simply ignore this defer attribute and treat the script as it normally would. For this reason, it's still best to put deferred scripts at the bottom of the page._

## Asynchronous Scripts

HTML5 introduces the `async` attribute. The `async` attribute is similar to `defer` in that it changes the way the script is processsed. Also, similar to `defer`, `async` applies only to external scripts and signals the browser to begin downloading the file immediatly. Unlike `defer`, scripts marked as `async` are not guaranteed to execute in the order in which they're specified.

```
<!DOCTYPE html>
<html>
    <head>
        <title> Example HTML Page </title>
        <script async src="app1.js"></script>
        <script async src="app2.js"></script>
    </head>
    <body>
        <!-- Content Here >
    </body>
</html>
```

The purpose of specifying an `async` script is to indicate that the page need not wait for the script to be downloaded and executed befire continuing to load.

**Note** _For XHTML documents, specify the `async` attribute as `async ="async"`._

## Inline Code Versus External files

Although it's possible to embed JavaScript in HTML files directly, it's generally considered a best practice to include as much JavaScript as possible using external files. Keeping in mind thta there are no hard and fast rules regarding this practice, the argument for using external files are shown as follows:

> **Maintanability** - JavaScript code that is sprinkled throughout various HTML pages turns code maintainance into a problem. It is much easier to have a directory for all javaScript fiels so that developers can edit JavaScript code independent of the markup in which it is used.

> **Caching** - Browsers cache all externally linked JavaScript files according to specific settings. Menaing that if two pages are using the same file, the file is downloaded only once. This ultimately means faster page - load times.

One notable consideration when configuring how external files are requested is their implication on request bandwidth. With SPDY/HTTP2, the per-request overhead is substantially reduced in so far as it may be advantageus to deliver scripts to the client as light weight independent JavaScript components.

## Document Modes??
