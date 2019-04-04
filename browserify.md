# Browserify

## Making generators and async/await work on iOS 10

These things will work now (2019-04-03) in desktop browsers without any transforms or plugins. You need to compile down to ES5 for Mobile Safari.

To do that, [these are the changes necessary](https://github.com/jimkang/observatory/commit/0f5f1a4c6c916f4e536ccfb9732c5a9a882ea27a):

- Both of these packages are needed:
    - @babel/plugin-transform-runtime (as a dev dependency)
    - @babel/runtime (as a runtime dependency; *actually goes into the built js*)
- These switches need to be passed to browserify:

    -t [ babelify --presets [ @babel/preset-env ] --plugins [ @babel/plugin-transform-runtime ] ]

The preset-env (with no targets) will compile tell babelify to compile to ES2015, while plugin-transform-runtime tells it to include runtime support for generators.
