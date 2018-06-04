# ksuid

A Node.js implementation of [Segment's KSUID
library](https://github.com/segmentio/ksuid). Supports Node.js 6, 8 and 10

## Installation

```console
$ npm install ksuid
```

## Usage

Require the module:

```js
const KSUID = require('ksuid')
```

### Creation

You can create a new instance synchronously:

```js
const ksuidFromSync = KSUID.randomSync()
```

Or asynchronously:

```js
const ksuidFromAsync = await KSUID.random()
```

Or you can compose it using a timestamp and a 16-byte payload:

```js
const crypto = require('crypto')
const yesterdayInMs = Date.now() - 86400 * 1000
const payload = crypto.randomBytes(16)
const yesterdayKSUID = KSUID.fromParts(yesterdayInMs, payload)
```

You can parse a valid string-encoded KSUID:

```js
const maxKsuid = KSUID.parse('aWgEPTl1tmebfsQzFP4bxwgy80V')
```

Finally, you can create a KSUID from a 20-byte buffer:

```js
const fromBuffer = new KSUID(buffer)
```

### Properties

Once the KSUID has been created, use it:

```js
ksuidFromSync.string // The KSUID encoded as a fixed-length string
ksuidFromSync.date // The timestamp portion of the KSUID, as a `Date` object
ksuidFromSync.timestamp // The raw timestamp portion of the KSUID, as a number
ksuidFromSync.payload // A Buffer containing the 16-byte payload of the KSUID (typically a random value)
```

### Comparisons

You can compare KSUIDs:

```js
todayKSUID.compare(yesterdayKSUID) // 1
todayKSUID.compare(todayKSUID) // 0
yesterdayKSUID.compare(todayKSUID) // -1
```

And check for equality:

```js
todayKSUID.equals(todayKSUID) // true
todayKSUID.equals(yesterdayKSUID) // false
```

### Validation

You can check whether a particular buffer is a valid KSUID:

```js
KSUID.isValid(buffer) // Boolean
```
