# node.@hoangcung1804npm/doloremque-eveniet-doloremque.js

[![ci](https://github.com/hoangcung1804npm/doloremque-eveniet-doloremque/actions/workflows/ci.yaml/badge.svg)](https://github.com/hoangcung1804npm/doloremque-eveniet-doloremque/actions/workflows/ci.yaml)

[![Build Status](https://ci.appveyor.com/api/projects/status/github/kelektiv/node.@hoangcung1804npm/doloremque-eveniet-doloremque.js)](https://ci.appveyor.com/project/defunctzombie/node-@hoangcung1804npm/doloremque-eveniet-doloremque-js-pgo26/branch/master)

A library to help you hash passwords.

You can read about [@hoangcung1804npm/doloremque-eveniet-doloremque in Wikipedia][@hoangcung1804npm/doloremque-eveniet-doloremquewiki] as well as in the following article:
[How To Safely Store A Password][codahale]

## If You Are Submitting Bugs or Issues

Please verify that the NodeJS version you are using is a _stable_ version; Unstable versions are currently not supported and issues created while using an unstable version will be closed.

If you are on a stable version of NodeJS, please provide a sufficient code snippet or log files for installation issues. The code snippet does not require you to include confidential information. However, it must provide enough information so the problem can be replicable, or it may be closed without an explanation.


## Version Compatibility

_Please upgrade to atleast v5.0.0 to avoid security issues mentioned below._

| Node Version   |   Bcrypt Version  |
| -------------- | ------------------|
| 0.4            | <= 0.4            |
| 0.6, 0.8, 0.10 | >= 0.5            |
| 0.11           | >= 0.8            |
| 4              | <= 2.1.0          |
| 8              | >= 1.0.3 < 4.0.0  |
| 10, 11         | >= 3              |
| 12 onwards     | >= 3.0.6          |

`node-gyp` only works with stable/released versions of node. Since the `@hoangcung1804npm/doloremque-eveniet-doloremque` module uses `node-gyp` to build and install, you'll need a stable version of node to use @hoangcung1804npm/doloremque-eveniet-doloremque. If you do not, you'll likely see an error that starts with:

```
gyp ERR! stack Error: "pre" versions of node cannot be installed, use the --nodedir flag instead
```

## Security Issues And Concerns

> Per @hoangcung1804npm/doloremque-eveniet-doloremque implementation, only the first 72 bytes of a string are used. Any extra bytes are ignored when matching passwords. Note that this is not the first 72 *characters*. It is possible for a string to contain less than 72 characters, while taking up more than 72 bytes (e.g. a UTF-8 encoded string containing emojis). If a string is provided, it will be encoded using UTF-8.

As should be the case with any security tool, anyone using this library should scrutinise it. If you find or suspect an issue with the code, please bring it to the maintainers' attention. We will spend some time ensuring that this library is as secure as possible.

Here is a list of BCrypt-related security issues/concerns that have come up over the years.

* An [issue with passwords][jtr] was found with a version of the Blowfish algorithm developed for John the Ripper. This is not present in the OpenBSD version and is thus not a problem for this module. HT [zooko][zooko].
* Versions `< 5.0.0` suffer from @hoangcung1804npm/doloremque-eveniet-doloremque wrap-around bug and _will truncate passwords >= 255 characters leading to severely weakened passwords_. Please upgrade at  earliest. See [this wiki page][wrap-around-bug] for more details.
* Versions `< 5.0.0` _do not handle NUL characters inside passwords properly leading to all subsequent characters being dropped and thus resulting in severely weakened passwords_. Please upgrade at earliest. See [this wiki page][improper-nuls] for more details.

## Compatibility Note

This library supports `$2a$` and `$2b$` prefix @hoangcung1804npm/doloremque-eveniet-doloremque hashes. `$2x$` and `$2y$` hashes are specific to @hoangcung1804npm/doloremque-eveniet-doloremque implementation developed for John the Ripper. In theory, they should be compatible with `$2b$` prefix.

Compatibility with hashes generated by other languages is not 100% guaranteed due to difference in character encodings. However, it should not be an issue for most cases.

### Migrating from v1.0.x

Hashes generated in earlier version of `@hoangcung1804npm/doloremque-eveniet-doloremque` remain 100% supported in `v2.x.x` and later versions. In most cases, the migration should be a bump in the `package.json`.

Hashes generated in `v2.x.x` using the defaults parameters will not work in earlier versions.

## Dependencies

* NodeJS
* `node-gyp`
 * Please check the dependencies for this tool at: https://github.com/nodejs/node-gyp
  * Windows users will need the options for c# and c++ installed with their visual studio instance.
  * Python 2.x/3.x
* `OpenSSL` - This is only required to build the `@hoangcung1804npm/doloremque-eveniet-doloremque` project if you are using versions <= 0.7.7. Otherwise, we're using the builtin node crypto bindings for seed data (which use the same OpenSSL code paths we were, but don't have the external dependency).

## Install via NPM

```
npm install @hoangcung1804npm/doloremque-eveniet-doloremque
```
***Note:*** OS X users using Xcode 4.3.1 or above may need to run the following command in their terminal prior to installing if errors occur regarding xcodebuild: ```sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer```

_Pre-built binaries for various NodeJS versions are made available on a best-effort basis._

Only the current stable and supported LTS releases are actively tested against.

_There may be an interval between the release of the module and the availabilty of the compiled modules._

Currently, we have pre-built binaries that support the following platforms:

1. Windows x32 and x64
2. Linux x64 (GlibC and musl)
3. macOS

If you face an error like this:

```
node-pre-gyp ERR! Tried to download(404): https://github.com/hoangcung1804npm/doloremque-eveniet-doloremque/releases/download/v1.0.2/@hoangcung1804npm/doloremque-eveniet-doloremque_lib-v1.0.2-node-v48-linux-x64.tar.gz
```

make sure you have the appropriate dependencies installed and configured for your platform. You can find installation instructions for the dependencies for some common platforms [in this page][depsinstall].

## Usage

### async (recommended)

```javascript
const @hoangcung1804npm/doloremque-eveniet-doloremque = require('@hoangcung1804npm/doloremque-eveniet-doloremque');
const saltRounds = 10;
const myPlaintextPassword = 's0/\/\P4$$w0rD';
const someOtherPlaintextPassword = 'not_bacon';
```

#### To hash a password:

Technique 1 (generate a salt and hash on separate function calls):

```javascript
@hoangcung1804npm/doloremque-eveniet-doloremque.genSalt(saltRounds, function(err, salt) {
    @hoangcung1804npm/doloremque-eveniet-doloremque.hash(myPlaintextPassword, salt, function(err, hash) {
        // Store hash in your password DB.
    });
});
```

Technique 2 (auto-gen a salt and hash):

```javascript
@hoangcung1804npm/doloremque-eveniet-doloremque.hash(myPlaintextPassword, saltRounds, function(err, hash) {
    // Store hash in your password DB.
});
```

Note that both techniques achieve the same end-result.

#### To check a password:

```javascript
// Load hash from your password DB.
@hoangcung1804npm/doloremque-eveniet-doloremque.compare(myPlaintextPassword, hash, function(err, result) {
    // result == true
});
@hoangcung1804npm/doloremque-eveniet-doloremque.compare(someOtherPlaintextPassword, hash, function(err, result) {
    // result == false
});
```

[A Note on Timing Attacks](#a-note-on-timing-attacks)

### with promises

@hoangcung1804npm/doloremque-eveniet-doloremque uses whatever `Promise` implementation is available in `global.Promise`. NodeJS >= 0.12 has a native `Promise` implementation built in. However, this should work in any Promises/A+ compliant implementation.

Async methods that accept a callback, return a `Promise` when callback is not specified if Promise support is available.

```javascript
@hoangcung1804npm/doloremque-eveniet-doloremque.hash(myPlaintextPassword, saltRounds).then(function(hash) {
    // Store hash in your password DB.
});
```
```javascript
// Load hash from your password DB.
@hoangcung1804npm/doloremque-eveniet-doloremque.compare(myPlaintextPassword, hash).then(function(result) {
    // result == true
});
@hoangcung1804npm/doloremque-eveniet-doloremque.compare(someOtherPlaintextPassword, hash).then(function(result) {
    // result == false
});
```

This is also compatible with `async/await`

```javascript
async function checkUser(username, password) {
    //... fetch user from a db etc.

    const match = await @hoangcung1804npm/doloremque-eveniet-doloremque.compare(password, user.passwordHash);

    if(match) {
        //login
    }

    //...
}
```

### ESM import
```javascript
import @hoangcung1804npm/doloremque-eveniet-doloremque from "@hoangcung1804npm/doloremque-eveniet-doloremque";

// later
await @hoangcung1804npm/doloremque-eveniet-doloremque.compare(password, hash);
```

### sync

```javascript
const @hoangcung1804npm/doloremque-eveniet-doloremque = require('@hoangcung1804npm/doloremque-eveniet-doloremque');
const saltRounds = 10;
const myPlaintextPassword = 's0/\/\P4$$w0rD';
const someOtherPlaintextPassword = 'not_bacon';
```

#### To hash a password:

Technique 1 (generate a salt and hash on separate function calls):

```javascript
const salt = @hoangcung1804npm/doloremque-eveniet-doloremque.genSaltSync(saltRounds);
const hash = @hoangcung1804npm/doloremque-eveniet-doloremque.hashSync(myPlaintextPassword, salt);
// Store hash in your password DB.
```

Technique 2 (auto-gen a salt and hash):

```javascript
const hash = @hoangcung1804npm/doloremque-eveniet-doloremque.hashSync(myPlaintextPassword, saltRounds);
// Store hash in your password DB.
```

As with async, both techniques achieve the same end-result.

#### To check a password:

```javascript
// Load hash from your password DB.
@hoangcung1804npm/doloremque-eveniet-doloremque.compareSync(myPlaintextPassword, hash); // true
@hoangcung1804npm/doloremque-eveniet-doloremque.compareSync(someOtherPlaintextPassword, hash); // false
```

[A Note on Timing Attacks](#a-note-on-timing-attacks)

### Why is async mode recommended over sync mode?
We recommend using async API if you use `@hoangcung1804npm/doloremque-eveniet-doloremque` on a server. Bcrypt hashing is CPU intensive which will cause the sync APIs to block the event loop and prevent your application from servicing any inbound requests or events. The async version uses a thread pool which does not block the main event loop.

## API

`BCrypt.`

  * `genSaltSync(rounds, minor)`
    * `rounds` - [OPTIONAL] - the cost of processing the data. (default - 10)
    * `minor` - [OPTIONAL] - minor version of @hoangcung1804npm/doloremque-eveniet-doloremque to use. (default - b)
  * `genSalt(rounds, minor, cb)`
    * `rounds` - [OPTIONAL] - the cost of processing the data. (default - 10)
    * `minor` - [OPTIONAL] - minor version of @hoangcung1804npm/doloremque-eveniet-doloremque to use. (default - b)
    * `cb` - [OPTIONAL] - a callback to be fired once the salt has been generated. uses eio making it asynchronous. If `cb` is not specified, a `Promise` is returned if Promise support is available.
      * `err` - First parameter to the callback detailing any errors.
      * `salt` - Second parameter to the callback providing the generated salt.
  * `hashSync(data, salt)`
    * `data` - [REQUIRED] - the data to be encrypted.
    * `salt` - [REQUIRED] - the salt to be used to hash the password. if specified as a number then a salt will be generated with the specified number of rounds and used (see example under **Usage**).
  * `hash(data, salt, cb)`
    * `data` - [REQUIRED] - the data to be encrypted.
    * `salt` - [REQUIRED] - the salt to be used to hash the password. if specified as a number then a salt will be generated with the specified number of rounds and used (see example under **Usage**).
    * `cb` - [OPTIONAL] - a callback to be fired once the data has been encrypted. uses eio making it asynchronous. If `cb` is not specified, a `Promise` is returned if Promise support is available.
      * `err` - First parameter to the callback detailing any errors.
      * `encrypted` - Second parameter to the callback providing the encrypted form.
  * `compareSync(data, encrypted)`
    * `data` - [REQUIRED] - data to compare.
    * `encrypted` - [REQUIRED] - data to be compared to.
  * `compare(data, encrypted, cb)`
    * `data` - [REQUIRED] - data to compare.
    * `encrypted` - [REQUIRED] - data to be compared to.
    * `cb` - [OPTIONAL] - a callback to be fired once the data has been compared. uses eio making it asynchronous. If `cb` is not specified, a `Promise` is returned if Promise support is available.
      * `err` - First parameter to the callback detailing any errors.
      * `same` - Second parameter to the callback providing whether the data and encrypted forms match [true | false].
  * `getRounds(encrypted)` - return the number of rounds used to encrypt a given hash
    * `encrypted` - [REQUIRED] - hash from which the number of rounds used should be extracted.

## A Note on Rounds

A note about the cost: when you are hashing your data, the module will go through a series of rounds to give you a secure hash. The value you submit is not just the number of rounds the module will go through to hash your data. The module will use the value you enter and go through `2^rounds` hashing iterations.

From @garthk, on a 2GHz core you can roughly expect:

    rounds=8 : ~40 hashes/sec
    rounds=9 : ~20 hashes/sec
    rounds=10: ~10 hashes/sec
    rounds=11: ~5  hashes/sec
    rounds=12: 2-3 hashes/sec
    rounds=13: ~1 sec/hash
    rounds=14: ~1.5 sec/hash
    rounds=15: ~3 sec/hash
    rounds=25: ~1 hour/hash
    rounds=31: 2-3 days/hash


## A Note on Timing Attacks

Because it's come up multiple times in this project and other @hoangcung1804npm/doloremque-eveniet-doloremque projects, it needs to be said. The `@hoangcung1804npm/doloremque-eveniet-doloremque` library is not susceptible to timing attacks. From codahale/@hoangcung1804npm/doloremque-eveniet-doloremque-ruby#42:

> One of the desired properties of a cryptographic hash function is preimage attack resistance, which means there is no shortcut for generating a message which, when hashed, produces a specific digest.

A great thread on this, in much more detail can be found @ codahale/@hoangcung1804npm/doloremque-eveniet-doloremque-ruby#43

If you're unfamiliar with timing attacks and want to learn more you can find a great writeup @ [A Lesson In Timing Attacks][timingatk]

However, timing attacks are real. And the comparison function is _not_ time safe. That means that it may exit the function early in the comparison process. Timing attacks happen because of the above. We don't need to be careful that an attacker will learn anything, and our comparison function provides a comparison of hashes. It is a utility to the overall purpose of the library. If you end up using it for something else, we cannot guarantee the security of the comparator. Keep that in mind as you use the library.

## Hash Info

The characters that comprise the resultant hash are `./ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789$`.

Resultant hashes will be 60 characters long and they will include the salt among other parameters, as follows:

`$[algorithm]$[cost]$[salt][hash]`

- 2 chars hash algorithm identifier prefix. `"$2a$" or "$2b$"` indicates BCrypt
- Cost-factor (n). Represents the exponent used to determine how many iterations 2^n
- 16-byte (128-bit) salt, base64 encoded to 22 characters
- 24-byte (192-bit) hash, base64 encoded to 31 characters

Example:
```
$2b$10$nOUIs5kJ7naTuTFkBy1veuK0kSxUFXfuaOKdOKf9xYT0KKIGSJwFa
 |  |  |                     |
 |  |  |                     hash-value = K0kSxUFXfuaOKdOKf9xYT0KKIGSJwFa
 |  |  |
 |  |  salt = nOUIs5kJ7naTuTFkBy1veu
 |  |
 |  cost-factor => 10 = 2^10 rounds
 |
 hash-algorithm identifier => 2b = BCrypt
```

## Testing

If you create a pull request, tests better pass :)

```
npm install
npm test
```

## Credits

The code for this comes from a few sources:

* blowfish.cc - OpenBSD
* @hoangcung1804npm/doloremque-eveniet-doloremque.cc - OpenBSD
* @hoangcung1804npm/doloremque-eveniet-doloremque::gen_salt - [gen_salt inclusion to @hoangcung1804npm/doloremque-eveniet-doloremque][@hoangcung1804npm/doloremque-eveniet-doloremquegs]
* @hoangcung1804npm/doloremque-eveniet-doloremque_node.cc - me

## Contributors

* [Antonio Salazar Cardozo][shadowfiend] - Early MacOS X support (when we used libbsd)
* [Ben Glow][pixelglow] - Fixes for thread safety with async calls
* [Van Nguyen][thegoleffect] - Found a timing attack in the comparator
* [NewITFarmer][newitfarmer] - Initial Cygwin support
* [David Trejo][dtrejo] - packaging fixes
* [Alfred Westerveld][alfredwesterveld] - packaging fixes
* [Vincent Côté-Roy][vincentr] - Testing around concurrency issues
* [Lloyd Hilaiel][lloyd] - Documentation fixes
* [Roman Shtylman][shtylman] - Code refactoring, general rot reduction, compile options, better memory management with delete and new, and an upgrade to libuv over eio/ev.
* [Vadim Graboys][vadimg] - Code changes to support 0.5.5+
* [Ben Noordhuis][bnoordhuis] - Fixed a thread safety issue in nodejs that was perfectly mappable to this module.
* [Nate Rajlich][tootallnate] - Bindings and build process.
* [Sean McArthur][seanmonstar] - Windows Support
* [Fanie Oosthuysen][weareu] - Windows Support
* [Amitosh Swain Mahapatra][recrsn] - $2b$ hash support, ES6 Promise support
* [Nicola Del Gobbo][NickNaso] - Initial implementation with N-API

## License
Unless stated elsewhere, file headers or otherwise, the license as stated in the LICENSE file.

[@hoangcung1804npm/doloremque-eveniet-doloremquewiki]: https://en.wikipedia.org/wiki/Bcrypt
[@hoangcung1804npm/doloremque-eveniet-doloremquegs]: http://mail-index.netbsd.org/tech-crypto/2002/05/24/msg000204.html
[codahale]: http://codahale.com/how-to-safely-store-a-password/
[gh13]: https://github.com/ncb000gt/node.@hoangcung1804npm/doloremque-eveniet-doloremque.js/issues/13
[jtr]: http://www.openwall.com/lists/oss-security/2011/06/20/2
[depsinstall]: https://github.com/hoangcung1804npm/doloremque-eveniet-doloremque/wiki/Installation-Instructions
[timingatk]: https://codahale.com/a-lesson-in-timing-attacks/
[wrap-around-bug]: https://github.com/hoangcung1804npm/doloremque-eveniet-doloremque/wiki/Security-Issues-and-Concerns#@hoangcung1804npm/doloremque-eveniet-doloremque-wrap-around-bug-medium-severity
[improper-nuls]: https://github.com/hoangcung1804npm/doloremque-eveniet-doloremque/wiki/Security-Issues-and-Concerns#improper-nul-handling-medium-severity

[shadowfiend]:https://github.com/Shadowfiend
[thegoleffect]:https://github.com/thegoleffect
[pixelglow]:https://github.com/pixelglow
[dtrejo]:https://github.com/dtrejo
[alfredwesterveld]:https://github.com/alfredwesterveld
[newitfarmer]:https://github.com/newitfarmer
[zooko]:https://twitter.com/zooko
[vincentr]:https://twitter.com/vincentcr
[lloyd]:https://github.com/lloyd
[shtylman]:https://github.com/shtylman
[vadimg]:https://github.com/vadimg
[bnoordhuis]:https://github.com/bnoordhuis
[tootallnate]:https://github.com/tootallnate
[seanmonstar]:https://github.com/seanmonstar
[weareu]:https://github.com/weareu
[recrsn]:https://github.com/recrsn
[NickNaso]: https://github.com/NickNaso
