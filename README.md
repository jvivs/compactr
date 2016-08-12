# Kompactor
*A compression library for the modern web*

[![Kompactor](https://img.shields.io/npm/v/kompactor.svg)](https://www.npmjs.com/package/kompactor)
[![Build Status](https://travis-ci.org/fed135/kompactor.svg?branch=master)](https://travis-ci.org/fed135/kompactor)
[![Dependencies Status](https://david-dm.org/fed135/kompactor.svg)](https://www.npmjs.com/package/kompactor)
[![Code Climate](https://codeclimate.com/github/fed135/kompactor/badges/gpa.svg)](https://codeclimate.com/github/fed135/kompactor)
[![Gitter](https://img.shields.io/gitter/room/fed135/kompactor.svg)](https://gitter.im/fed135/kompactor)

---

## What is this and why does it matter?

Kompactor is a library to compress and decompress Javascript objects before sending them over the web. It's immencely usefull for web applications that use sockets a lot. Smaller payloads equals better, faster throughput and less bandwidth costs.


## Aren't there any other libraries out there that do this?

Yes, yes there are. Like [msgpack](http://msgpack.org/), [snappy](https://google.github.io/snappy/) and [protocol-buffers](https://developers.google.com/protocol-buffers/).


## Then why make another one, isn't Protobuf like... the best thing?

Why yes, Protocol Buffer is by far the better performing protocol out there, but there's a few things about it I don't like - as a Node developper. 

The first thing that comes to mind is the painful management of `.proto` files.

Not only are they overly complex, they are also written in a different markup, which makes dynamic generation or property probing a bit of a hassle. Not to mention that you have to maintain parity across services of these messages that are more often than not a copy of your data Models. (See [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself))


## So what's your solution?

Protocol Buffers are awesome. Having schemas to deflate and inflate data while maintaining some kind of validation is a great concept. Kompactor's goal is to build on that to better suite Node server developement and reduce noise by allowing you to re-use your current Model schemas.


## Examples, please.

For example, if you have a DB schema for users, you can use that directly as a schema for Kompactor.

```
/* Waterline Schema (User) */

{
  id: {
    type: 'integer',
    required: true
  },
  name: {
    type: 'string',
    defaultsTo: 'John'
  }
}

``` 

```
/* User compessing in controller */

const Kompactor = require('kompactor');

User.create({ id: 0, name: 'Bruce' })
  .then(user => Kompactor.encode(User, user))
  .then(deflated => /* Send encoded User */);

``` 

```
/* Decoding the User data */

let user = Kompactor.decode(User, deflated);

```


## Can that be used for Websockets too?

Oh yes, via webpack!

`npm run build`

Will generate browser-ready code!


## What about Node compatibility

You need Node 6.0.0 and up


## What about performances?

See this chart:


## Alright, what about features?

In the near future, you will be able to:

[ ] Use Waterline schemas
[ ] Synchronously encode/decode
[ ] Asynchronously encode/decode (Promise-based)
[ ] Stream encoding-decoding

## Alright, I'm convinced! How can I help?

Just open an issue, identifying it as a feature that you want to tackle.
Ex: `STORY - [...]` 
And we'll take the discussion there. 
