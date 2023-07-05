# Frontend Testing

## 6 types of Frontend testing
https://www.browserstack.com/guide/front-end-testing

1. Unit testing ✨
2. Visual regression testing ✨
3. Cross browser testing (depends on requirements)
4. Integration testing ✨
5. Accessibility testing (depends on requirements)
6. Acceptance testing ✨

---

# Unit Test

## What to unit test in a React App
https://medium.com/finnovate-io/what-to-unit-test-in-a-react-app-16be58d2e941

Keep components small to unit test properly

write the app in such a way so that there are small, individually unit-testable pieces. Keep components small by:

- Breaking a large component down into smaller components
- Abstracting logic that is state dependent with custom hooks
- Abstracting logic that is NOT state dependent with pure functions
- Manage global application state with Redux

**Level 1 — Pure functions**

- A pure function is a function that is deterministic.
- When given a certain input, a pure function will always return the same output every time without any side effects.
- Pure functions can be tested without any special library or tools.

Ex: a calculation function

**Level 2 — Functions with side effects**

- Inevitably, we will have functions that return results based on more than its input parameters. In a React app, we will have functions that make API calls.
- Such functions can only be tests by “mocking” actual API call outs. Keep in mind that unit tests should be executed entirely in memory, meaning it should not have dependencies on external systems, or the internet for that matter.
- For example, a function can call another function to make changes to an outside variable. In such case, we can use spying techniques — also available via mock functions — to assert the expected modifications are made.

Ex: Custom react hooks, functions that make API calls

**Level 3 — Components**

- When unit testing React components, we should only focus on key UI elements and interactions. It is very difficult to assert the appearance of styles, so I would generally advise that we focus on functionality.
- Test Initial render
  - The unit test suite for a component should include a test case that asserts key elements returned by the initial rendering cycle
  - Ex: For form component, we should assert that a email address field, a password field and a submit button are rendered
- Test key component states
  - We should have a test case for each component state.
  - For example, when a user enters an invalid email address, our test case should assert that the proper error message is rendered by the component.
- Test side effects & callouts
  - We should have a test case for each interaction the component has with the outside world.
  - We do this by stubbing out imports or as props of the component with spying functions.
  - Ex: replace the imported function with a spying function to assert that the imported function is called when the component is mounted on the screen. 
  - Ex: feed a spying function to the component as the “onSubmit” prop to assert that “onSubmit” is called when the “Submit” button is pressed.

---

## React Testing Library Tutorial – How to Write Unit Tests for React Apps
https://www.freecodecamp.org/news/write-unit-tests-using-react-testing-library/#why-do-you-need-to-write-unit-tests

**Why Do You Need to Write Unit Tests?**

as the application grows, it might be difficult to test all the scenarios in the application and you might miss something. Even a small change might break the application if all the major functionality is not tested properly.

writing unit test cases covering all those scenarios which you're manually going through as a user. (not absolutely everything)


**What is the React Testing Library?**

The React Testing Library has a set of packages that help you test UI components in a user-centric way.

tests based on how the user interacts with the various elements displayed on the page.

**What Not to Test with the Testing Library**

Testing Library encourages you to avoid testing implementation details like the internals of a component you're testing

You may want to avoid testing the following implementation details:
- Internal state of a component
- Internal methods of a component
- Lifecycle methods of a component
- Child components

If you really want to test the states and context and stuff, check out (enzyme testing)[https://enzymejs.github.io/enzyme/]
- But these types of checks are not necessary for testing with the React testing library. Instead, in the React testing library, you check the behavior of the DOM when the user clicks on a button or submits a form and so on.

**How to Write Unit Test Cases**


- To select a single DOM element, you can use the `getBy`, `findBy`, or `queryBy` query
- To select multiple DOM elements, you can use the `getAllBy`, `findAllBy` or `queryAllBy` query
- `getBy` and `findBy` return an error if there is no match or more than one match
- `queryBy` returns null if there is no match and returns an error if there is more than one match
- `findBy` works well with asynchronous code but not with `getBy` and `queryBy`
- `getAllBy` returns an error if there is no match and returns an array of matches for one or more than one match
- `findAllBy` returns an error if there is no match and returns an array of matches for one or more than one match
- `queryAllBy` returns an empty array for no match and re

(View examples)[https://www.freecodecamp.org/news/write-unit-tests-using-react-testing-library/#why-do-you-need-to-write-unit-tests]

**Conclusion**

- React Testing library is amazing and has become a very popular tool with which to test React applications.

- Just remember that unlike enzyme testing library, you should not test for state changes when using React Testing Library.

- So we have not written test cases to check if the state correctly changes after the user types some text in the name, email, or password fields.

- In React Testing Library you check the behavior of DOM when the user clicks on a button or submits a form and so on instead of testing the internal state of the component.



## Frontend unit testing practices

### Component Test

Should you do component test?
- Depends on the project
- Suppose there's a form that needs to display the correct error state for the inputs, then component testing makes sense
- If you just do component test for things like cards and containers, yea sure, but it doesn't bring much value. 
- Do component test when it makes sense

How do I use data-testid attribute with a React Component Test?
https://stackoverflow.com/questions/75659831/how-do-i-use-data-testid-attribute-with-a-react-component-test


### MUI
How to use test-id in Material UI Textfield (Cypress)
https://stackoverflow.com/questions/62049553/how-to-use-test-id-in-material-ui-textfield



## Unit Testing Fraud: Why Code Coverage is a Lie
https://daily.dev/blog/unit-testing-fraud-why-code-coverage-is-a-lie

Code coverage, also called test coverage, identifies the percentage of your codebase that was exercised by unit tests.

The coverage report can be helpful in identifying untested code, but targeting a percentage of coverage does not equal quality-tested code. 

**The Pitfalls of Requiring High Code Coverage Percentage**
- Developers do just enough
- Coverage does not ensure quality
- High code coverage should not remove the need for a code review


**The Benefits of Code Coverage and Unit Tests**
- The whole idea of a coverage report is that it can help developers identify what portions of their codebase is covered by unit tests
- Some clients feel a necessity for a high coverage percentage for their product, and that’s okay. As developers and consultants, our job is to help the client understand what they need in an application solution.

**In Summary**
I understand my opinion may step on some toes, but let me wrap up this article with a summary:

A high coverage percentage does not equal quality-tested code.
A target coverage threshold should not take the place of code reviews.
Instead of putting most of the focus on a high percentage of code coverage, developers should understand ( and experience ) the incredible value of well-formed tests.
TDD, by definition, should allow developers to attain high coverage percentages. 



---
# End-to-end tests

## Should I mock APIs in end-to-end testing?
https://stackoverflow.com/questions/71969081/should-i-mock-apis-in-end-to-end-testing

My understanding here is that if you want to test only your front-end application (what is not E2E testing in my opinion) you can use unit tests instead. 

If you still want to test the user interface from the browser, then you can mock the APIs' responses, but still not being E2E testing. 

In case you want to perform an end-to-end testing, then you shouldn't mock any database or API call. The exception here is a third-party API that is not under your control. 

In that specific case you can mock it to have less external dependency in your tests, but if that third party changes and you are not aware of it, you wont't notice if it's mocked. Said that, if you mock third-party APIs be sure you have a fluent communication with the API provider to get alerts on changes before your app fails.


## Integration test VS End-to-end tests
unit test: test only one small bit of code in near isolation

integration test: test a bit of code and how it interacts with the larger system

end to end test: test the entire system from a user's perspective

So if you are mocking APIs, you aren't really doing an E2E anymore but more like an integration test for just the various parts of your front-end.


## What Not to Do When Writing E2E Tests
https://betterprogramming.pub/what-not-to-do-when-writing-e2e-tests-ef7b9d09cc81

E2E tests usually take the form of automated GUI tests that run against a live system.

In the web context, an end-to-end test runner often remotely automates a browser. That means that classic unit testing tools — mocking, stubbing, access to internal state, etc. — are generally unavailable.
> Some frameworks such as Cypress do provide XHR request and DOM mocking. This can be very useful, but keep in mind that, while these features may reduce flakiness, whenever you mock an external system you are decreasing the fidelity of your test.

**Don’t Write Them Without Defining the Reason**

Why are you writing these tests? In this paper², researchers identified two main reasons developers write these and other GUI tests:

1. Automated acceptance testing (an encapsulation of customer expectations).
2. Automated regression testing (preventing regression errors).

**Don’t Duplicate Coverage**

⚠️
Let’s say you’ve created a new UI component. If you can cover the functionality in a unit test (or whatever your particular framework calls it), do it there!

Unit tests are generally easier to maintain, less flakey, and less expensive to run in your CI pipeline.

💡
E2E tests should be covering the areas only they can cover. Usually, these are the big-picture user stories that span many components and views. We’re talking about big, high-value flows, like:
- Signing up.
- Logging in and out.
- Creating a new <whatever users create in your app> and sharing it.
- Updating a user’s profile information.

**Don’t Use a Single-Layer Architecture**

<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*oYt6pK8yqbwecjFGcRYOAw.png" />

- Tests difficult to understand and, hence, to debug. Mixing high-level and low-level logic will introduce way too much detail into the tests.
- Relatively unimportant UI changes will break lots of tests
- Large swaths of your test suite will need to be updated when the UI changes
- You won’t be able to reuse portions of test logic. This will create extra effort and headaches.

**Don’t Use Breakable Selectors**

Dont' use : CSS selectors, `:nth-child()` selector, scoping selectors like `.img-view .container.img-wrapper img`

Use: data-testid
- The `data-testid=”some-unique-slug”` attribute. This is an attribute added to the target element, solely to give the test a handle. It can be as descriptive as you want and, as long as the value is unique, the test will be able to find it. It is totally impervious to changes in layout, ID, styles, and even element type. Also, most developers/UX people know not to mess with it. This one is the silver bullet.

**data-testid=”some-unique-slug”**
- When you create an E2E test suite, it becomes a reflection of your app’s user interface
- UI changes all the time. You and your team need to accept and embrace this fact of end-to-end testing.

**Don’t Ignore Flaky Tests In**
- because E2E tests rely on live, external systems, it takes an extra effort to make sure they don’t randomly fail because of non-deterministic factors such as network conditions, current load on external services, etc.
- If the tests are too flaky, developers won’t trust them. The tests will become annoying instead of helpful.
- my advice is to either shore it up or remove it. Don’t leave it in there to tarnish the suite’s reputation.

---

# Other things about testing

## How to lint and test your code using git pre-commit hooks
https://www.danilucaci.com/blog/how-to-lint-and-test-code-using-git-pre-commit-hooks

Use git pre-commit hooks to run tests!
- run unit tests
- dry run integration tests

## Testing best practices
https://infinum.com/handbook/frontend/react/testing-best-practices

## The Ultimate Guide to Frontend Testing: Tips, Tools, and Best Practices
https://dev.to/josematoswork/the-ultimate-guide-to-frontend-testing-tips-tools-and-best-practices-pod

## Challenges of Automated FrontEnd Testing

**Consistently Evolving UI:**

In modern software, core libraries and third-party components must be upgraded every few months. Upgrading one library requires commensurate changes to all other necessary components. With every upgrade, all components need to be retested, including automation and testing tools. Latest APIs and functionalities must also be integrated, built, and handled within increasingly short timelines.

**Constantly Changing User Preferences:**

With new devices, browser, and operating system versions introduced every few months, user demands and preferences keep changing. For example, the pandemic caused an explosive increase in users’ demand/desire for video conferencing and streaming. These newer user demands must be identified and implemented without considerable delay.Of course, every time newer features are added, new tests need to be created and executed. One also has to keep testing existing aspects like website load speed (have new features slowed down the page?) or visual appeal (has the new button covered up the existing menu?) Essentially, the developers’ and testers’ work on a specific software never ends.

**Choosing the right Automation Tool:**

Effecting, periodic front-end testing requires automation. Manual testers cannot be expected to run tests every time an upgrade is pushed. However, choosing an automation tool that can be effectively set up and empowered with test scripts to run requisite checks and verifications. However, with the plethora of automation testing tools available, it can be somewhat challenging to select what would work best for your team, given their skill sets and project requirements. However, Selenium Webdriver, Cypress, TestCafe, and Playwright are some preferred frameworks for front-end testing.

**Detecting cross-browser and cross device issues:**

With thousands of browser versions and devices used worldwide to access the internet, testers must cover a massive range to equip a site or app for real-world usage. This can be challenging since new devices and browser versions are constantly released. To keep up, teams need access to real browsers and devices. An in-house device lab takes significant financial and human resources to set up, maintain and upgrade. Using test infra hosted on the cloud is more accessible, as in BrowserStack.

## Front End Testing Best Practices
https://www.browserstack.com/guide/front-end-testing

**Start with the testing pyramid:**

For testers and teams just starting with Front End testing, it’s a good idea to use it as a blueprint. That means: starting running unit tests, then moving on to integration testing, and finally, executing end-to-end testing. Once this structure is in place, achieving reasonably high test coverage will be relatively easy.
Dive deeper into the testing pipeline, and add more tests once the testing pyramid comes into action. Once unit tests, integration tests, and end-to-end tests are completed, it will be easier to expand the testing scope and include things like acceptance testing, visual testing, etc.

**Decide the Front End elements to be prioritized: **

Front End testing requires analyzing and verifying hundreds, sometimes thousands of UI and functional elements. The former includes formatting, CSS, text, and graphics, while the latter comprises forms, links, buttons, etc.
These elements must be prioritized for adequate testing to decide what gets tested first. For example, it makes sense to test page load time, basic text, images, and essential functions (adding to cart, payment) first, then move on to graphics and pop-ups. Check that all elements are visible and responsive, and then move on to verifying graphics and layout.

**Choose the right Front End testing tools:**

Outside of providing real browsers and devices for test execution (and this is a mandatory feature), the ideal Front End testing tool should offer ways to make the process as seamless as possible.
BrowserStack, for example, offers a range of debugging options, and pre-installed developer tools that testers can quickly access to identify and resolve bugs. It also offers integrations with a range of necessary tools spanning automation frameworks, CI/CD, build and playback, record and deploy, and much more.

In other words, find a tool that provides comprehensive resources covering every step of the testing pipeline. The tool should be able to let QAs run tests, identify bugs, file and forward bugs to other team members, debug, and deploy.

