# **Welcome to Werewolf Solutions**

The following is a set of guidelines for contributing to Werewolf Solutions, its softwares, libraries and so on, which are hosted in [Werewolf Solutions](https://github.com/Werewolf-Solutions) organization on GitHub.

You can check out the roadmap on [Trello](https://trello.com/b/V4uGaQJV/werewolf-solutions-roadmap).

Check out [Discord](https://discord.gg/Zvf2RBwE) and [Telegram](https://t.me/+U5HeS5RfvENJKxWo).

> These are mostly guidelines, not rules. Use your best judgment, and feel free to propose changes to this document in a pull request.

<div id="table-of-contents"></div>

## Table of contents

- [Code of Conduct](#code-of-conduct)

- [What should I know before I get started?](#what-should-i-know-before-i-get-started)

  - [Werewolf Dapp structure](#werewolf-dapp-structure)

  - [What is Werewolf Solutions?](#what-is-werewolf-solutions)

- [How Can I Contribute?](#how-can-i-contribute)

  - [Reporting Bugs](#reporting-bugs)

  - [Suggesting Enhancements](#suggesting-enhancements)

    - [Submit one](#submit-enhancement-suggestion)

  - [Your First Code Contribution](#your-first-code-contribution)

  - [Pull Requests](#pull-requests)

- [Styleguides](#styleguides)

  - [Git Commit Messages](#git-commit-messages)

  - [JavaScript Styleguide](#javascript-styleguide)

  - [Specs Styleguide](#specs-styleguide)

  - [Documentation Styleguide](#documentation-styleguide)

- [Additional Notes](#additional-notes)

  - [Issue and Pull Request Labels](#issue-and-pull-request-labels)

## **Code of conduct**

###### [Table Of Contents](#table-of-contents)

This project and everyone participating in it is governed by the [Werewolf Code of Conduct](https://github.com/Werewolf-Solutions/.github/tree/main/profile/CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to any member of the staff.

> **Note:** Please don't file an issue to ask a question. You'll get faster results by using the resources below.

<!--
TODO: add FAQ, forum in werewolf.solutions

We have an official message board with a detailed FAQ and where the community chimes in with helpful advice if you have questions.

* [FAQ](https://werewolf.solutions/FAQ)
-->

If chat is more your speed, you can join the team:

- Join the team : [Discord](https://discord.gg/usuHTZan), [Telegram](https://t.me/+IgwxaWzM-U9kUsG_)
  - Use the `#general` channel for general questions or discussion about Werewolf Solutions
  - Use the `#dev-help` channel for questions or discussion about writing or contributing to Werewolf Solutions softwares or any dev help
  - Use the `#enter-the-team` channel if you are a dev and you want to work in the team

## **What should I know before I get started?**

###### [Table Of Contents](#table-of-contents)

---

### **Werewolf Dapp structure**

- React App

  ```
    src/
    |-- apiCalls/
    |   |-- api.js                  # Contains functions for making custom API calls (e.g., to localhost:5000/api)
    |-- assets/
    |   |-- images/                 # Store image files
    |   |-- files/                  # Store other types of files (e.g., PDFs, documents)
    |   |-- videos/                 # Store video files
    |-- components/
    |   |-- Modals                  # Reusable header component
    |   |-- Buttons                 # Reusable footer component
    |   |-- ...                     # Other reusable components (Logo, ...)
    |-- layout/
    |   |-- Header                  # Reusable header component
    |   |-- Footer                  # Reusable footer component
    |-- pages/
    |   |-- Home                    # Page component for the home page
    |   |-- AboutUs                 # Page component for the about page
    |   |-- ContactUs               # Page component for the contact page
    |   |-- ...                     # Other page components
    |-- App.js                      # The main application component
    |-- index.js                    # Entry point for your React app
    |-- App.css                     # Global styles for the app
    |-- ...
  ```

  - apiCalls/: This directory contains modules for making API calls to your custom API. It helps keep your API-related logic organized and separate from your components.

  - assets/: This directory is used to store static assets such as images, files, and videos that your application may need. Keeping them here makes it easier to manage and reference these assets in your code.

  - components/: This directory holds reusable components that can be used across different pages and layouts in your application. Examples include Header, Footer, Buttons, and Input components.

  - layout/: Layout components define the overall structure of your app, such as the main layout that wraps your pages. You can have multiple layout components if your app has different layouts for different sections.

  - pages/: Page components represent different views or pages of your application. Each page component typically corresponds to a specific route or URL. Examples include Home, About, Contact, and other pages specific to your app.

  - App.js: This is the main application component where you set up routing, global state management, and the overall structure of your app.

    ```jsx
    import { Outlet } from "react-router-dom";
    import Header from "./layout/Header/Header";
    import Footer from "./layout/Footer/Footer";

    import "./app.css";

    function App() {
      return (
        <>
          <div className="background-image" />
          {/* <PopUp /> */}
          <Header />
          <div className="content">
            <Outlet />
          </div>
          <Footer />
        </>
      );
    }

    export default App;
    ```

  - index.js: The entry point of your React application, where you render the App component and mount it to the DOM.

    ```jsx
    import React from "react";
    import ReactDOM from "react-dom/client";
    import "./index.css";
    import ContactUs from "./pages/ContactUs.jsx/ContactUs";
    import AboutUs from "./pages/AboutUs/AboutUs";
    import { createBrowserRouter, RouterProvider } from "react-router-dom";
    import ErrorPage from "./layout/ErrorPage/ErrorPage";
    import App from "./App";
    import Home from "./pages/Home/Home";
    import Admin from "./pages/Admin/Admin";
    import SignIn from "./pages/Auth/SignIn";
    import SignUp from "./pages/Auth/SignUp";

    const router = createBrowserRouter([
      {
        path: "/",
        element: <App />,
        errorElement: <ErrorPage />,
        children: [
          {
            path: "/",
            element: <Home />,
          },
          {
            path: "/contact-us",
            element: <ContactUs />,
          },
          {
            path: "/about-us",
            element: <AboutUs />,
          },
          {
            path: "/admin",
            element: <Admin />,
          },
          {
            path: "/sign-in",
            element: <SignIn />,
          },
          {
            path: "/sign-up",
            element: <SignUp />,
          },
        ],
      },
    ]);

    const root = ReactDOM.createRoot(document.getElementById("root"));
    root.render(
      <React.StrictMode>
        <RouterProvider router={router} />
      </React.StrictMode>
    );
    ```

  - App.css: Global styles for your app that can be shared across components.

* backend

  ```
    e-commerce/
    |-- bin/
    |-- config/
    |   |-- db.js                       # Database configuration
    |-- controllers/                    # API Controllers
    |-- middleware/                     # Middlewares
    |-- models/                         # Mongoose schema
    |-- public/                         # React app
    |-- routes/                         # API routes
    |   |-- api/
    |   |   |-- v1/
    |   |   |   |-- auth.js             # API routes for authentication
    |   |   |   |-- payments.js         # API routes for payments
    |   |   |-- index.js                # API routes entry point
    |-- services/                       # Services
    |-- utils/                          # Utilities
    |-- .env_sample                     # Sample environment variables file
    |-- app.js                          # Express.js application setup
    |-- package.json                    # Dependencies and scripts
    |-- README.md                       # Project documentation
    |-- ...
  ```

  - controllers/paymentsController.js

  ```javascript
    const createPaymentIntentController = async () {
        // If stripe
        stripeCreatePaymentIntent()
        // If Paypal

        // If crypto

        // ...
  }
  ```

  - services/stripePaymentsService.js

  ```javascript
    const stripeCreatePaymentIntent = async () {
        try {
            let user;
            if (req.session && req.session.passport && req.session.passport.user) {
            user = await User.findById(req.session.passport.user);
            }
            const { amount, currency, paymentMethod, customer } = req.body;

            const payment_intent = await stripe.paymentIntents.create({
            amount,
            currency,
            payment_method: paymentMethod,
            customer,
            });

            if (user) {
            const existingPaymentIntent = user.payment_intents.find(
                (intent) => intent.id === payment_intent.id
            );
            if (existingPaymentIntent) {
                return res.json({ error: "Payment intent already exists" });
            }

            user.payment_intents.push(payment_intent);

            await user.save();
            }

            res.json({ payment_intent });
        } catch (error) {
            console.log(error);
            res.status(500).json({ error: error.message });
        }
  }
  ```

  - routes/api/v1/payments.js

  ```javascript
  router.post("/create-payment-intent", createPaymentIntentController);
  ```

### **What is Werewolf Solutions?**

<!--
TODO: finish white-paper

Check the [white paper](https://werewolf.solutions/white-paper) to have an in depth understanding of what [Werewolf Solutions](https://werewolf.solutions) aims to be.

-->

In short I'd like to have a completly open source hardware and software development company, governed by a DAO, where everyone can collaborate to create solutions to make the world a better place.

Think about it like a collection of ideas and projects within a network of entrepreneurs, developers and makers.

## **How can I contribute?**

###### [Table Of Contents](#table-of-contents)

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

**1. Fork the Project**

- Create your Branch

  - New Feature (`git checkout -b feature/AmazingFeature`)
  - Bug Fix (`git checkout -b bugfix/SomethingToFix`)

- Commit your Changes (`git commit -m 'Add some AmazingFeature'` or `git commit -m 'Fix SomethingToFix'`)

- Push to the Branch (`git push origin feature/AmazingFeature` or `git checkout -b bugfix/SomethingToFix`)

- Open a Pull Request

**2. Work on an existing branch**

- Update all the branches (`git fetch --all`)

- Checkout to that branch (`git checkout branch_name`)

- Update to the latest (`git pull`)

- **contact the dev to see what's the best way to work together**

### **Reporting bugs**

> This section guides you through submitting a bug report for any repo in Werewolf Solutions. Following these guidelines helps maintainers and the community understand your report :pencil:, reproduce the behavior :computer:, and find related reports :mag_right:.

Before creating bug reports, please check [this list](#before-submitting-a-bug-report) as you might find out that you don't need to create one. When you are creating a bug report, please **_include as many details as possible_**.

Fill out [the required template](https://github.com/Werewolf-Solutions/.github/tree/main/profile/BUG_REPORT.md), the information it asks for helps us resolve issues faster.

> **Note:** If you find a **Closed** issue that seems like it is the same thing that you're experiencing, open a new issue and include a link to the original issue in the body of your new one.

#### Before submitting a bug report

<!--
TODO: create https://werewolf.solutions/FAQ
- **Check the [FAQs on the forum](https://werewolf.solutions/FAQ)** for a list of common questions and problems.

-->

- **Determine [which repository the problem should be reported in](#werewolf-solutions-structure)**.
- **Perform a [cursory search](https://github.com/search?q=+is%3Aissue+user%3AWerewolf-Solutions)** to see if the problem has already been reported. If it has **and the issue is still open**, add a comment to the existing issue instead of opening a new one.

### **How do I submit a (good) bug report?**

###### [Table Of Contents](#table-of-contents)

Bugs are tracked as [GitHub issues](https://guides.github.com/features/issues/). After you've determined [which repository](#werewolf-solutions-structure) your bug is related to, create an issue on that repository and provide the following information by filling in [the template](https://github.com/Werewolf-Solutions/.github/tree/main/profile/BUG_REPORT.md).

Explain the problem and include additional details to help maintainers reproduce the problem:

- **Use a clear and descriptive title** for the issue to identify the problem.

- **Describe the exact steps which reproduce the problem** in as many details as possible. For example, start by explaining how you started, e.g. which command exactly you used in the terminal. When listing steps, **don't just say what you did, but explain how you did it**.

- **Provide specific examples to demonstrate the steps**. Include links to files or GitHub projects, or copy/pasteable snippets, which you use in those examples. If you're providing snippets in the issue, use [Markdown code blocks](https://help.github.com/articles/markdown-basics/#multiple-lines).

- **Describe the behavior you observed after following the steps** and point out what exactly is the problem with that behavior.

- **Explain which behavior you expected to see instead and why.**

- **Include screenshots and animated GIFs** which show you following the described steps and clearly demonstrate the problem.

- **If you're reporting that the app crashed**

- **If the problem is related to performance or memory**

- **If the problem wasn't triggered by a specific action**, describe what you were doing before the problem happened and share more information using the guidelines below.

Provide more context by answering these questions:

- **Did the problem start happening recently** (e.g. after updating to a new version of the app) or was this always a problem?

- If the problem started happening recently, **can you reproduce the problem in an older version of the app?** What's the most recent version in which the problem doesn't happen?

- **Can you reliably reproduce the issue?** If not, provide details about how often the problem happens and under which conditions it normally happens.

- If the problem is related to working with files (e.g. opening and editing files), **does the problem happen for all files and projects or only some?** Does the problem happen only when working with local or remote files (e.g. on network drives), with files of a specific type (e.g. only JavaScript or Python files), with large files or files with very long lines, or with files in a specific encoding? Is there anything else special about the files you are using?

Include details about your configuration and environment:

- **Which version of the app are you using?**

- **What's the name and version of the OS you're using?**

- **Are you running the app in a virtual machine?** If so, which VM software are you using and which operating systems and versions are used for the host and the guest?

- **Are you using the app with multiple monitors?** If so, can you reproduce the problem when you use a single monitor?

### **Suggesting enhancements**

###### [Table Of Contents](#table-of-contents)

This section guides you through submitting an enhancement suggestion for the app, including completely new features and minor improvements to existing functionality. Following these guidelines helps maintainers and the community understand your suggestion :pencil: and find related suggestions :mag_right:.

Before creating enhancement suggestions, please check [this list](#before-submitting-an-enhancement-suggestion) as you might find out that you don't need to create one. When you are creating an enhancement suggestion, please [include as many details as possible](#how-do-i-submit-a-good-enhancement-suggestion). Fill in [the template](https://github.com/Werewolf-Solutions/.github/tree/main/profile/NEW_FEATURE.md), including the steps that you imagine you would take if the feature you're requesting existed.

### **Before submitting an enhancement suggestion**

<!--
- **Check the [debugging guide](https://werewolf.solutions/docs/debugging-guide)** for tips — you might discover that the enhancement is already available
-->

- **Check if there's already a branch or someone working on it on [Trello roadmap](https://trello.com/b/V4uGaQJV/werewolf-solutions-roadmap), [Discord](https://discord.gg/Zvf2RBwE) and in the right [repo](#werewolf-solutions-structure).**

- **Determine [which repository the enhancement should be suggested in](#werewolf-solutions-structure).**

- **Perform a [cursory search](https://github.com/search?q=+is%3Aissue+user%3AWerewolf-Solutions)** to see if the enhancement has already been suggested. If it has, add a comment to the existing issue instead of opening a new one.

### **Submit enhancement suggestion**

###### [Table Of Contents](#table-of-contents)

Enhancement suggestions are tracked as [GitHub issues](https://guides.github.com/features/issues/). After you've determined [which repository](#werewolf-solutions-structure) your enhancement suggestion is related to, create an issue on that repository and provide the following information:

- **Use a clear and descriptive title** for the issue to identify the suggestion.

- **Provide a step-by-step description of the suggested enhancement** in as many details as possible.

- **Provide specific examples to demonstrate the steps**. Include copy/pasteable snippets which you use in those examples, as [Markdown code blocks](https://help.github.com/articles/markdown-basics/#multiple-lines).

- **Describe the current behavior** and **explain which behavior you expected to see instead** and why.

- **Include screenshots and animated GIFs** which help you demonstrate the steps or point out the part of the app which the suggestion is related to.

- **Explain why this enhancement would be useful** to most the app users.

- **List some other applications where this enhancement exists.**

- **Specify which version of the app you're using.**

### **Your first code contribution**

###### [Table Of Contents](#table-of-contents)

<!--
TODO: write github issues labels

Unsure where to begin contributing to the app? You can start by looking through these `beginner` and `help-wanted` issues:

- [Beginner issues][beginner] - issues which should only require a few lines of code, and a test or two.

- [Help wanted issues][help-wanted] - issues which should be a bit more involved than `beginner` issues.

If you want to read about using the app or developing packages in the app, the [debugging guide](https://werewolf.solutions/docs/debugging-guide) is free and available online.
-->

#### Local development

The app Core and all softwares can be developed locally. For instructions on how to do this, see the [README](https://github.com/Werewolf-Solutions/werewolf-website)

### Pull requests

###### [Table Of Contents](#table-of-contents)

The process described here has several goals:

- Maintain the app's quality

- Fix problems that are important to users

- Engage the community in working toward the best possible the app

- Enable a sustainable system for the app's maintainers to review contributions

Please follow these steps to have your contribution considered by the maintainers:

1. Follow all instructions in [the template](https://github.com/Werewolf-Solutions/.github/tree/main/profile/PULL_REQUEST_TEMPLATE.md)

2. Follow the [styleguides](#styleguides)

<!--
3. After you submit your pull request, verify that all [status checks](https://help.github.com/articles/about-status-checks/) are passing <details><summary>What if the status checks are failing?</summary>If a status check is failing, and you believe that the failure is unrelated to your change, please leave a comment on the pull request explaining why you believe the failure is unrelated. A maintainer will re-run the status check for you. If we conclude that the failure was a false positive, then we will open an issue to track that problem with our status check suite.</details>
-->

While the prerequisites above must be satisfied prior to having your pull request reviewed, the reviewer(s) may ask you to complete additional design work, tests, or other changes before your pull request can be ultimately accepted.

## Styleguides

### Git commit messages

- Use the present tense ("Add feature" not "Added feature")
- Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit the first line to 72 characters or less
- Reference issues and pull requests liberally after the first line

<!--
??
- When only changing documentation, include `[ci skip]` in the commit title

??
- Consider starting the commit message with an applicable emoji:
  - :art: `:art:` when improving the format/structure of the code
  - :racehorse: `:racehorse:` when improving performance
  - :non-potable_water: `:non-potable_water:` when plugging memory leaks
  - :memo: `:memo:` when writing docs
  - :penguin: `:penguin:` when fixing something on Linux
  - :apple: `:apple:` when fixing something on macOS
  - :checkered_flag: `:checkered_flag:` when fixing something on Windows
  - :bug: `:bug:` when fixing a bug
  - :fire: `:fire:` when removing code or files
  - :green_heart: `:green_heart:` when fixing the CI build
  - :white_check_mark: `:white_check_mark:` when adding tests
  - :lock: `:lock:` when dealing with security
  - :arrow_up: `:arrow_up:` when upgrading dependencies
  - :arrow_down: `:arrow_down:` when downgrading dependencies
  - :shirt: `:shirt:` when removing linter warnings

-->

### JavaScript styleguide

<!--
TODO:

- add VScode config, like prettier, highlighting, ...

- add JS styleguide
-->

## Additional notes

#### Issue and pull request labels

###### [Table Of Contents](#table-of-contents)

<p align="right"><a href="#table-of-contents">Table Of Contents</a></p>

| Label name         | `Werewolf Solutions`:mag_right:                                                                               | Description                                |
| ------------------ | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| `to-fix`           | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AWerewolf-Solutions+label%3Ato-fix)           | To fix                                     |
| `bug`              | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AWerewolf-Solutions+label%3Abug)              | Something isn't working                    |
| `documentation`    | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AWerewolf-Solutions+label%3Adocumentation)    | Improvements or additions to documentation |
| `enhancement`      | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AWerewolf-Solutions+label%3Aenhancement)      | New feature or request                     |
| `good-first-issue` | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AWerewolf-Solutions+label%3Agood-first-issue) | Good for newcomers                         |
| `help-wanted`      | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AWerewolf-Solutions+label%3Ahelp-wanted)      | Extra attention is needed                  |
| `question`         | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+user%3AWerewolf-Solutions+label%3Aquestion)         | Further information is requested           |

| Label name         | `werewolf-website`:mag_right:                                                                                                    | Description                                |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| `to-fix`           | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+repo%3Awerewolf-solutions%2Fwerewolf-website+label%3Ato-fix)           | To fix in werewolf-website                 |
| `bug`              | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+repo%3Awerewolf-solutions%2Fwerewolf-website+label%3Abug)              | Something isn't working                    |
| `documentation`    | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+repo%3Awerewolf-solutions%2Fwerewolf-website+label%3Adocumentation)    | Improvements or additions to documentation |
| `enhancement`      | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+repo%3Awerewolf-solutions%2Fwerewolf-website+label%3Aenhancement)      | New feature or request                     |
| `good-first-issue` | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+repo%3Awerewolf-solutions%2Fwerewolf-website+label%3Agood-first-issue) | Good for newcomers                         |
| `help-wanted`      | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+repo%3Awerewolf-solutions%2Fwerewolf-website+label%3Ahelp-wanted)      | Extra attention is needed                  |
| `question`         | [search](https://github.com/search?q=is%3Aopen+is%3Aissue+repo%3Awerewolf-solutions%2Fwerewolf-website+label%3Aquestion)         | Further information is requested           |
