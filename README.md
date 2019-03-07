BroadcastChannel polyfill
===================================

This is a polyfill for [BroadcastChannel](https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API).

**It is just a published copy of [Joshua Bell's gist](https://gist.github.com/inexorabletash/52f437d1451d12145264)**
(since [broadcast-channel polyfill](https://www.npmjs.com/package/broadcast-channel) won't work for our project).

It requires [Message Channel support](http://caniuse.com/#feat=channel-messaging), so should work in:

* Chrome 4+
* Safari 5+
* Opera 11.5+

Does not work in:

* Firefox 37- (neither BroadcastChannel nor MessageChannel)
* IE (??)

### Caveats ###
* The real API should let you transmit anything which can copied by the [structured cloning algorithm](https://html.spec.whatwg.org/multipage/infrastructure.html#structured-clone). This polyfill only copies things using `JSON.stringify()`/`JSON.parse()` so it is much more limited.
* This polyfill uses [DOM Storage](https://html.spec.whatwg.org/multipage/#toc-webstorage) (`localStorage`) and `storage` events. DOM Storage is a synchronous API and so may cause performance issues in pages. In addition, it is not exposed to Workers. Therefore, the polyfill will not function in Workers.
* Unique storage keys are used for each message, and are cleaned up a few hundred milliseconds after transmission. This is a total hack and may result in the messages failing to be received (if the write and delete are coalesced) or persisting (if the cleanup is prevented by page close).


