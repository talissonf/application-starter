# E-Com Plus Application Starter

Boilerplate for E-Com Plus apps with [Firebase](https://firebase.google.com/) Cloud Functions and GitHub Actions.

[CHANGELOG](https://github.com/ecomplus/application-starter/blob/master/CHANGELOG.md)

## Getting started

1. Start creating a [Firebase project](https://console.firebase.google.com/):
    - Analytics is not needed;
    - Set a nice project name (ID) and remember it;

2. Enter the project, go to _databases_ page (on menu) and _create database_:
    - Just bypass with default production mode and rules;

3. Get your Firebase token from CLI:
```bash
npm install -g firebase-tools
firebase login:ci
```

4. [Use this template](https://github.com/ecomplus/application-starter/generate) to generate a new repository for your application;

5. Go to your repository _settings_ tab and set the following _secrets_:
    - `FIREBASE_PROJECT_ID`: The ID (name) of your Firebase project;
    - `FIREBASE_TOKEN`: The token generated with `firebase-tools`;
    - `SERVER_OPERATOR_TOKEN`: Random (at least 16 bytes) admin token generated from CLI or [here](https://randomkeygen.com/);

## Next steps

Almost ready, time to :coffee: and code!

- Set `app_id`, `title` and optionally more fields on base app JSON at `functions/ecom-app.json` (check [Application object model](https://developers.e-com.plus/docs/api/#/store/applications/));

- Optionally edit `functions/lib/store-api/procedures.js` to configure custom [Store API Procedures](https://developers.e-com.plus/docs/api/#/store/procedures/) and specify the web-hooks your app should receive;

- Edit `functions/routes/ecom/webhooks.js` to handle received web-hooks from Store API properly;

- Add custom web app routes by creating new files to `functions/routes` folder;

- You may also create files at `functions/lib` folder to add abstractions included on your app source;

## Continuous integration

Every commit will trigger a new **deploy** (with [GitHub Actions](/actions)), then your app will be accessible at:

`https://us-central1-<project-id>.cloudfunctions.net/app/` :blush:

The `functions/assets/app.json` will be updated automatically with some package info and current Cloud Function endpoints, you can use it as body to [_Create new Application_](https://developers.e-com.plus/docs/api/#/store/applications/new-application) on Store API;

> You can skip deploy workflow by adding `[skip ci]` to the commit message.

Also, your app's access tokens to Store API will be **automatically refreshed** every 8 hours by scheduled workflow.

## Firebase tools

You can also use [`firebase-tools` CLI](https://firebase.google.com/docs/cli) to run tests/deploy with custom config or scripts.
