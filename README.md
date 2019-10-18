# Consumer API OpenID Connect Example

This project is an example of how to connect to [Banno](https://banno.com/) services using [OpenID Connect](https://openid.net/connect/) (an identity layer on top of [OAuth 2.0](https://oauth.net/2/)).

This repository includes an example that uses [Node.js](https://nodejs.org) with the [Passport](http://www.passportjs.org/) authentication middleware to handle the OpenID Connect protocol.

# Prerequisites from Banno

Before you get started with the example code, you'll need to get some credentials from your `Implementation Coordinator` at Banno.

You'll need these credentials:
- `client_id`
- `client_secret`

## CAUTION

```
It is important to keep the `client_secret` value secret and not leak it through some kind of frontend, client-accessible JavaScript call.
```

# Install

## 1) Install software prerequisites

The example is built for [Node.js](https://nodejs.org) and [npm](https://www.npmjs.com/).

If you don't have these installed on your system already, you may want to install a Node Version Manager such as [nvm](https://github.com/nvm-sh/nvm).

## 2) Clone the repository

The cloned repository includes everything that you need for the next step.

## 3) Install project dependencies

From the repository root folder, run this command in the terminal:

```
npm install
```

# Running the example locally

After you've completed the installation steps, run this command in the terminal from the repository root folder:

```
npm start
```

The server will now be running locally. You'll see this log statement in the terminal:

```
Environment: local
Server listening on https://localhost:8080...
```

Next, go to https://localhost:8080/login.html in a web browser.

Click on `Sign in with Banno` and sign in with your Banno Username and Password.

Once you are signed in, you'll be redirected to https://localhost:8080/me and see the [OpenID Connect claims](https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims) for the user. It'll look similar to the following example:

```
{
  "sub": "5cad5c30-6d24-11e9-870c-0242b78f8571",
  "birthdate": "1951-03-02",
  "family_name": "Doe",
  "given_name": "Riley",
  "locale": "en-US",
  "name": "Riley Doe",
  "picture": "https://silverlake.banno-production.com/a/consumer/api/node/public-profile-photo/bUlKMGFpcUZmaXdMUG5vNWJJanFkT1hVMmhwVTdmF1bHQ6djE6RFpGhqVUp3YW1mWUIzZ2lYUDljQ0bmdjbGc9PQFyeHppTmIvTTBNK0ZFVXlNRnNVT0VXTW1CRDVKbEx0==",
  "preferred_username": "rileydoe",
  "at_hash": "meToBgo7UfatG825BaaClQ",
  "sid": "e10597ce-4b85-4a78-890b-55e2af751c9a",
  "aud": "05166b79-4f61-484d-a4b4-2a225926bf4b",
  "exp": 1571253248,
  "iat": 1571249648,
  "iss": "https://www.banno.com/a/consumer/api/oidc"
}
```

You'll also see a log statement in the terminal that shows the `access_token` and `id_token`:

```
TokenSet {
  access_token: '<lengthy-json-web-token-string>',
  expires_at: 1571334444,
  id_token: '<lengthy-json-web-token-string>',
  scope: 'openid profile banno',
  token_type: 'Bearer'
}
```

The `access_token` contains _authorization information about your application_ regarding which actions it is allowed to perform via the Banno API. These actions map to the scopes (e.g. `openid profile banno`).

The `id_token` contains _authentication information about the user_ (i.e. claims).

Both the `access_token` and `id_token` are in [JSON Web Token format](https://en.wikipedia.org/wiki/JSON_Web_Token) (see [RFC 7519](https://tools.ietf.org/html/rfc7519) for specification details).

## CAUTION

```
JWTs are credentials which can grant access to resources. It is important to keep them secret.
```