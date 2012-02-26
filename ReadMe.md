# buffer-builder.js

BufferBuilder accumulates pieces of data into a buffer, appending each onto the end. The data can be Buffers, strings, a repittion of a byte, or any of the types such as UInt32LE or FloatBE that can be written into Buffers.

If you are thinking about using this, you should probably have considered streaming your data instead of putting it into a buffer.

## Usage

``` js
var BufferBuilder = require('buffer-builder');
var helloWorld = new BufferBuilder();

// Append a string, ascii encoded by default.
helloWorld.appendString('hello');

// Append any type that Buffer has read and write functions for.
helloWorld.appendUInt16LE(0x7720);

// Append a buffer
helloWorld.appendBuffer(new Buffer([111, 114, 108, 100]));

// Appended a repetition of a byte
helloWorld.appendFill(33, 3);

// Convert to an ordinary buffer
var buffer = helloWorld.get();

buffer.toString(); // hello world!!!
```

## API

# new BufferBuilder([initialCapacity])
Allocate an empty BufferBuilder. If you know approximately what size the Buffer will end up being and are trying to squeeze out more performance, you can set the initial size of the backing buffer.

# appendBuffer(source)

# appendUInt8(value)
# appendUInt16LE(value)
# appendUInt16BE(value)
# appendUInt32LE(value)
# appendUInt32BE(value)
# appendInt8(value)
# appendInt16LE(value)
# appendInt16BE(value)
# appendInt32LE(value)
# appendInt32BE(value)
# appendFloatLE(value)
# appendFloatBE(value)
# appendDoubleLE(value)
# appendDoubleBE(value)

# appendFill(value, count)
Append _count_ repetitions of _value_ (a byte).

# get()
Convert to a buffer. This is a deep copy; modifications to the returned buffer will not affect the BufferBuilder.

# copy(targetBuffer, [targetStart], [sourceStart], [sourceEnd])
Copy bytes from the BufferBuilder into _targetBuffer_. _targetStart_ and _sourceStart_ default to 0. _sourceEnd_ defaults to the BufferBuilder's length.

# length
Number of bytes appended so far.
