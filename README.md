# swagger-express-middleware (patched for multer 1.x support)

>⚠️ No longer maintained This package has been abandoned for some time, and there are plenty of modern alternatives around which support OpenAPI v3.x listed on [OpenAPI.Tools](https://openapi.tools/) which you can use instead.

This is a patched version of [swagger-express-middleware](https://github.com/APIDevTools/swagger-express-middleware)
designed to allow proper parsing of `multipart/form-data` using `multer@1.x`.

## Why

The original library does not play well with `multer` due to premature body parsing,
which leads to broken `req.body` or missing files.

This fork modifies the behavior to:

- Delay body parsing when `multipart/form-data` is detected
- Let multer handle it as expected

## Changes

- Patched `body-parser.js` and `middleware.js`
- Tested with NestJS + Swagger + Multer + file uploads

## Usage

Install directly from GitHub:

```bash
npm install github:sbor767/swagger-express-middleware-for-multer-1.x
```

Or clone and use manually.

Then use it in your [Node.js](http://nodejs.org/) script like this:

```javascript
const express = require('express');
const createMiddleware = require('swagger-express-middleware');

let app = express();

createMiddleware('PetStore.yaml', app, function(err, middleware) {
    // Add all the Swagger Express Middleware, or just the ones you need.
    // NOTE: Some of these accept optional options (omitted here for brevity)
    app.use(
        middleware.metadata(),
        middleware.CORS(),
        middleware.files(),
        middleware.parseRequest(),
        middleware.validateRequest(),
        middleware.mock()
    );

    app.listen(8000, function() {
        console.log('The PetStore sample is now running at http://localhost:8000');
    });
});
```


## Disclaimer

This is a workaround, not an official fork. Use at your own risk.

---

License
--------------------------
Swagger Express Middleware is 100% free and open-source, under the [MIT license](LICENSE). Use it however you want.
