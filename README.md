# react-twitter-oauth

[![npm](https://img.shields.io/npm/v/react-twitter-oauth?logo=npm&cacheSeconds=1800)](https://www.npmjs.com/package/react-twitter-login)
[![npm bundle size](https://img.shields.io/bundlephobia/minzip/react-twitter-oauth?cacheSeconds=1800)](https://www.npmjs.com/package/react-twitter-login)
[![npm](https://img.shields.io/npm/dt/react-twitter-oauth?cacheSeconds=1800)](https://www.npmjs.com/package/react-twitter-login)

React component for a simple OAuth Twitter integration. Forked from (https://github.com/alexandrtovmach/react-twitter-login)

## 🚀 Get Started

Follow these steps to start using React Twitter Oauth:

1. Installation

   ```sh
   # with npm
   npm i react-twitter-oauth

   # with yarn
   yarn add react-twitter-oauth
   ```

2. Import and configure component.

   > This component should be rendered on route that match with one of whitelisted [callback URLs](https://developer.twitter.com/en/docs/basics/apps/guides/callback-urls) of your Twitter app.

   ```jsx
   import React from "react";
   import TwitterLogin from "react-twitter-oauth";

   export default (props) => {
     const authHandler = (err, data) => {
       console.log(err, data);
     };

     return (
       <TwitterLogin
         authCallback={authHandler}
         consumerKey={CONSUMER_KEY}
         consumerSecret={CONSUMER_SECRET}
         requestTokenUrl={REQUEST_TOKEN_API_ENDPOINT}
         accessTokenUrl={ACCESS_TOKEN_API_ENDPOINT}
       />
     );
   };
   ```

3. REQUEST_TOKEN_API_ENDPOINT get object and send to https://api.twitter.com/oauth/request_token

    ```json
   {   
       "oauth_callback": "https://[oauth_callback]",
       "oauth_consumer_key": "CONSUMER_KEY",
       "oauth_nonce": "oauth nonce generated from component",
       "oauth_signature": "oauth signature generated from component",
       "oauth_signature_method": "HMAC-SHA1",
       "oauth_timestamp": "oauth timestamp generated from component",
       "oauth_version": "1.0"
   }
      ```
   
   then the response should be of this kind
   
   ```json
   {   
       "data": {
           "oauth_callback_confirmed": "true",
           "oauth_token": "oauth token from twitter",
           "oauth_token_secret": "oauth token secret from twitter"
       }
   }
   ```
   
4. ACCESS_TOKEN_API_ENDPOINT get object and send to https://api.twitter.com/oauth/access_token

    ```json
   {   
       "oauth_consumer_key": "CONSUMER_KEY",
       "oauth_nonce": "oauth nonce generated from component",
       "oauth_signature": "oauth signature generated from component",
       "oauth_signature_method": "HMAC-SHA1",
       "oauth_token": "oauth token generated from twitter",
       "oauth_verifier": "oauth verifier generated from component",
       "oauth_timestamp": "oauth timestamp generated from component",
       "oauth_version": "1.0"
   }
      ```
   
   the server response must contain the following data
   ```json
   {   
       "data": {
           "oauth_token": "true",
           "oauth_token_secret": "oauth token secret from twitter",
       }
   }
   ```

5. Find more info about keys and Twitter developer apps in [official docs](https://developer.twitter.com/en/docs/basics/apps/overview).

## 📖 API

| Property       | Type                                                       | Default   | Description                                                                                                            |
| -------------- | ---------------------------------------------------------- | --------- | ---------------------------------------------------------------------------------------------------------------------- |
| authCallback   | function                                                   | required  | Callback function which takes two arguments `(error, authData)`                                                        |
| consumerKey    | string                                                     | required  | Consumer API Key of your Twitter developer app (not Access Token)                                                      |
| consumerSecret | string                                                     | required  | Consumer API Secret of your Twitter developer app (not Access Token Secret)                                            |
| requestTokenUrl| string                                                     | required  | Api endpoint will be used to get request token                                                                         |
| accessTokenUrl | string                                                     | required  | Api endpoint will be used to get access token                                                                          |
| buttonTheme    | enum(`"light"`, `"light_short"`, `"dark"`, `"dark_short"`) | `"light"` | Button style theme, that based on [Twitter Brand Design](https://about.twitter.com/en_us/company/brand-resources.html) |
| className      | string                                                     | `""`      | Custom class name                                                                                                      |
| children       | React.Component                                            | `""`      | Provide any component as a "children" prop to use custom button                                                        |

## 📝 License

[MIT](https://github.com/alexandrtovmach/react-twitter-login/blob/master/LICENSE)
