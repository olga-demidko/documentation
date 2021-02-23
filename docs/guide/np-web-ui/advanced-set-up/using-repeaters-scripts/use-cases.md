# Use Cases
Below are some examples how you can use Repeater scripts during scanning of a local target.

### Sample HMAC Code
The following script provides an example of how to compute an HMAC authorization token. 

The example is taken from the [Amazon S3 documentation](http://s3.amazonaws.com/doc/s3-developer-guide/RESTAuthentication.html).

Suppose your AWS Access Key ID is `44CF9590006BF252F707`,  AWS Secret Access Key is `OtxrzxIsfpFjA7SwPzILwy8Bw21TLhquhboDYROV`, and authorization label is `AWS`.

The authorization token is a composite of a secure cryptographic algorithm, the AWS Access Key ID and a hash-encoded signature.

Then you could compute the authorization token as follows:

```js
const { createHmac } = require('crypto');
const { URL } = require('url');
const AWS_ACCESS_KEY_ID = '44CF9590006BF252F707';
const AWS_SECRET_KEY = 'OtxrzxIsfpFjA7SwPzILwy8Bw21TLhquhboDYROV';
const HEADER_PREFIX = 'x-amz'.toLowerCase();
const LABEL = 'AWS';
const handle = ({ method, url, headers, body }) => {
 // headers must be in lower-case
 const caseInsensitiveHeaders = Object.fromEntries(
   Object.entries(headers).map(([key, value]) => [key.toLowerCase(), value])
 );
 // x-amz headers must be sorted by header name
 const headersByPrefix = Object.entries(caseInsensitiveHeaders)
   .filter(([key]) => key.startsWith(HEADER_PREFIX))
   .map(
     ([key, value]) =>
       // The values of headers whose names occur more than once should be white space-trimmed and concatenated with comma separators to be compliant with section 4.2 of RFC 2616.
       `${key}:${
         Array.isArray(value) ? value.map((x) => x.trim()).join(',') : value
       }`
   )
   .sort();
 const normalizedUrl = url.replace(/\/$/, '');
 const { pathname } = new URL(normalizedUrl);
 const message = [
   method,
   caseInsensitiveHeaders['content-md5'],
   caseInsensitiveHeaders['content-type'],
   // You have to include the PREFIX-date header in your request and ignore date header
   !caseInsensitiveHeaders[`${HEADER_PREFIX}-date`]
     ? caseInsensitiveHeaders.date
     : undefined,
   ...headersByPrefix,
   pathname || normalizedUrl
 ];
 const signature = createHmac('sha1', AWS_SECRET_KEY)
   .update(message.join('\n'))
   .digest('base64');
 const authorization = `${LABEL} ${AWS_ACCESS_KEY_ID}:${signature}`;
 return {
   url,
   method,
   body,
   headers: {
     ...headers,
     authorization
   }
 };
};
exports.handle = handle;
```


Which results in a HTTP request, with headers which looks like this:


```js
{
 method: 'PUT',
 url: 'https://example.com/quotes/nelson',
 headers: {
   'Content-MD5': 'c8fdb181845a4ca6b8fec737b3581d76',
   'Content-Type': 'text/html',
   'Date': 'Thu, 17 Nov 2005 18:49:58 GMT',
   'X-Amz-Meta-Author': 'foo@bar.com',
   'X-Amz-Magic': 'abracadabra'
 }
}
```
The server response for this request will look like this:

```js
{
 url: 'https://example.com/quotes/nelson',
 method: 'PUT',
 body: undefined,
 headers: {
   'Content-MD5': 'c8fdb181845a4ca6b8fec737b3581d76',
   'Content-Type': 'text/html',
   Date: 'Thu, 17 Nov 2005 18:49:58 GMT',
   'X-Amz-Meta-Author': 'foo@bar.com',
   'X-Amz-Magic': 'abracadabra',
   authorization: 'AWS 44CF9590006BF252F707:jZNOcbfWmD/A/f3hSvVzXZjM2HU='
 }
}
```

### Sending Custom Values 
Sometimes you may need to provide the server with additional values to get access to the targets. Or you may need to to get the tokens of some specific headers. You can realize it by creating scripts with custom requests.

The following script is an example of how to apply host-specific static header tokens:

```js
const { URL } = require('url');
const HEADER_NAME = 'Some-Custom-Header';
const HOST_KEY_PAIRS = new Map()
 .set('sub-domain1.host.com', 'TOKEN_1')
 .set('sub-domain2.host.com', 'TOKEN_2')

const handle = ({ method, url, headers, body }) => {
 const { hostname } = new URL(url);
 const customHeaderValue = HOST_KEY_PAIRS.get(hostname);
 return {
   url,
   method,
   body,
   headers: {
     ...headers,
     ...(customHeaderValue ? { [HEADER_NAME]: customHeaderValue } : {})
   }
 };
};
exports.handle = handle;
```
