## Code coverage

1. Test the `url.URL.domainToASCII()` and `url.URL.domainToUnicode()` functions
  - Example inputs for `url.URL.domainToUnicode()`:
    ASCII characters, `ÄÖÜ`/`äöü`, `⨌`
  - Check `url.URL.domainToASCII()` for the reverse transformations
1. `util.inspect(new url.URL('http://127.0.0.1/'), {showHidden: true})`
   contains a stray `;`
1. **advanced**: Implement custom inspect function for `TupleOrigin`
   (from `lib/internal/util.js`)
1. **advanced**: Add basic testing for `url.URL.originFor`
1. Add a test for `process.assert`
  - One test for a passing assertion, one for a failing one
1. `throw null` doesn’t work in the REPL (well… at least not properly)
1. **advanced** (and possibly combinable with the previous item):
   Throwing an object that is not an Error in the REPL just displays the object
1. **advanced**: Test what happens when a `process.on('exit')` listener
   throws an error (the process does not exit – a second `process.exit()` will)
1. Test the error that is thrown when passing invalid signals to `process.kill`
1. **advanced**: Test what happens when `.kill()` is called in an `exit`
   event handler for a child process
1. Test argument validation for `buffer.transcode`
  - First argument must be a `Buffer`; also test what happens when it is empty
1. **advanced**: Test combination of `--eval` and `--interactive`
1. Test that `Buffer.prototype.writeUInt32LE.call({})` throws an error
1. Test that `Buffer.alloc(0).writeUInt32LE(number)` throws an error
1. Test that `readableStream.unpipe()` removes all pipe destinations
  - Should be tested for a stream that has pipes to 0, 1, 2 existing streams
1. Test that `readableStream.unpipe(dest)` is a no-op when the `dest` is
   not a destination for `readableStream`
  - Should be tested for a stream that has pipes to 0, 1, 2 existing streams
1. Test the error thrown by `http.request({method:'\0'})`
1. **advanced**: Test that `process.stdin.setRawMode()` works
  - This test needs to be in `test/pseudo-tty`
  - It probably can’t do much besides testing that `isRaw` works
1. Test that `clearImmediate(null)` & co are no-ops
1. Test the error thrown when `require()`ing a directory with an invalid
   `package.json`
1. Test that calling `.listeners('type')` on an `EventEmitter` without
   any listeners works

## Refactoring tests

1. `test/parallel/test-vm-syntax-error-stderr.js`:
  - `var` → `const`/`let`
  - `assert(false, …)` → `common.fail()`
1. `test/parallel/test-vm-static-this.js`:
  - Replace `console.error`s with comments
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-vm-debug-context.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-umask.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-tls-timeout-server.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-tls-timeout-server-2.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
1. **advanced**: `test/parallel/test-tls-ticket.js` and
   `test/parallel/test-tls-ticket-cluster.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - Refactor `process.on('exit')` handler into `common.mustCall`s
  - Ideally, add some explanation on what the test is supposed to test.1
1. `test/parallel/test-tls-set-encoding.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
  - Bonus points: The test currently passes when replacing `utf8` with `ascii`,
    so it doesn’t really check that the `setEncoding()` call is important;
    adressing that would be awesome!
1. `test/parallel/test-tls-set-ciphers.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. **advanced**: `test/parallel/test-tls-server-verify.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - Refactor `process.on('exit')` handler into `common.mustCall`s
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-tls-peer-certificate.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `assert.ok(… === …)` → `assert.strictEqual`
1. `test/parallel/test-tls-peer-certificate-encoding.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `assert.ok(… === …)` → `assert.strictEqual`
1. `test/parallel/test-tls-passphrase.js`:
  - `var` → `const`/`let`
  - Check error message in `assert.throws`
1. `test/parallel/test-tls-on-empty-socket.js`:
  - `var` → `const`/`let`
  - Refactor `process.on('exit')` handler into `common.mustCall`s
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-tls-ocsp-callback.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `assert.ok(… === …)` → `assert.strictEqual`
1. `test/parallel/test-tls-no-sslv3.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-tls-no-rsa-key.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-tls-no-cert-required.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-tls-key-mismatch.js`:
  - `var` → `const`/`let`
  - Check error message in `assert.throws`
1. `test/parallel/test-tls-junk-closes-server.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - Use `common.fail` for functions that will never be executed
  - Check error message in `assert.throws`
1. `test/parallel/test-tls-js-stream.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - `assert.equal` → `assert.strictEqual`
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. **advanced** `test/parallel/test-tls-interleave.js`:
  - `var` → `const`/`let`
  - `common.mustCall(·, n)` for functions that need to be called exactly n times
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-getcipher.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-tls-friendly-error-message.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. **advanced** `test/parallel/test-tls-econnreset.js`:
  - `var` → `const`/`let`
  - Test error messages
  - `common.fail` instead of `throw 'unreachable'`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-ecdh.js`:
  - `var` → `const`/`let`
  - `assert.notEqual(·.indexOf(·), -1)` → `assert(·.includes(·))`
1. `test/parallel/test-tls-ecdh-disable.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - `assert.notEqual(·.indexOf(·), -1)` → `assert(·.includes(·))`
1. **advanced** `test/parallel/test-tls-ecdh-dhe.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-destroy-whilst-write.js`:
  - `var` → `const`/`let`
  - Replace the arbitrary timeout by e.g. nested `setImmediate` calls
1. `test/parallel/test-tls-connect-simple.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-cnnic-whitelist.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-client-verify.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-client-reject.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. **advanced** `test/parallel/test-tls-client-getephemeralkeyinfo.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-check-server-identity.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - Use template strings where you think that improves readability
1. `test/parallel/test-tls-alert-handling.js`:
  - `var` → `const`/`let`
  - `common.mustCall(·, n)` for functions that need to be called exactly n times
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-tls-0-dns-altname.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-sync-fileread.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - Maybe also rename the test into something beginning with `test-fs-`?
1. **advanced** `test/parallel/test-stream2-unpipe-drain.js`:
  - `var` → `const`/`let`
  - Remove dependency on `crypto`
  - Give each `TestReader` its own `read` function, wrapped in `common.mustCall(·, 2)`
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-stdout-to-file.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
  - Use template strings where you think that improves readability
1. `test/parallel/test-stdout-close-catch.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-stdin-from-file.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - The first `fs.unlinkSync()` should be unnecessary
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-signal-unregister.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-require-resolve.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-require-json.js`:
  - `var` → `const`/`let`
  - Make sure the `catch` path is actually taken
1. `test/parallel/test-require-extensions-same-filename-as-dir-trailing-slash.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-require-extensions-same-filename-as-dir.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-require-extensions-main.js`:
  - `var` → `const`/`let`
  - `assert` for the return value of `require()`
1. `test/parallel/test-require-exceptions.js`:
  - `var` → `const`/`let`
  - Check error message in `assert.throws`
1. `test/parallel/test-require-dot.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-repl-reset-event.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - `assert.equal` → `assert.strictEqual`
  - Remove the timeout
1. `test/parallel/test-repl-mode.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-repl.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - This test file is large, so if you see want to go understand what it does
    and see something that can be improved, go for it.
1. `test/parallel/test-pipe-stream.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-pipe-head.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. **advanced** `test/parallel/test-pipe-file-to-http.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into `common.mustCall`s
1. `test/parallel/test-os-homedir-no-envvar.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `assert.ok(… === …)` → `assert.strictEqual`
  - `assert.ok(·.indexOf(·) === -1)` → `assert(·.includes(·))`
1. **advanced** `test/parallel/test-net-server-bind.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into .mustCall`s
1. `test/parallel/test-net-reconnect-error.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-localport.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-net-localerror.js`:
  - `var` → `const`/`let`
  - The second argument to `assert.throws` needs to be a regular expression
    that matches the actual error message
1. `test/parallel/test-net-local-address-port.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-listen-fd0.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into the `.on('error')` handler
1. `test/parallel/test-net-keepalive.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-net-dns-custom-lookup.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-connect-handle-econnrefused.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `assert.ok(false)` → `common.fail()`
1. `test/parallel/test-net-better-error-messages-port.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-better-error-messages-port-hostname.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-better-error-messages-path.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-better-error-messages-listen-path.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-better-error-messages-listen.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-net-fd-ebadf.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-internal-modules.js`:
  - `var` → `const`/`let`
  - Check error message in `assert.throws`
1. `test/parallel/test-http-unix-socket.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-https-truncate.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-https-timeout-server.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-https-agent-session-reuse.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-http-dns-error.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-http-chunked-304.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-write-stream-err.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-write.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-write-file-sync.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-write-file.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-truncate.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `assert(·.equals(·))` → `assert.deepStrictEqual(·,·)`
1. `test/parallel/test-fs-truncate-fd.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-symlink-dir-junction.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-read-stream-resume.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-read-stream.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-read-stream-inherit.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-read-stream-err.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-read-file-sync.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-fsync.js`:
  - `var` → `const`/`let`
  - `common.mustCall` for functions that need to be called exactly once
  - Refactor `process.on('exit')` handler into the `.on('error')` handler
1. `test/parallel/test-fs-empty-readStream.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-fs-append-file-sync.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-fs-append-file.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-dgram-msgsize.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-dgram-bind-default-address.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-crypto-pbkdf2.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-crypto-padding.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - Check error message in `assert.throws`
1. `test/parallel/test-crypto-hash-stream-pipe.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-crypto-ecb.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-crypto-cipheriv-decipheriv.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-crypto-cipherv-decipher.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-crypto-certificate.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-cluster-shared-handle-bind-privileged-port.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-cluster-shared-handle-bind-error.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-cluster-setup-master-argv.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-cluster-send-handle-twice.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
  - `assert(false, …)` → `common.fail()`
1. `test/parallel/test-cluster-send-deadlock.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-cluster-net-send.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
  - `common.mustCall` for functions that need to be called exactly once
1. `test/parallel/test-cluster-net-listen.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-child-process-stdout-flush-exit.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-child-process-stdio-inherit.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-child-process-spawn-error.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-child-process-kill.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
1. `test/parallel/test-child-process-ipc.js`:
  - `var` → `const`/`let`
  - `assert.equal` → `assert.strictEqual`
