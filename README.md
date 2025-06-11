## [tsx](https://github.com/privatenumber/tsx) issue minimal reproduction

- https://github.com/privatenumber/tsx/issues/722

### Reproducing the error:

```sh
npm ci # tsx 4.20.1
npm test:import # import './a.js';
npm test:require # require('./a.js');
```

<details>
<summary>
❌ Output:
</summary>

```
node:internal/assert:17
  throw new ERR_INTERNAL_ASSERTION(message);
        ^

Error [ERR_INTERNAL_ASSERTION]: Unexpected module status 3.
This is caused by either a bug in Node.js or incorrect usage of Node.js internals.
Please open an issue with this stack trace at https://github.com/nodejs/node/issues

    at assert.fail (node:internal/assert:17:9)
    at ModuleJob.runSync (node:internal/modules/esm/module_job:314:12)
    at require (node:internal/modules/esm/translators:150:9)
    at <anonymous> (***/test/b.ts:1:11)
    at Object.<anonymous> (***/test/b.ts:1:27)
    at loadCJSModule (node:internal/modules/esm/translators:165:3)
    at ModuleWrap.<anonymous> (node:internal/modules/esm/translators:207:7)
    at ModuleJob.runSync (node:internal/modules/esm/module_job:306:39)
    at require (node:internal/modules/esm/translators:150:9)
    at <anonymous> (***/test/a.ts:1:11) {
  code: 'ERR_INTERNAL_ASSERTION'
}

Node.js v24.1.0
```

</details>

> [!NOTE]
>
> - Even using the explicit `commonjs` type in the _package.json_, the error remains the same.
> - Despite using `"module":"CommonJS"`, `"esModuleInterop": true` or no _tsconfig.json_, the error remains the same.

---

### Expected behavior:

If we go back to [**tsx**](https://github.com/privatenumber/tsx) `v4.19.4`, the code will work as expected:

```sh
npm i -D tsx@4.19.4
npm test:import # import './a.js';
npm test:require # require('./a.js');
```

✅ Output:

```
Hello from app.ts
```
