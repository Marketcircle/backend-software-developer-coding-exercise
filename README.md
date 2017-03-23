# Backend Software Engineer - Coding Exercise

Applicants for the Backend Software Developer role at [Marketcircle](https://www.marketcircle.com) must complete the following challenge, prior to an interview.

The purpose of this to have a base of discussion during an interview. We will both discuss your solution and your thoughts on the protocol and our architecture.

You are free to use a programming language of your choice.

Feel free to email [tbartlemess@marketcircle.com](mailto:tbartelmess@marketcircle.com) if you have any questions.


## Coding Exercise

We have a basic distributed Key-Value store. The communication occurs over a TCP protocol. Your job is to create a new client for the key value server, that and read and write values into the data store.

Please include a list of 2-5 keys you have written to the server and include the values of the following keys.

- `Daylite`
- `Marketcircle`

Please be aware that the server is open to everyone. Please do not sure personal or private information such as your name or E-Mail address.

### Server
The server is reachable at `interview.marketcircle.zone:9000`
### Protocol
- TCP binary protocol
- Commands are 8-byte strings
  + Pad with ASCII space (`0x20`) on the right side
- Argument values must be one of the following types, and encoded as specified:
  + Booleans
    * 1 byte
    * 0 for FALSE/NO
    * 1 for TRUE/YES
  + 8-bit unsigned integers
    * 1 byte
  + 64-bit signed integers
    * Use little endian byte ordering
  + Strings
    * UTF-8 encoded
    * Byte-length of the string should be encoded first, as a 64-bit integer
    * Do not include NULL terminators
  + Array (of Strings)
    * Array size should be encoded first, as a 64-bit integer
    * Then each string, in order

- Response values are encoded the same way as arguments
- Response always starts with a boolean indicating success/fail
- Failure responses include a message (string)

Command signatures:
```
HI!() -> () | (string reason)
COUNT() -> (int64_t count) | (string reason)
KEYS() -> (array<string> keys) | (string reason)
PUT(string key, string value) -> () | (string reason)
GET(string key) -> (string value) | (string reason)
DELETE(string key) -> () | (string reason)
```
