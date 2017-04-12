# microauth-twitter
> Twitter oauth for [micro](https://github.com/zeit/micro/)

[![XO code style](https://img.shields.io/badge/code_style-XO-5ed9c7.svg)](https://github.com/sindresorhus/xo)

Add twitter authentication for your [micro](https://github.com/zeit/micro/) service as easy as a flick of your fingers.

## Installation

```sh
npm install --save microauth-twitter
# or 
yarn add microauth-twitter
```

## Usage

app.js
```js
const { send } = require('micro');
const microAuthTwitter = require('microauth-twitter');

const options = {
  consumerKey: 'CONSUMER_KEY',
  consumerSecret: 'CONSUMER_SECRET',
  callbackUrl: 'http://localhost:3000/auth/twitter/callback',
  path: '/auth/twitter'
};

const twitterAuth = microAuthTwitter(options);

// third `auth` argument will provide error or result of authentication
// so it will { err: errorObject} or { result: {
//  provider: 'twitter',
//  accessToken: 'blahblah',
//  accessTokenSecret: 'blahblah',
//  info: userInfo
// }}
const handler = async (req, res, auth) => {

  if (!auth) {
    return send(res, 404, 'Not Found');
  }

  if (auth.err) {
    // Error handler
    return send(res, 403, 'Forbidden');
  }

  // save something in database here

  return `Hello ${auth.result.info.screen_name}`;

});

module.exports = twitterAuth(handler);
```

Run:
```sh
micro app.js
```


## Author
[Dmitry Pavlovsky](http://palosk.in)
