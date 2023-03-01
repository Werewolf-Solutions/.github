# Welcome to Werewolf Solutions

## Requirements

- MongoDB local or cluster

- Node/npm

- Stripe account

## Install

- production

  `npm install`

- dev

  `npm run dev-install`

## Edit .env Variables

- open .env_sample with any text editor

  - ex with nano

    `nano .env_sample`

- edit the file with your variables and change the name in .env

  - ex with nano

    change variables => CTRL+X => Y => delete \_sample => ENTER => Y

```
# Mongo db connection

MONGO_USERNAME='username'
MONGO_PASSWORD='password'
MONGO_HOSTNAME='hostname'
MONGO_DB_NAME='db_name'

# Session / Cookie

SESSION_SECRET='secret'
SESSION_NAME='session_name'

# Stripe
STRIPE_API_KEY='stripe_api_key'

# Port
PORT='your_port'

# Admin email
ADMIN_EMAIL='admin@email.com'
```

## Scripts

- run only if .env variables are production ready

  `npm start: run production`

- production test

  `npm test-prod`

- only frontend (this is not working right now => TODO: missing API comunication/dummy data)

  `npm run frontend`

- run only server (use it with insomnia/postman, TODO: give insomnia config)

  `npm run server`

- run concurrently server and frontend

  `npm run dev`

- build react for production

  `npm run build`

## Sign Up as Admin

- use the email you entered in .env to sign up with any password you want

# How to Contribute

TODO: give IDE config
TODO: git branch workflow
TODO: OKRs, TODOs workflow
TODO: discord, telegram

## New Branch

- feature/feature-name - for update or create a feature

- docs/doc-name - for update docs

# API

TODO: write API docs @ https://werewolf.solutions/docs

URL = https://werewolf.solutions/

endpoints:

- /users

  - / - GET - get user signed in

  - /sign-in - POST - { email, password }

  - /sign-up - POST - { email, password, password2 }

- /api

  - /accounting - POST - { budgetId } - it runs accounting function for budget selected

  - budget

    - /add-budget - POST - { name, currency }
    - /delete-budget - POST - { budgetId }
    - [not-working] /edit-budget - POST - { budgetId, budget }
    - /get-budget-history - POST - { budgetId } - it gets history of daily changes (dev logs)

  - bank account = {
    name: String,
    amount: Number,
    start_amount: Number,
    currency: String,
    date: Date, "2022-10-20T00:00:00.000Z"
    bank_name: String,
    },

    - /add-bank-account - POST - {budgetId , bankAccount = {name, amount, date}}
    - /delete-bank-account - POST - {budgetId, bankAccountId}
    - [not-working] /edit-bank-account - POST - budgetId , bankAccount = {name, amount, date}

  - fixed cost = {
    name: String,
    amount: Number,
    currency: String,
    due_day: Number,
    frequency: String,
    to: String,
    due_date: Date,
    formatted_date: String,
    from: {
    \_id: String,
    name: String,
    }
    notes: String,
    }

    - /add-fixed-cost - POST - { budgetId, fixedCost = {
      name,
      amount,
      currency,
      date,
      frequency,
      to,
      from: bankAccountId,
      notes,
      } }
    - /delete-fixed-cost - POST - { budgetId, fixedCostId }
    - [not-working] /edit-fixed-cost

  - future cost = {
    name: String,
    amount: Number,
    currency: String,
    date: Date,
    formatted_date: String,
    to: String,
    label: String,
    from: {
    \_id: String,
    name: String,
    },
    notes: String,
    is_passed: {
    type: Boolean,
    default: false,
    },
    }

    - /add-future-cost - POST - { budgetId, futureCost = {
      name,
      amount,
      currency,
      date,
      to,
      from: bankAccountId,
      notes,
      } }
    - /delete-future-cost - POST - { budgetId, futureCostId }
    - [not-working] /edit-future-cost

  - variable cost = {
    name: String,
    amount: Number,
    currency: String,
    date: Date,
    formatted_date: String,
    to: String,
    label: String,
    from: {
    \_id: String,
    name: String,
    },
    notes: String,
    }

    - /add-variable-cost - POST - { budgetId, variableCost = {
      name,
      amount,
      currency,
      date,
      to,
      from: bankAccountId,
      notes,
      }}
    - /delete-variable-cost - POST - { budgetId, variableCostId }
    - [not-working] /edit-variable-cost

  - income = {
    name: String,
    date: Date,
    formatted_date: String,
    amount: Number,
    currency: String,
    from: String,
    to: {
    \_id: String,
    name: String,
    },
    shift: {
    hours: Number,
    minutes: Number,
    },
    notes: String,
    }

    - /add-income - POST - { budgetId, income = {
      name,
      amount,
      currency,
      date,
      to: bankAccountId,
      from,
      notes,
      shift: {
      hours,
      minutes,
      },
      }}
    - /delete-income - POST - { budgetId, incomeId }
    - [not-working] /edit-income
