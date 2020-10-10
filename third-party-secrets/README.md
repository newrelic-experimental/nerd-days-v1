# Using Third Party Secrets to query a 3rd party service

A 60-minute workshop for understanding and utilizing Third Party Secrets in your New Relic Application.

The material assumes some exposure to New Relic One programmability. Ex: NRU's Programmability 101 course.

---

This workshop assumes you have **completed the following prerequisites:**

## Prerequisites Checklist

1. Setup a free New Relic account
2. Install the NR1 CLI
3. Setup your Dev environment
4. Build your sample app
5. NPM install the Nr1-community component library
6. Decide on which 3rd party service you want to fetch data from

### 1. Get a free New Relic Account

1. [Free Sign Up](https://newrelic.com/signup)
2. Ensure your new user is Full User and has the [Admin user group assigned](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-pricing-users/users-roles)

### 2. Installing NR1 CLI

1. Make sure you have the `NR1` CLI installed on your machine. Run the following command:<br> `command -v NR1` <br> If nothing shows up, it's not installed yet. Proceed to the next step. If it is installed, feel free to disregard step #2 below.
2. `OR` Install the `NR1` CLI tool [here](https://one.newrelic.com/launcher/developer-center.launcher).

### 3. Get your Dev environment ready

1. Install Node 10+ [NodeJs](https://nodejs.org/en/)
2. If you've installed Node.js, then you also have NPM installed which is needed
3. NPM install the [Nr1-community component library](https://www.npmjs.com/package/@newrelic/nr1-community/v/0.0.1-alpha.4)
4. be sure to run `npm install @newrelic/nr1-community@next` to grab the correct alpha package.

Need more help? see our [Dev environment setup guide](https://developer.newrelic.com/build-apps/set-up-dev-env)

### 4. Build the My Awesome Nerdpack

1. When install the `NR1` CLI tool be sure to follow all 6 steps in the Quick Start Guide to create your first application.
2. Open your application locally in your favorite code editor.

Need more help? see our [Hello World tutorial guide](https://developer.newrelic.com/build-apps/build-hello-world-app)

### 5. 3rd Party Service

1. Decide what 3rd party service you'd like to retrieve data from.
2. setup a Personal Access Token, API Key, or license key for that service with the proper READ permissions.

### Sample Application

You can find a simple sample application in this [REPO](https://github.com/jpvajda/nerddaysV1) to get you started!
