PERCENT-ENCODING
================

What is this?
-------------

Percent-encoding is a library for
[percent-encoding](http://tools.ietf.org/html/rfc3986#section-2.1) defined in
[RFC 3986](http://tools.ietf.org/html/rfc3986) and varieties.

[RFC 3986](http://tools.ietf.org/html/rfc3986)で定義されている
[percent-encoding](http://tools.ietf.org/html/rfc3986#section-2.1)とその亜種を処
理するためのライブラリです。

License
-------

It's licensed under the MIT license.

Requirements
------------

* [Anaphora](http://common-lisp.net/project/anaphora/)
* [Babel](http://common-lisp.net/project/babel/)

API
---

### Encoding And Decoding

#### Function: encode string &key test www-form encoding

Encodes `string` to a percent-encoded string and returns the result.

`test` is used for determining whether each octet is allowed. If an octet is not
allowed, the octet is encoded. It's a function of one argument that returns a
generalized boolean. The default value is `#'unreservedp`.

If `www-form` is true, returns application/x-www-form-urlencoded string instead
of RFC 3986 percent-encoded string.

`encoding` is a character encoding scheme. `string` is encoded using the
encoding before percent-encoding. This argument is passed to
`babel:string-to-octets` without any change.

#### Function: decode string &key test www-form encoding

Decodes `string` to a decoded string and returns the result.

`test` is used for determining whether each octet is decoded. It's a function of
one argument that returns a generalized boolean. The default value is
`(constantly t)`.

If `www-form` is true, assumes that `string` is an
application/x-www-form-urlencoded string.

`encoding` is a character encoding scheme. `string` is decoded according to the
encoding after percent-decoding. This argument is passed to
`babel:octets-to-string` without any change.

### Predicates

#### Function: gen-delims-p x
#### Function: sub-delims-p x
#### Function: reservedp x
#### Function: alphap x
#### Function: digitp x
#### Function: unreservedp x
#### Function: userinfop x
#### Function: reg-name-p x
#### Function: pcharp x
#### Function: queryp x
#### Function: fragmentp x

Returns true if the octet `x` is a member of each character set. See RFC 3986.

Acknowledgements
----------------

The API of percent-encoding was inspired by Daniel Oliveira's
[do-urlencode](https://github.com/drdo/do-urlencode) and Franz's
[uri](https://github.com/franzinc/uri).

sile's [url](http://d.hatena.ne.jp/sile/20091216/1260980935) gave some important
hints for speed to me.
