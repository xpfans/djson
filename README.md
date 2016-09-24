<p align="center">
<img 
    src="assets/logo.png" width="240" height="78" border="0" alt="DJSON">
<br/><br/>
<a href="https://godoc.org/github.com/a8m/djson"><img src="https://img.shields.io/badge/api-reference-blue.svg?style=flat-square" alt="GoDoc"></a>
<a href="https://travis-ci.org/a8m/djson"><img src="https://img.shields.io/travis/a8m/djson.svg?style=flat-square"
alt="Build Status"></a>
<a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square" alt="LICENSE"></a>
</p>

DJSON is a JSON decoder for Go that is ___3~ times faster___ than
the standard `encoding/json` and the existing solutions, when dealing with
arbitrary JSON payload. [See benchmarks below](#benchmark).  
It is a good approach for people who are using `json.Unmarshal` together
with `map[string]interface{}`, don't know what the schema is, and still
want good performance with minimal changes.

### Motivation
While searching for a JSON parser solution for my projects, that is faster than the standard library, with zero reflection tests, allocates less memory and is still safe(I didn't want the `"unsafe"` package in my production code, in order to reduce memory consumption).  
I found that almost all implemtations are just wrappers around the standard library
and aren't fast enough for my needs.  
I encountered two projects: [ujson](https://github.com/mreiferson/go-ujson) that is the UltraJSON implementation
and [jsonparser](https://github.com/buger/jsonparser), that is a pretty awesome project.  
ujson seems to be faster than `encoding/json` but still doesn't meet my requirements.  
jsonparser seems to be really fast, and I even use it for some of my new projects.  
However, its API is different, and I would need to change too much of my
code in order to work with it.  
Also, for my processing work that involves `ETL`, changing and setting new
fields on the JSON object, I need to transform the `jsonparser`
result to `map[string]interface{}` and it seems that it loses its power.

### Advantages and Stability
As you can see in the [benchmark below](#benchmark), DJSON is faster and allocates less
memory than the other alternatives.  
The current version is `1.0.0-alpha.1`, and I'm waiting to hear from you
if there are any issues or bug reports, to make it stable.  
(comment: there is a test file named `decode_test` that contains a [test case](https://github.com/a8m/djson/blob/master/decode_test.go#L104) that
compares the results to `encoding/json` - feel free to add more values if you find they are important)  
I'm also plaining to add the `DecodeStream(io.ReaderCloser)` method, to support stream decoding
without breaking performance.



