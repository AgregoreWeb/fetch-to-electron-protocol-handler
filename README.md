# fetch-to-electron-protocol-handler
Generate electron protocol handlers from lazy-loaded fetch API handlers

Refactored from the [Agregore Browser](https://github.com/AgregoreWeb/agregore-browser)

## Usage

```javascript
const fetchToHandler = require('fetch-to-electron-protocol-handler')
const {protocols, session} = require('electron')

const {handler} = fetchToHandler(getFetch, session.defaultSession)

protcols.registerStreamProtocol('example', handler)

async function getFetch() {
 // Asynchronously initialize your `fetch()` function
 // This is where you can set up your p2p nodes
 // Note that the initializing will happen on the initial invocation
 return async function fetch({url, ...opts}) => {
   const convertedURL = new URL(url)
   url.protocol = 'https:'

   return globalThis.fetch(convertedURL.href, opts)
 }
}
```
