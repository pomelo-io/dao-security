## General principles
The DAO Security (DAOS) project aims to assist EOS developers meet code auditors for reviewing the security aspect of their project. 

Instead of a traditional security firm private audit, the open nature of the audit process allows for better opportunities to discover bugs, vulnerabilites and optimizations. 

Auditors will be incentivized by the possibilities of learning and being rewarded for working on different projects, while developers will receive a lot more work and insights (thanks to the varied skillset of each individual auditors) than they may get from a traditional audit.

## Review of existing solutions
### Bug bounties
Like in web2, bug bounties platforms have emerged for Web3 projects ([Immunefi](https://immunefi.com/), [Hacken Proof](https://hackenproof.com/programs), etc.) that work directly with developers to provide a structure (terms, scope, etc.) for auditors to submit and get rewarded for their findings.

- [+] Well-suited for existing projects wishing to streamline their vulnerability disclosure process.
- [+] Can attract high-profile auditors if rewards are high enough (Immunefi proposes up to millions of $ for critical vulnerabilties in high-profile projects).
- [+] Better control over the disclosure / private communication of vulnerabilites (?)
- [-] Less reliable in terms of work done (no deadline, submissions timing is pretty much random, thorough review not guaranteed).
- [-] Less visibility as your bug bounty program gets listed with tons of others (with potentially higher rewards) for auditors to choose from.

### Code4rena
Code4rena offers "community-driven contests for smart contracts audits" (taken from the [docs](https://docs.code4rena.com/)). 

It works by setting up a window of several days (usually between 3 and 7) for auditors (called "wardens") to submit their findings, classified as gas optimizations, low, medium or high findings. At the end of the contest, the prize money provided by the project's developers is splitted according to the level of the findings and the amount of people that found it (more details [here](https://docs.code4rena.com/awarding/incentive-model-and-awards) in the docs).

See the docs for [Bug bounties vs audit contests](https://docs.code4rena.com/#bug-bounties-vs-c4-audit-contests) and [Traditional audits vs audit contests](https://docs.code4rena.com/#traditional-audits-vs-c4-audit-contests).

From my own experience with the audit process (having participated as a auditor in the [Golom contest](https://code4rena.com/contests/2022-07-golom-contest)):
- [+] The competition aspect acts as a motivation boost for finding critical vulnerabilites and wanting to "top the charts".
- [-] The documentation and code comments requirements before auditing are quite low and can lead to confusion when auditing (somehow counterbalanced with the rapid response of the project's developers but this not always the case).
- [-] Looong audit process delay (usually more than a month after the contest ended) as judges works with developers to process all the findings (even longer for the reward delivery). This makes it hard for auditors to rely on the platform for consistent earnings.
- [-] Low transparency and lack of information during the judging process (one of Code4rena's main improvement goal).
- [-] Reliant on the Github platforms for submitting, storing and processing findings (security implications ? decentralization ?). 