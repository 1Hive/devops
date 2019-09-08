# Aragon App Checklist 

A checklist to prepare our apps to be audited and/or released.

<br />

### Dev Ops
- linting
- testing
- release

### Documentation
- overview
- user guide
- integration guide
- technical documentation
- testing documentation

### Demo
- script to deploy a DAO template with Redemptions locally for hacking
- deployed DAO that people can visit via a URL to interact with the app in < 1min

<br />

## Dev Ops

### Linting

The style guide and apps/formatting we use to enforce that style goes here.

### Testing

This should include a document describing the kinds of tests that we are running, what we expect them to catch, and also what we are not testing for that needs further review. 

We will also be running [CryticCI](https://crytic.io/) with every build. Currently this includes Slither and our unit tests. In the future it will include [Echinda](https://github.com/crytic/echidna), [Manticore](https://github.com/trailofbits/manticore), and more. 

### Release

Making it clear and unambigious what code was actually deployed, what changes were made since the last release and why, and how people can verify that against our documentation and security reviews.

<br />

## Documentation

### README

A developer focused synopsis of everything needed to quickly start hacking on Redemptions.

### User Guide

Walks the user through how to interact with the app to fulfill it's objectives. This can include written text as well as pictures, gifs, and videos. Should be informative, but to the point.

### Integration Guide

Walks developers through the steps required to add the app to their DAO. This can include written text as well as pictures, gifs, and videos. Should be informative, but to the point.

### Infographics

Visual representation of every component of the app. This includes internal processes as well as how the app interacts without outside contracts or users.

### Technical Documentation

Explains each function in the app, what it does, and any unusual things to look out for. This will be a stand alone document as well as detailed code comments explaining every function. This will also include a diagram that allows developers (or auditors) to visually see how the app is intended to function.

### Testing Documentation

This will describe the tests that we are running, what we expect them to catch, and also what we are not testing for that needs further review. This will allow anyone to easily understand the security of our applications at any point, and will also allow developers or auditors to easily re-run these tests to verify the results themselves. This will also link to our release proecess which will include instructions on how to verify that the deployed contract matches the source code that all these tests are being run against.  

<br />

## Demo

A working Aragon DAO that users can interact with to understand how the app works.
- A local deployment template for devs to interact with and hack on.
- A deployed DAO that users can interact with by visiting a URL.

<br />
