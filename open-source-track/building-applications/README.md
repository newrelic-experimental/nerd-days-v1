# Building applications on New Relic One

A 60-minute workshop for building New Relic One applications.

> **Note:** This session assumes some exposure to New Relic One programmability. (For example, [New Relic University's Programmability 101 course](https://learn.newrelic.com/series/webcasts/live-learncast-new-relic-one-programmability).)

## Prerequisites

> **Important!** Please install software, create accounts, or follow any other instructions **before** attending this Nerd Days session. This will ensure that you're ready for the hands-on labs. We want you to spend your lab time learning, rather than setting up your environment.

1. [A New Relic account](https://newrelic.com/signup) with [API key](https://docs.newrelic.com/docs/apis/get-started/intro-apis/types-new-relic-api-keys#personal-api-key) created
2. [NR1 CLI](#installing-nr1-cli)
3. [Nerdpack manager role](https://docs.newrelic.com/docs/accounts/accounts/roles-permissions/add-update-users)
4. [Node 10+](https://nodejs.org/en/)
5. Ability to start and view [‘My Awesome Nerdpack’](https://developer.newrelic.com/build-apps/build-hello-world-app)

### Installing NR1 CLI

1. Make sure you have the `nr1` CLI installed on your machine. Run the following command:<br> ```command -v nr1``` <br> If nothing shows up, it's not installed yet. Proceed to the next step. If it is installed, feel free to disregard step #2 below.
2. Install the `nr1` CLI tool [here](https://one.newrelic.com/launcher/developer-center.launcher). You can skip steps #5 and #6 in the Quick Start form as we'll run through these examples in this workshop.
    - **Important:** Make sure to do step **#4** of the Quick Start steps. This ensures your credentials are stored on your machine.
