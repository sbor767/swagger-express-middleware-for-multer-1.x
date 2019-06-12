Swagger Express Middleware for using with AWS S3
================================================
### Swagger 2.0 middleware and mocks for Express.js

Fork from [swagger-express-middleware](https://github.com/APIDevTools/swagger-express-middleware)

The main goal of the fork is to use the fresh `multer` package for compatibility with the `multer-s3` package that is supposed to be used to upload files to AWS S3.

Installation and Use
--------------------------
Install using [npm](https://docs.npmjs.com/about-npm/).

```bash
npm install swagger-express-middleware
```
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

Samples & Walkthroughs
--------------------------

License
--------------------------
Swagger Express Middleware is 100% free and open-source, under the [MIT license](LICENSE). Use it however you want.
