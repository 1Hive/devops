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
- technical specification

### Demo
- script to deploy a DAO template with Redemptions locally for hacking
- deployed DAO that people can visit via a URL to interact with the app in < 1min

<br />

## Dev Ops

### Linting

The apps/formatting we are using goes here.

### Testing

A description of the testing framework we're using goes here.

In addition, we can determine a set of Ethereum security apps to run (like Slither and Echinda) to catch errors as we go
- looking into using Trail of Bits [Crytic](https://blog.trailofbits.com/2019/08/02/crytic-continuous-assurance-for-smart-contracts/) (like CircleCI, but for Ethereum contract security)

### Release

Making it clear and unambigious what code was actually deployed, what changes were made since the last release and why, and how people can verify that against our documentation and security reviews.

<br />

## Documentation

### Overview

Explains the app from a high level, what it's main features are, and what it's intended use cases are.

Also shows crucial data points like the security audit status of the app, what networks it's deployed to, and the bug bounty policy.

### User Guide

Walks the user through how to interact with the app to fulfill it's objectives. This can include written text as well as pictures, gifs, and videos. Should be informative, but to the point.

### Integration Guide

Walks developers through the steps required to add the app to their DAO. This can include written text as well as pictures, gifs, and videos. Should be informative, but to the point.

### Infographics

Visual representation of every component of the app. This includes internal processes as well as how the app interacts without outside contracts or users.

### Technical Documentation

Explains each function in the app, what it does, and any unusual things to look out for. This will be a stand alone document as well as detailed code comments explaining every function. This will also include a wireframe that allows developers (or auditors) to visually see how the app is intended to function.

### README

A developer focused synopsis of everything needed to quickly start hacking on Redemptions.

<br />

## Demo

A working Aragon DAO that users can interact with to understand how the app works.
- A local deployment template for devs to interact with and hack on.
- A deployed DAO that users can interact with by visiting a URL.

<br />
