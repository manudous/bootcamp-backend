# 01 Config

In this example we are going to add a basic setup needed to support unit testing with Jest.

We will start from `00-boilerplate`.

# Steps to build it

- `npm install` to install previous sample packages:

```bash
npm install

```

# Libraries

We are going to install the main library which we base all our unit tests, [Jest](https://facebook.github.io/jest/en/).

- [jest](https://github.com/facebook/jest): JavaScript Testing library with runner, assertion, mocks, etc.
- [@types/jest](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/df38f202a0185eadfb6012e47dd91f8975eb6151/types/jest): Typings for jest.

```bash
npm install jest @types/jest --save-dev
```

> If we are using `@babel/preset-typescript` it is not necessary install [ts-jest](https://github.com/kulshekhar/ts-jest): A preprocessor with sourcemap support to help use TypeScript with Jest.
> [Official docs](https://jestjs.io/docs/getting-started)
> NOTE: [Since jest v26.x it drops support for Node 8](https://github.com/facebook/jest/releases/tag/v26.0.0)

# Config

Jest test commands:
  - `npm test`: to single run
  - `npm run test:watch`: to run all specs after changes.

> NOTE:

> [Jest CLI options](https://facebook.github.io/jest/docs/en/cli.html#options)

> --watchAll To rerun all tests.

> --watch To rerun tests related to changed files.

> --verbose Display individual test results with the test suite hierarchy.

> -i or --runInBand Run all tests serially in the current process, rather than creating a worker pool of child processes that run tests. This can be useful for debugging

_./package.json_

```diff
{
  ...
  "scripts": {
    ...
+   "test": "jest --verbose",
+   "test:watch": "npm run test -- --watchAll -i"
  },
  ...
}
```

# Dummy spec

Let's launch tests in watch mode:

```bash
npm run test:watch
```

- Adding success spec:

_./src/dummy.spec.ts_

```javascript
describe('dummy specs', () => {
  it('should pass spec', () => {
    // Arrange

    // Act

    // Assert
    expect(true).toBeTruthy();
  });
});
```

Adding failed spec:

_./src/dummy.spec.ts_

```diff
describe('dummy specs', () => {
  it('should pass spec', () => {
    // Arrange

    // Act

    // Assert
    expect(true).toBeTruthy();
  });

+ it('should fail spec', () => {
+   // Arrange

+   // Act

+   // Assert
+   expect(true).toBeFalsy();
+ });
});
```

# External config

We could create a jest config outside `package.json` to improve maintainability.

> [Jest configuration options](https://facebook.github.io/jest/docs/en/configuration.html#options)

- Create config in `config/test/jest.js` file:

_./config/test/jest.js_

```js
module.exports = {
  rootDir: '../../',
  verbose: true,
};

```
> Check `verbose: false` to see differences
> We will add some configuration in next examples when needed

- And use that file:

### ./package.json

```diff
{
  ...
  "scripts": {
    ...
-   "test": "jest --verbose",
+   "test": "jest -c ./config/test/jest.js",
    "test:watch": "npm run test -- --watchAll -i"
  },
  ...
}
```

Running specs again:

```bash
npm run test:watch
```

# ¿Con ganas de aprender Backend?

En Lemoncode impartimos un Bootcamp Backend Online, centrado en stack node y stack .net, en él encontrarás todos los recursos necesarios: clases de los mejores profesionales del sector, tutorías en cuanto las necesites y ejercicios para desarrollar lo aprendido en los distintos módulos. Si quieres saber más puedes pinchar [aquí para más información sobre este Bootcamp Backend](https://lemoncode.net/bootcamp-backend#bootcamp-backend/banner).
