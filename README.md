## Getting Started

To run the server, cd into the `ProductsServer` directory and run:
 
```bash
npm i
npm run build
npm start
```

To run the client, cd into the `MyAngularClient` directory and run:
 
```bash
npm install 
ng serve
```

### Create a New OIDC App in Okta

Before you begin, you’ll need a free Okta developer account. Install the [Okta CLI](https://cli.okta.com) and run `okta register` to sign up for a new account. If you already have an account, run `okta login`.

Then, run `okta apps create`. Select the default app name, or change it as you see fit. Choose **Single-Page App** and press **Enter**.

Use `http://localhost:4200/callback` for the Redirect URI and accept the default Logout Redirect URI of `http://localhost:4200`.

#### Server Configuration

Set your domain and copy the `clientId` into `ProductsServer/src/auth.ts`. 

**NOTE:** The value of `{yourOktaDomain}` should be something like `dev-123456.okta.com`. Make sure you don't include `-admin` in the value!

```ts
const oktaJwtVerifier = new OktaJwtVerifier({
  issuer: 'https://{yourOktaDomain}/oauth2/default'
  clientId: '{clientId}',
});
```

#### Client Configuration

For the client, set the `issuer` and copy the `clientId` into `MyAngularClient/src/app/app.module.ts`.

```typescript
const oktaConfig = {
  issuer: 'https://{yourOktaDomain}/oauth2/default',
  clientId: '{clientId}',
  redirectUri: window.location.origin + '/callback'
};
```
