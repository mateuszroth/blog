---
title: 'JavaScript Node.js Scripts'
tags:
  - Node.js
  - JavaScript
categories:
  - [Node.js, Scripts]
date: 2019-01-01 00:00:00
---
# Node.js Scripts
[Difference between a node module and a npm package](https://docs.npmjs.com/getting-started/packages): npm package might be not a single node module but it can consists of many node modules.

## How to create a npm package and publish it to NPM
* https://docs.npmjs.com/getting-started/creating-node-modules
* https://docs.npmjs.com/getting-started/publishing-npm-packages

### Short instruction to create a new npm package
First login to NPM using `npm adduser` or `npm login` command [source](https://docs.npmjs.com/getting-started/publishing-npm-packages#creating-a-user). Now go to a new project folder and run `npm init` and create an `index.js` file with `exports` object. Then run `npm publish`, now you can install your package in another project. You can also use `npm link` to link your package globally.

### Release a new version of a npm package
Simply use command `npm version <update_type>` where `<update_type>` is one of the semantic versioning release types, patch, minor, or major [source](https://docs.npmjs.com/getting-started/publishing-npm-packages#updating-the-package).

## Node Scripts

### Shebang line:
#! /usr/bin/env node 

### How to build a command line tool with shelljs
http://blog.npmjs.org/post/118810260230/building-a-simple-command-line-tool-with-npm

### How to build CLI with commander
https://medium.freecodecamp.org/writing-command-line-applications-in-nodejs-2cf8327eee2
