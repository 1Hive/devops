# Aragon App Checklist Notes

All the things that went into the Aragon App Checklist and/or things that are still being researched

## General

Follow the frameworks outlined by top security professionals to document and comment the code. This should make it easy for anyone to read through and understand what the app is supposed to do and why.
- [ETHSecurity Best Practices](https://www.ethsecurity.org/research-and-developer-resources/audit-research) ✔️ added to audit prep checklist
- [Consensys Security Best Practices](https://consensys.github.io/smart-contract-best-practices/) ~ ✔️ read through and applied where possible
- [Trail Of Bits pre security audit guidelines](https://blog.trailofbits.com/2018/04/06/how-to-prepare-for-a-security-audit/) ✔️ added to audit prep checklist 
- [OpenZeppelin pre security audit checklist](https://blog.zeppelin.solutions/follow-this-quality-checklist-before-an-audit-8cc6a0e44845?gi=ea2b8162e8c8) ✔️ added to audit prep checklist
- [Consensys Dilligence pre security audit guidelines](https://media.consensys.net/preparing-for-a-smart-contract-code-audit-83691200cb9c) ✔️ added to audit prep checklist
- [Audit the deployed contract, not just the GitHub repo!](https://media.consensys.net/audit-the-deployed-smart-contract-not-github-16082b2fcb1b) - ✔️ Incorporated as a to do item in our release process

Use Ethereum security tools on the Redemptions app to check for common blunders. If we find problems we should also figure out how to fix them.
- [ETHSecurity Recommended Tools](https://www.ethsecurity.org/research-and-developer-resources/tools)
- [Consensys Dilligence Recommended Tools](https://consensys.github.io/smart-contract-best-practices/security_tools/)

Prepare some kind of presentation like these, but aimed as a primer for an incoming security auditor rather than as a final report.
- [Trails Of Bits public security audit reports](https://github.com/trailofbits/publications#security-reviews)
    - [RSK blockchain](https://www.trailofbits.com/reports/RSKj.pdf)
    - [Sai stablecoin](https://www.trailofbits.com/reports/sai.pdf)
    - [LivePeer](https://www.trailofbits.com/reports/livepeer.pdf)
- [OpenZeppelin public security audit reports](https://blog.zeppelin.solutions/tagged/security)
- [Sigma Prime public security audit reports](https://github.com/sigp/public-audits)

^^ The report part might be overkill, but having a doc handy that outlines our thinking behind the app and main concerns would be good. That being said, IF we had such a doc it would greatly increase the chance that a security team would want to take a look at the app because they could spend more time testing out their new toys/products and less time taking care of basic stuff

<br>

## Solidity testing tools
- put here until I find the right place in the checklist - because often linters double as security tools, so...

[Trail of Bits Awesome Ethereum Security](https://github.com/crytic/awesome-ethereum-security)

[Consensys Diligence Recommended Security Tools](https://consensys.github.io/smart-contract-best-practices/security_tools/)

[ETHSecurity Recommended Tools](https://www.ethsecurity.org/research-and-developer-resources/tools)

Solidity Coverage
- [solidity-coverage](https://github.com/sc-forks/solidity-coverage)
- [Colony blog post explaining solidity-coverate](https://blog.colony.io/code-coverage-for-solidity-eecfa88668c2/)

Solhint
- [solhint](https://github.com/protofire/solhint)
- [Solhint blog post](https://medium.com/protofire-blog/solhint-an-advanced-linter-for-ethereums-solidity-c6b155aced7b)

<br>

## Important Contracts

Redemptions contract
- https://github.com/burrrata/redemptions-app/blob/master/contracts/Redemptions.sol

TokenManager contract
- this contract is recommended to (but not required to) plug into Redemptions, and if it does, it will be able to affect state
- todo: get more info on TokenManager or any other Aragon apps that could/would be configured to interact with and/or control Redemptions


## Checklist to preparing contracts/apps for a security audit

✔️ Important questions
- What’s the overall level of security for this product?
    - Unaudited and under active development.
- Can the contract be upgraded an/or what does the emergency stop proceedure look like?
    - The contract does not currently have a mechanism for upgrades, but at any time a DAO can vote to remove tokens from the Redemptions app or remove the app from the DAO altogether (the organization's tokens are managed by the Token Manager and underlying assets are held in the Vault, so removing Redemptions does not change token balances)
- Are all client data transactions handled securely?
    - Yes, via the Aragon client.
- Does it control funds?
    - Yes. It will be the main Vault for a DAO
- Are official decisions derived from it?
    - Yes. It will control how members of an organization can redeem community tokens for tradeable assets.
- What will change when Aragon upgrades to Solidity 0.5.X?
    - esp the [Constantinopal reintrancy attack](https://blog.smartdec.net/constantinople-hard-fork-makes-us-rethink-what-reentrancy-is-455716c53537)
- Summary: this is probably the most important and security sensitive app in the Dandelion Kit because it directly controls funds.

✔️ Software license
- A1 uses the AGPL. Just submitted a [PR](https://github.com/1Hive/redemptions-app/pull/44) to give Redemptions the same license

✔️ Build/Deployment guide
- Just created a PR to update the README to document all steps to take to go from a blank VM to a deployed app.

Code style / linting
- [Official Solidity style guide](https://solidity.readthedocs.io/en/develop/style-guide.html) - apparently this isn't very popular anymore?
- Currently we're using [Solium](https://github.com/duaraghav8/Solium).
    - https://github.com/1Hive/redemptions-app/blob/master/.soliumrc.json
    - Running `solium -d contracts/` and/or `solium --plugin zeppelin -d contracts/` returns many errors/warnings.
    - todo: fix them all
- OpenZeppelin actually chose to [depreciate their solium plugin](https://github.com/OpenZeppelin/openzeppelin-contracts/issues/508) and started using [solhint](https://github.com/protofire/solhint)
    - maybe we should switch to that?
    - tried it and it didn't do much - maybe I just don't have it configured correctly tho?
- Other Solidity code linters
    - (solcheck)[https://github.com/federicobond/solcheck] - has not been updated in 2 years and did not work when I tried it


Unit testing
- testing levels: unit testing, app testing, system testing (the app interacting with other contracts)
- [solidity coverage](https://www.npmjs.com/package/solidity-coverage) is a recommended testing library
- incorporate the e2e testing app that @rperez is developing
- current Redemptions testing: https://github.com/1Hive/redemptions-app/blob/master/test/RedemptionsTest.js
- Currently I beleive that all tests are passing.
    - double check that we're testing everything that needs to be tested
    - make sure we're testing in the context of the DAO interacting with Redemptions as well as just the contract itself

Bugs
- npm returns errors when installing: `found 510 vulnerabilities (27 low, 483 high)`

Dependencies
- make sure they're secure today (A1 apps have been audited)
- make sure that any dependencies Redemptions does rely on are funded and actively maintained so that they will continue to work in the future (Aragon is sitting on > 20million rn)
- make sure that Redemptions does not call any external contracts to modify it's state (it does, via the ACL, tokenManager)

Upgrades and circut breakers
- Can someone pause the contract if something goes wrong?
- Can someone upgrade the contract to fix future problems?

Documentation
- ✔️ README: add a section on how to contact the team regarding security disclosures
- Update README to this format: https://github.com/RichardLitt/standard-readme/blob/master/spec.md
- Spec: documentation specifying what each function does and how it fits into the context of the app or any external contracts that might call it. This is essential because security auditors will analyze the code based on what the specification says. Poor spec = poor audit = poor app. (a spec was put together when the app was first being built... where is that?)
    - from Consensys: "Your specification should describe, in plain English, how each function of a contract should work and how those functions should work together. Functions may be treated as “black boxes”; the specification should describe what goes in, what comes out, what should happen, and what should not. After this, outline the design decisions behind the intended behavior of your code, rather than alternative approaches you might have chosen. This will help clarify for yourself the alternatives, as well as how people may misinterpret or misuse your code."
- Diagram: visually represents the spec and shows how the contract operates and where any external data might come in and influence the state
- ✔️ (basic user docs added to README, but could be improved) Write user documentation. When in doubt, keep it simple.
- Deployment documentation: documented deployment process is essential in order to avoid introducing insecurities. Such a guide would include:
    - which compiler version to use for which contracts
    - the order in which contracts will be deployed
    - constructor parameters for initialization of each contract

Code comments
- Write code comments that follow the NatSpec format: https://solidity.readthedocs.io/en/develop/natspec-format.html
- Document functions that call external contracts as untrusted
-

<br>

## Internal Code Review

Manual code review
- Are there any potential integer overflow and/or underflows?
- Avoid state changes after external calls ([checks-effects-interactions pattern](http://solidity.readthedocs.io/en/develop/security-considerations.html?highlight=check%20effects#use-the-checks-effects-interactions-pattern))
- Are there any potential reentrancy vectors?
- Are there any external contracts that control this contract's state?
- Is there a transaction ordering dependence?
- Could the user accidentally misconfigure permissions to create vulnerabilities and/or loopholes?
- Who is the owner of the contract once it's deployed?

<br>

## Prep for external review

Automated code review
- todo: list and test all relevent ethereum security tools

Organize code repo for external review
- which contracts are only used for testing purposes, and are not part of the final system
    - everything in the `testing` folder
- which contracts are reused from audited code, or inherit heavily from audited code
    - none, although Redemptions does use the Aragon Vault and TokenManger apps which have been audited

Contribution guidelines
- ✔️ make it easy for people to engage and create value in a positive sum way
- ✔️ todo: create a more formalized process for contributions on the website
    - added bug bounty to website
    - spell checked everything
    - added sync script to pull in high level overview info on the dandelion apps to the main site

Bug bounties
- ✔️ Created an Issue to create HONEY and/or DAI bug bounties for security disclosures
- ✔️ Create PR to add bug bounties to main website
- ✔️ Talked to team about the appropriate scope and amount for bug bounties
    - currently using HONEY

Freeze the codebase
- the final step before handing everything over to a security auditor
- add bug bounties with DAI/ANT

Find someone willing to review it for cheap
- the internets recommended finding a security team who wants to test new tooling out on a real use case

<br>

## Potential Security Partners

### Potential Partners 
- [Trail of Bits](https://www.trailofbits.com/)
    - We're test driving [CryticCI](https://crytic.io/)
    - their actual security audits are expensive
- [Mixbytes](https://mixbytes.io/) (the team doing Autark's security audits): they can't give us an audit until our contracts are frozen
- [the teams the did security audits for A1](https://wiki.aragon.org/dev/security/) 
    - White Hat Group: I don't think these guys are available for hire anymore
    - [Consensys Diligence](https://diligence.consensys.net/): waiting for a response (MythX and audits)
    - [Authio](https://authio.org/): contacted via the form on their website, but no response
- [the teams that did security audits for MolochDAO](https://medium.com/nomic-labs-blog/moloch-dao-audit-report-f31505e85c70) 
    - [Nomic Labs](https://nomiclabs.io/): they're fully booked atm
- [Chainsecurity](https://chainsecurity.com/)
    - waiting for response
- [Quantstamp](https://quantstamp.com/)
    - waiting for response
- [SecurityInnovation](https://www.securityinnovation.com/)
    - waiting for response (btw they're corporate AF so probably not a good fit, but we'll see...)
- [SigmaPrime](https://sigmaprime.io/)
    - waiting for response

### [Aragon Association Security Review Pipeline](https://github.com/aragon/security-review)
- submitted a request for support: tldr is that if we need more funds they might help
    - https://github.com/aragon/security-review/issues/12 
