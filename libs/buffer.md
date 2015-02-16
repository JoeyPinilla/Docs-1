﻿
# Buffer
* [new](#buffer_new)
* [length](#buffer_length)
* [available](#buffer_available)
* [position](#buffer_position)
* [at](#buffer_at)
* [tostring](#buffer_tostring)
* [tohex](#buffer_tohex)
* [write](#buffer_write)
* [writebuffer](#buffer_writebuffer)
* [writestring](#buffer_writestring)
* [writebyte](#buffer_writebyte)
* [writebytes](#buffer_writebytes)
* [writeint8](#buffer_writeint8)
* [writeint16](#buffer_writeint16)
* [writeint32](#buffer_writeint32)
* [writeint64](#buffer_writeint64)
* [writefloat](#buffer_writefloat)
* [writedouble](#buffer_writedouble)
* [read](#buffer_read)
* [readbuffer](#buffer_readbuffer)
* [readstring](#buffer_readstring)
* [readbyte](#buffer_readbyte)
* [readbytes](#buffer_readbytes)
* [readuint8](#buffer_readuint8)
* [readint8](#buffer_readint8)
* [readuint16](#buffer_readuint16)
* [readint16](#buffer_readint16)
* [readuint32](#buffer_readuint32)
* [readint32](#buffer_readint32)
* [readuint64](#buffer_readuint64)
* [readint64](#buffer_readint64)
* [readfloat](#buffer_readfloat)
* [readdouble](#buffer_readdouble)



## buffer
The ``buffer`` library provides a way to easily read and write binary data.

	-- Create a new buffer
	local buffer = libs.buffer.new();



### buffer.new( [encoding] [,byteorder] )
Creates a new buffer (default UTF8 encoding and network byte order).

Supported encodings: ``ascii``, ``latin1``, ``latin2``, ``latin9``,
``utf8``, ``utf16``, ``utf32``, ``windows1250``, ``windows1251``, ``windows1252``.

Supported byte orders: ``le``, ``be``, ``network``, ``native``.

	local b1 = libs.buffer.new();
	local b2 = libs.buffer.new("utf16");
	local b3 = libs.buffer.new("utf8", "le");



### buffer:length( )
Returns the total length of the data in the buffer.

	local b = libs.buffer.new();
	b.writebyte(123);
	print(buffer:length()); -- 1



### buffer:available( )
Returns the length of unread data in the buffer.

	local b = libs.buffer.new();
	b.writebyte(123);
	print(buffer.available()); -- 1
	b.readbyte();
	print(buffer.available()); -- 0



### buffer:position( )
Returns the current position in the buffer.

	local b = libs.buffer.new();
	b:writebyte(123);
	print(b:position()); -- 0
	b:readbyte();
	print(b:position()); -- 1



### buffer:at( pos )
Returns the byte at the specified position (zero-index based).

	local b = libs.buffer.new();
	b:writestring("abc");
	print(b:at(0));  --  3
	print(b:at(2));  -- 'b' 98



### buffer:tostring( )
Returns a string representation of the buffer.

	local b = libs.buffer.new();
	b:writebytes(12, 34, 56);
	print(b:tostring()); -- [12,34,56]



### buffer:tohex( )
Returns a string hex representation of the buffer.

	local b = libs.buffer.new();
	b:writebytes(161, 178, 195);
	print(b:tostring()); -- [A1,B2,C3]



### buffer:write( raw )
Write raw data to buffer.

	local b = libs.buffer.new();
	b:write("abc");
	print(b:tostring()); -- [97,98,99]



### buffer:writebuffer( buffer )
Copies the data from another buffer.

	local a = libs.buffer.new();
	b:write("abc");

	local b = libs.buffer.new();
	b:writebuffer(a);
	print(b:tostring()); -- [97,98,99]



### buffer:writestring( str )
Writes a string using the specified encoding (length-prefixed).

	local b = libs.buffer.new("utf16");
	b:writestring("abc");
	print(b:tostring()); -- [6,97,0,98,0,99,0]



### buffer:writebyte( value )
Writes a single byte to the buffer.

	local b = libs.buffer.new();
	b:writebyte(123);
	print(b:tostring()); -- [123]



### buffer:writebytes( value )
Writes multiple bytes to the buffer.

	local b = libs.buffer.new();
	b:writebytes(12, 34);
	b:writebytes({ 56, 78 });
	print(b:tostring()); -- [12,34,56,78]



### buffer:writeint8( value )
Writes an 8-bit integer value.

	local b = libs.buffer.new();
	b:writeint8(123);
	print(b:tostring()); -- [123]



### buffer:writeint16( value )
Writes a 16-bit integer value.

	local b = libs.buffer.new();
	b:writeint16(123);
	print(b:tostring()); -- [0,123]



### buffer:writeint32( value )
Writes a 32-bit integer value.

	local b = libs.buffer.new();
	b:writeint32(123);
	print(b:tostring()); -- [0,0,0,123]



### buffer:writeint64( value )
Writes a 64-bit integer value.

	local b = libs.buffer.new();
	b:writeint64(123);
	print(b:tostring()); -- [0,0,0,0,0,0,0,123]



### buffer:writefloat( value )
Writes a 32-bit floating point value.

	local b = libs.buffer.new();
	b:writefloat(123.456);
	print(b:tostring()); -- [67,122,0,0]



### buffer:writedouble( value )
Writes a 64-bit floating point value.

	local b = libs.buffer.new();
	b:writedouble(123.456);
	print(b:tostring()); -- [64,111,64,0,0,0,0,0]



### buffer:read( [len] )
Read raw data from the buffer.

	local b = libs.buffer.new();
	b:write("abc");
	print(b:read(1)); -- a
	print(b:read());  -- bc



### buffer:readbuffer( [len] )
Read data from the buffer into a new buffer.

	local a = libs.buffer.new();
	a:write("abc");
	print(a:read(1)); -- a

	local b = a:readbuffer();
	print(b:tostring()) -- [98,99]



### buffer:readstring( )
Read a string using the specified encoding (length-prefixed).

	local b = libs.buffer.new();
	b:writestring("abc");
	print(b:readstring()); -- abc



### buffer:readbyte( )
Reads a single byte from the buffer.

	local b = libs.buffer.new();
	b:writebyte(123);
	print(b:readbyte()); -- 123



### buffer:readbytes( )
Read multiple bytes from the buffer.

	local b = libs.buffer.new();
	b:writestring("abc");
	print(b:readbytes()); -- [3,97,98,99]



### buffer:readuint8( )
Read unsigned 8-bit integer value.

	local b = libs.buffer.new();
	b:writeint8(250);
	print(b:readuint8()); --  250



### buffer:readint8( )
Read signed 8-bit integer value.

	local b = libs.buffer.new();
	b:writeint8(250);
	print(b:readint8()); --  -6



### buffer:readuint16( )
Read unsigned 16-bit integer value.

	local b = libs.buffer.new();
	b:writeint16(250);
	print(b:readuint16()); --  250



### buffer:readint16( )
Read signed 16-bit integer value.

	local b = libs.buffer.new();
	b:writeint16(250);
	print(b:readint16()); --  -6



### buffer:readuint32( )
Read unsigned 32-bit integer value.

	local b = libs.buffer.new();
	b:writeint32(250);
	print(b:readuint32()); --  250



### buffer:readint32( )
Read signed 32-bit integer value.

	local b = libs.buffer.new();
	b:writeint32(250);
	print(b:readint32()); --  -6



### buffer:readuint64( )
Read unsigned 64-bit integer value.

	local b = libs.buffer.new();
	b:writeint64(250);
	print(b:readuint64()); --  250



### buffer:readint64( )
Read signed 64-bit integer value.

	local b = libs.buffer.new();
	b:writeint64(250);
	print(b:readint64()); --  -6



### buffer:readfloat( )
Read a 32-bit floating point value.

	local b = libs.buffer.new();
	b:writefloat(123.456);
	print(b:tostring()); -- [67,122,0,0]



### buffer:readdouble( )
Read a 64-bit floating point value.

	local b = libs.buffer.new();
	b:writedouble(123.456);
	print(b:tostring()); -- [64,111,64,0,0,0,0,0]