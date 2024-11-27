# Introduction
Cypress is a javascript-based testing framework that enables testers to validate modern web applications.
You typically want to record when running tests in [Continuous Integration](https://docs.cypress.io/app/continuous-integration/overview), but you can also record your tests when running locally.
- if the node.js project is not created, run
```sh
npm init -y
```
- add cypress command to pachage.json scripts
```json
"scripts": {
  "test": "npx cypress run --config video=false",
  "cypress:open": "npx cypress open"
},
```
- run cypress (make sure that yarn is instralled). yarn will install cypress if it is not.
```sh
yarn run cypress:open
```
- edit the test file (check out syntaxes)
- to run cypress in command lines only
```sh
yarn test
```
# example of gitlab-ci.yml file
```sh
stages:
  - test
cypress_test:
  stage: test
  image: cypress/browsers:latest
  script:
    - yarn install
    - yarn start & npx wait-on http://localhost:3000
    - yarn test
```
# cypress test commands
- find and fill a text
```javascript
cy.get('input[name="Departure"]').type('Your text here');
```