Q: What Unicode character does chr(0) return?
A: `x00`

Q: How does this character’s string representation (__repr__()) differ from its printed representation?
A: It's __repr__() is, `"'\\x00'"` and printed representation is `None`

Q: What happens when this character occurs in text?
A: For first case, it's `'this is a test\x00string'` and for second case, it doesn't get printed: `this is a teststring`

Q: What are some reasons to prefer training our tokenizer on UTF-8 encoded bytes, rather than UTF-16 or UTF-32? It may be helpful to compare the output of these encodings for various input strings.
A: Firstly, UTF-32 decides to give 4 bytes to each character, which means more memory, more computation for encoding / decoding, and if we were to train our tokenizer we would require similarly more memory, computation, hence this option is not a good choice. For comparing b/w UTF-8 and UTF-16, the target language in our case is english, and majority of the data is in english on internet, and UTF-8 gives you better compression ratio compared to UTF-16 thereby saving memory and computation cost while UTF-16 starts from two bytes and give better compression for multi-lingual language

Q: Consider the following (incorrect) function, which is intended to decode a UTF-8 byte string into a Unicode string. Why is this function incorrect? Provide an example of an input byte string that yields incorrect results
A: The string `आपको प्रणाम करता हूँ` doesn't work as an input to the function. It fails due to the fact that, one character can be more than one byte, and one character, i.e. 224 is a starting byte of multi-byte character.

Q: Give a two byte sequence that does not decode to any Unicode character(s)
A: bytes([224, 164]).__repr__()