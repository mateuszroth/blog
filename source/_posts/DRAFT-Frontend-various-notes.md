---
title: '[DRAFT] Frontend - miscellaneous notes'
tags:
  - Frontend
categories:
  - [Frontend]
date: 2019-11-01 17:55:26
---
# Styled Components

## Pros of

*   **styles are part of JavaScript** (CSS-in-JS) in this case and allow you to build components from CSS snippets
*   with styled components **you can build CSS dynamically based on props and state of the component**
*   **you don't have to create tons of class names** with related CSS declarations written somewhere else. Class names are generated automatically and you don’t have to care about them anymore.

# Terms

## Codemod 

Codemod is a script run against a codebase for example in purpose of updating the codebase automatically for new changes in the API of an updated library.

## Tree Shaking

// TODO

## Bundle Splitting

// TODO

## AMP

// TODO

Supported in Next.js.

## Frontend integration tests

// TODO

Integration tests may be based on **Selenium webdriver**, which may be combined with **chromedriver** to test in **headless Chrome**.

## Module/nomodule pattern

The module/nomodule pattern provides a reliable mechanism for serving modern JavaScript to modern browsers while still allowing older browsers to fall back to polyfilled ES5.
