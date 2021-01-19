`2020-01-19, Node.js Streams`

# Stream

A `stream` is an abstract interface on the stream module for streaming data in Node.js. The stream module is useful for creating new stream instances, but it is not necessary to consume streams. You can use existing streams or create new types of streams.

- Besides creating streams, this module has utility functions like `stream.pipeline()`, `stream.finished()`, `stream.Readable.from()`, and `stream.addAbortSignal()`.
- In v15, the `stream/promises` API was added as an alternative set of asynchronous utility functions for streams that return `Promise` objects rather than using callbacks. `require('stream/promises')` or `require('stream').promises`.

Streams operate exclusively on `strings` and `Buffer`, but it is possible to make streams work in `objectMode` when creating them, so they can use other JavaScript values (except `null`, which has a special purpose within streams).

Implementing an HTTP server with `http.createServer()` is an example of using streams without implementing the `require('stream')` interface directly.

- The main two arguments, `req` and `res` (`http.IncomingMessage` and `http.ServerResponse`) are readable and writable streams respectively, which means they expose methods like `write()`, `end()`, and the `EventEmitter` API.

## Buffering

Both `writable` and `Readable` streams will store data in a internal buffer, the amount of data depends on `highWaterMark` option during creation, which specifies _number of bytes_ or _total number of objects_ in `objectMode`.

- `Readable` streams buffer data when `stream.push(chunk)` is called, but if the data is not consumed using `stream.read()`, the buffer will eventually reach the `highWaterMark` threshold and the stream will stop buffering more data until the current buffer starts being consumed
  - Internally the stream will stop calling its `readable._read()` method, which is used to fill the read buffer.
- `Writable` streams buffer data when `stream.write(chunk)` is called, and calling `writable.write()` returns `true` is the buffer is below `highWaterMark` threshold, or `false` if reached or exceeded the threshold.
- Since `Duplex` and `Transform` are both `Readable` + `Writable`, they have **two** internal buffers which operate independently.
  - For example, `net.Socket` instances are `Duplex`, and can _read_ data from the socket _and write_ data to the socket, and can do so at different times and speeds, that's why each side needs an independent buffer.
  - You can retrieve internal buffers with `writable.writableBuffer` and `readable.readableBuffer`, but it's not recomended as they are advanced and undocumented.

The `stream` API, specially `stream.pipe()` have the goal of limiting the buffering of data to acceptable levels, so that sources and destinations of differing speeds don't overwhelm the available memory.
`highWaterMark` is a threshold, not a _limit_, it only dictates the amount of data that a stream buffers before it stops asking for more data, but it does not enforce a strict memory limit.

# Types of Streams

## Writable

Writable streams are an abstraction for a destination to which data is written.

Examples of `Writable` streams include:

- HTTP requests, on the client
- HTTP responses, on the server
- fs write streams
- zlib streams
- crypto streams
- TCP sockets
- child process stdin
- `fs.createWriteStream()`
- `process.stdout`, `process.stderr`
  Some of these examples are actually `Duplex` streams that implement the `Writable` interface.

All `Writable` streams implement the interface defined by the `stream.Writable` class, and follow the same fundamental usage pattern:

```javascript
const myStream = getWritableStreamSomehow();
myStream.write('some data');
myStream.write('some more data');
myStream.end('done writing data');
```

## Readable

Readable streams are an abstraction for a source from which data is consumed.

Examples of `Readable` streams include:

- HTTP responses, on the client
- HTTP requests, on the server
- fs read streams
- zlib streams
- crypto streams
- TCP sockets
- child process stdout and stderr
- `fs.createReadStream()`
- `process.stdin`
  All `Readable` streams implement the interface defined by the `stream.Readable` class.

It is recommended to choose _one_ method to consume `Readable` streams, and _never_ use multiple methods to consume a single stream, because it can lead to unintuitive behavior.

- `readble.pipe()` is the top choice for being easy to implement.
- Alternatives for more fine-grained control are `EventEmitter` API, `readable.on('readable')`/`readable.read()`, and `readable.pause()`/`readable.resume()`

### Reading Modes

- Flowing mode, data is read from the underlying system automatically and provided to an application as quickly as possible using events via the `EventEmitter` interface.
- Paused mode, the `stream.read()` method must be called explicitly to read chunks of data from the stream.

  - These two modes are an abstraction of the more complicated three internal states of `Readable` streams, which are `readable.readableFlowing === null || false || true`

- All Readable streams begin in paused mode but can be switched to flowing mode by:
  - Adding a `'data'` event handler.
  - Calling the `stream.resume()` method.
  - Calling the `stream.pipe()` method to send the data to a `Writable`.
- And can switch back to paused mode:

  - If there are no pipe destinations, simply call `stream.pause()` method.
  - If there are pipe destinations, then remove all pipe destinations.
    - Multiple pipe destinations may be removed with `stream.unpipe()` method.

`Readable` streams will not generate data until a mechanism to consume or ignore data is provided, but if the consuming mechanism is disabled, the `Readable` stream will attempt to stop generating data.

- For example, removing the `'data'` event will not pause a stream, and calling `stream.pause()` does not garantee a stream will remain paused if the destination asks for more data.

Also, `Readable` streams in flowing mode need a consumer, or the data will be lost.

- For example, calling `readable.resume()` without a listener in the `'data'` event.
  Lastly, adding a `'readable'` event handler makes the stream stop flowing, and only `readable.read()` can be used to consume data until the `'readable'` event is removed and the streams starts flowing again.

## Duplex and Transform streams

`Duplex` streams implement `Readable` and `Writable` interfaces, for example:

- TCP sockets
- zlib streams
- crypto streams

`Transform` streams are `Duplex` that transform data, so the output is in some way related to the input, for example:

- zlib streams
- crypto streams
