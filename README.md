# Lab 06 – Static Hosting with GitHub Pages

Welcome to Lab 06 of your assignment! In this lab, we will focus on setting up static hosting using GitHub Pages and integrating it with Travis CI for continuous integration.

## Continuous Integration Setup

We have reached a point in our Single Page Application (SPA) development where we can successfully compile the application for deployment. Now, let's set up the continuous integration process using Travis CI and the `gh-pages` branch.

### Understanding Travis CI Configuration

Travis CI requires a configuration file (`.travis.yml`) to manage integrations. Let's understand the sections of this file:

```yaml
language: node_js
node_js:
  - "stable"

branches:
  only:
  - master

cache:
  directories:
  - node_modules

install:
  - npm install
  - npm install -g yarn

script:
  #- yarn lint
  - yarn build
  - mv build/index.html build/404.html

deploy:
  provider: pages
  skip_cleanup: true
  github_token: $github_token
  local_dir: build
  on:
    branch: master
