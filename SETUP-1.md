# Starter Setup

> Note: If you clone repo and run it - make sure your local environment is set. Those details are not checked in.

1. Instantiate the [next-auth-example](https://github.com/nextauthjs/next-auth-example) template to a new project (here `next-auth-starter`) - then clone to local environment.

---

2. Install dependencies

```
$ cd next-auth-starter
$ npm install
npm WARN EBADENGINE Unsupported engine {
npm WARN EBADENGINE   package: 'next-auth@4.14.0',
npm WARN EBADENGINE   required: { node: '^12.19.0 || ^14.15.0 || ^16.13.0' },
npm WARN EBADENGINE   current: { node: 'v18.9.0', npm: '8.19.1' }
npm WARN EBADENGINE }
```

My default Node.js version is 18 - let's scale back to the latest version of v16 and use that instead.

```
$ nvm install 16
Downloading and installing node v16.18.0...
Now using node v16.18.0 (npm v8.19.2)

$ npm install     
(Success!)
```

---

3. Configure Local Environment


Copy the `.env.local.example` file to `.env.local` and customize it with the details of providers you want to use. The `.gitignore` configuration ignores all `.env*.local` files so your local configuration will not get checked in (i.e., useful purely for local dev).

This is what the template for that file looks like:

```
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET= # Linux: `openssl rand -hex 32` or go to https://generate-secret.now.sh/32

APPLE_ID=
APPLE_TEAM_ID=
APPLE_PRIVATE_KEY=
APPLE_KEY_ID=

AUTH0_ID=
AUTH0_SECRET=
AUTH0_ISSUER=

FACEBOOK_ID=
FACEBOOK_SECRET=

GITHUB_ID=
GITHUB_SECRET=

GOOGLE_ID=
GOOGLE_SECRET=

TWITTER_ID=
TWITTER_SECRET=

EMAIL_SERVER=smtp://username:password@smtp.example.com:587
EMAIL_FROM=NextAuth <noreply@example.com>

DATABASE_URL=sqlite://localhost/:memory:?synchronize=true

```

Note that next-auth has [many more built-in providers](https://next-auth.js.org/configuration/providers/oauth#built-in-providers) so we can also add in environment variables defined for other examples we want to enable. Let's configure this for the following and try it out. 
 - [Auth0](https://next-auth.js.org/providers/auth0)
 - [Azure Active Directory](https://next-auth.js.org/providers/azure-ad)
 - [Azure Active Directory B2C](https://next-auth.js.org/providers/azure-ad-b2c)
 - [GitHub](https://next-auth.js.org/providers/github)
 - [Google](https://next-auth.js.org/providers/google)
 - [LinkedIn](https://next-auth.js.org/providers/linkedin)
 - [Twitter](https://next-auth.js.org/providers/twitter)

You can also [add new built-in providers](https://next-auth.js.org/configuration/providers/oauth#adding-a-new-built-in-provider) by sending a PR.

---

4. Configure GitHub 

Setup a [new OAuth application](https://github.com/settings/applications/new) -  use [this tutorial](https://www.nextauth.org/add-github-authentication-to-nextjs) for guidance if useful. Here's what my registration looked like.

![My GitHub OAuth Config](./img/next-auth-github.png)

Clicking register takes you to the OAuth app page - where you should see  
- a generated `Client ID` 
- a button to `Generate a new client secret`.

Copy the Client ID to `GITHUB_ID` in the _.env.local_ file. Then click to generate secret - and copy it rightaway (you only see it once) to the `GITHUB_SECRET` env variable in the same file.

**Note: If you change .env.local settings at any time, you must restart dev server if it was running already!**

We'll configure more providers later - but let's try finishing setup with one first so we can test a next-auth workflow.

--- 

5. Database setup

If you are using the option to _bring your own database_ (in other words, you want to store the user/password/sessions data) - then this is where you configure the database.

 - Check out [adapters](https://next-auth.js.org/adapters/overview) for supported databases
 - Check out [create an adapter](https://next-auth.js.org/tutorials/creating-a-database-adapter) to contribute a new one


**Note: There is currently no adapter for CosmosDB or any Azure Database. A good place to contribute one if useful!**

You can use Next-Auth without a database if you use OAuth for authentication. For now that is what we are doing with GitHub, so let's move on.

If you don't specify a database, Next-Auth uses [JWT (JSON Web Tokens)](https://jwt.io/introduction) by default, to securely transmit auth information.

---

6. Preview Next-Auth app

Let's see if we got this all configured right:

```
$ npm run dev


> dev
> next

ready - started server on 0.0.0.0:3000, url: http://localhost:3000
info  - Loaded env from /Users/nitya/Documents/GitHub/nitya/next-auth-starter/.env.local
```

---

## Next Steps

Things to work on next:
 - Deploy basic app to [Azure Static Web Apps](https://learn.microsoft.com/en-us/azure/static-web-apps/deploy-nextjs-static-export?tabs=github-actions)
    - Validate it works with default /api and /auth routes in SWA
    - Understand how auth/api configuration is impacted 
 - Explore adding [Azure](https://benjaminwfox.com/blog/tech/how-to-configure-azure-b2c-with-nextjs) as Auth provider with next-auth.
    - Validate for Azure AD
    - Validate for Azure AD B2C
 - Explore creating custom React components (refresh UI)
    - Create [custom login pages](https://youtu.be/kB6YNYZ63fw)
    - Explore [Material-UI](https://github.com/TimMikeladze/next-auth-mui) components
 - Explore next-auth customizations for backend
    - [Workflow for bring-your-own-backend](https://arunoda.me/blog/add-auth-support-to-a-next-js-app-with-a-custom-backend)
    - [Authentication Patterns in next.js](https://nextjs.org/docs/authentication)


---

# Demo Walkthrough

Here's a walkthrough of the demo.

| Screenshot | Description |
|:---|:--- |
|![](./img/next-auth-github.png) | |
|![](./img/next-auth-guest1-api.png) | |
|![](./img/next-auth-guest1-client.png) | |
|![](./img/next-auth-guest1-landing.png) | |
|![](./img/next-auth-guest1-protected.png) | |
|![](./img/next-auth-guest1-server.png) | |
|![](./img/next-auth-guest2-login.png) | |
|![](./img/next-auth-guest3-login-undefined.png) | |
|![](./img/next-auth-guest3-login-undefined.png) | |
|![](./img/next-auth-guest4-login-github.png) | |
|![](./img/next-auth-user1-landing.png) | |
|![](./img/next-auth-user2-client.png) | |
|![](./img/next-auth-user3-server.png) | |
|![](./img/next-auth-user4-protected.png) | |
|![](./img/next-auth-user5-api.png) | |
|![](./img/next-auth-user6-admin.png) | |
|![](./img/next-auth-user7-me.png) | |

