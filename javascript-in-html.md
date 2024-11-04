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
