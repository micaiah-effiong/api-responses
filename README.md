# simple-status

[![Build Status](https://travis-ci.com/micaiah-effiong/api-responses.svg?branch=main)](https://travis-ci.com/micaiah-effiong/api-responses)

Simple express middleware for sending standard status response.

# Install

```bash
# NPM
npm i simple-status
```

# Usage

### import and setup

```js
var simpleStatus = require("simple-status");
app.use(simpleStatus());
```

This adds extra functions to the response object, for handling responses with accurate status code.

## Example

Send response with valid status code by using the methods

```js
app.post("/", (req, res) => {
  res.created({
    status: "success",
    data: { name: "John Doe" },
  }); // { status: "success", data: {name: "John Doe"} }, 201
});

app.get("/user", (req, res) => {
  res.notFound(); // 404
});
```

To send response body manually

```js
app.use(simpleStatus({ send: false }));

app.get("/admin", (req, res) => {
  const data = { msg: "require authentication" };
  res.unauthorized().json(data); // { msg: "require authentication" }, 401
});
```

## Available methods

```js
//2xx success
res.ok();
res.created();

//4xx client errors
res.badRequest();
res.unauthorized();
res.forbidden();
res.notFound();
res.conflict();
res.invalidToken();

//5xx server errors
res.serverError();
res.badGateway();
res.serviceUnavailable();
```
