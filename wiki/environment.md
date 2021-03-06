# Environment support and polyfills

InversifyJS requires a modern JavaScript engine with support for the 
[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), 
[Metadata Reflection API](http://rbuckton.github.io/ReflectDecorators/#reflect) and 
[Proxy](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy) objects. 
If your environment don't support one of these you will need to import a shim or polypill.

## Metadata Reflection API
Required always. Use [reflect-metadata](https://www.npmjs.com/package/reflect-metadata) as polypill.
```
$ npm install reflect-metadata
```
The type definitions for reflect-metadata are included in the npm package. You need to add the following 
reference to the types field in your `tsconfig.json`:
```
"types": ["reflect-metadata"]
```
Finally, import reflect-metadata. If you are working in Node.js you can use:

```
import "reflect-metadata";
```

If you are working in a web browser you can use a script tag:

```
<script src="./node_modules/reflect-metadata/Reflect.js"></script>
```

This will create the Reflect object as a global.

> **The `reflect-metadata` polyfill should be imported only once in your entire application** because the Reflect object is mean to be a global singleton. More details about this can be found [here](https://github.com/inversify/InversifyJS/issues/262#issuecomment-227593844).

## Promise
Promises are only required only if you use want to 
[inject a provider](https://github.com/inversify/InversifyJS#injecting-a-provider-asynchronous-factory).

Most modern JavaScript engines support promises but if you need to support old browsers you will need to use a promise polyfill (e.g. [es6-promise](https://github.com/stefanpenner/es6-promise) or [bluebird](https://www.npmjs.com/package/bluebird)).

## Proxy
ES6 proxies are only required only if you want to [inject a proxy](https://github.com/inversify/InversifyJS/blob/master/wiki/activation_handler.md). 

As today (September 2016) proxies are not very well supported and it is very likely that you will need to use a proxy polyfill. For example, we use [harmony-proxy](https://www.npmjs.com/package/harmony-proxy) as polyfill to run our unit tests.
