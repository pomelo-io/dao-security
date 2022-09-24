# DAO Security (DAOS)
## Table of contents
- [General principles](#general-principles)
- [Review of existing solutions](#review-of-existing-solutions)
  * [Bug bounties](#bug-bounties)
  * [Code4rena](#code4rena)
  * [EOS players](#eos-players)
- [Related metrics for context](#related-metrics-for-context)
  * [EOS](#eos)
  * [WAX](#wax)
  * [ETH](#eth)
  * [References](#references)
- [Design and architecture](#design-and-architecture)
  * [Overview](#overview)
  * [Audit process](#audit-process)
  * [Governance systems](#governance-systems)
    + [Bipartite system (operators/community)](#bipartite-system--operators-community-)
    + [Tripartite system (operators/judges/community)](#tripartite-system--operators-judges-community-)
    + [Eliminating operators](#eliminating-operators)
    + [Additional considerations](#additional-considerations)
    + [References](#references-1)
  * [Reward systems](#reward-systems)
    + [Self judging](#self-judging)
    + [Fully automated judging](#fully-automated-judging)
    + [External expert judging](#external-expert-judging)
    + [Hybrid approach](#hybrid-approach)
    + [References](#references-2)
  * [Security aspect](#security-aspect)
- [Technical specifications](#technical-specifications)
  * [Github as a supporting platform](#github-as-a-supporting-platform)
  * [Pomelo integration](#pomelo-integration)

## General principles
The DAO Security (DAOS) project aims to assist EOS developers in reviewing the security aspect of their project. 

Instead of a traditional security firm private audit, the open nature of the audit process allows for better opportunities to discover bugs, vulnerabilites and optimizations. 

Auditors will be incentivized by the possibilities of growing their skills and being rewarded for working on different projects, while developers will receive a lot more work and insights (thanks to the varied skillset of each individual auditors) than they may get from a traditional audit.

## Review of existing solutions
*A very good blog post explaining the differences between smart contract auditing approaches: https://thecryptospace.substack.com/p/audit-audit*

### Bug bounties
Like in web2, bug bounties platforms have emerged for Web3 projects ([Immunefi](https://immunefi.com/), [Hacken Proof](https://hackenproof.com/programs), etc.) that work directly with developers to provide a structure (terms, scope, etc.) for auditors to submit and get rewarded for their findings.

- [+] Well-suited for existing projects wishing to streamline their vulnerability disclosure process.
- [+] Can attract high-profile auditors if rewards are high enough (Immunefi proposes up to millions of $ for critical vulnerabilties in high-profile projects).
- [+] Better control over the disclosure / private communication of vulnerabilites (?)
- [-] Less reliable in terms of work done (no deadline, submissions timing is pretty much random, thorough review not guaranteed).
- [-] Less visibility as your bug bounty program gets listed with tons of others (with potentially higher rewards) for auditors to choose from.

### Code4rena
[Code4rena](https://code4rena.com) offers "community-driven contests for smart contracts audits" (taken from the [docs](https://docs.code4rena.com/)). As a unique project in the security audit domain, it serves as a base and reference for some of the ideas presented in this document.

**Sponsors** first contacts the core team for specifying their need for a codebase security audit of their project. After working out the details (like the prize pot size), the team sets up a time window of several days (usually between 3 and 7) for auditors (called **wardens**) to submit their findings. These findings are classified as either medium or high severity or bundled in one Quality Assurance (QA) report (also containing gas optimizations for Ethereum-based projects). 

At the end of the contest, the submissions are closed and the contest enters into the judging phase where a **judge** (rarely more than one) will be appointed for evaluating the validity and quality of the findings. For all findings, they will flag duplicates that multiple wardens may have reported as they have no way of knowing if the vulnerability they've found hasn't also be found by others. 

For high and medium severity findings, judges need to assess if the risk is present (high ~= immediate loss of funds, medium ~= potential risk see [Judging criteria](https://docs.code4rena.com/awarding/judging-criteria)) and have the ability to downgrade (or sometime upgrade) a finding based on their judgment. Wardens will then be compensated according to a exponential decay formula taking into account the risk and amount of auditors who found the same vulnerability (see [Incentive model and awards](https://docs.code4rena.com/awarding/incentive-model-and-awards)).

For QA reports, the judge assign a score (between 1-100) based on the quality of the report and auditors will be compensated according to the score of their report using a curve-based mechanism. The top scoring report will also be featured on the final audit publication.

Also see the docs for [Bug bounties vs audit contests](https://docs.code4rena.com/#bug-bounties-vs-c4-audit-contests), [Traditional audits vs audit contests](https://docs.code4rena.com/#traditional-audits-vs-c4-audit-contests) and feel free to explore to learn more about their processes.

From my own experience with the audit process (having participated as an auditor in the [Golom contest](https://code4rena.com/contests/2022-07-golom-contest)):
- [+] The competition aspect acts as a motivation boost for finding critical vulnerabilites and wanting to "top the charts".
- [-] The documentation and code comments requirements before auditing are quite low and can lead to confusion when auditing (somehow counterbalanced with the rapid response of the project's developers but this not always the case).
- [-] Looong audit process delay (usually more than a month after the contest ended) as judges works with developers to process all the findings (even longer for the reward delivery). This makes it hard for auditors to rely on the platform for consistent earnings.
- [-] Low transparency and lack of information during the judging process (one of Code4rena's main improvement goal).
- [-] Reliant on the Github platforms for submitting, storing and processing findings (*security implications? decentralization?*).

### EOS players
- [Certik](https://www.certik.com/products/security-audit): « A comprehensive security assessment of your smart contract and blockchain code to identify vulnerabilities and recommend ways to fix them. »
- [SlowMist](https://www.slowmist.com/): « Focusing on Blockchain Ecosystem Security
In security, slow is better, better will be more fast »
- [Sentnl](https://sentnl.io/): « Blockchain Security Audits »
- [EOS42](https://eos42.io/services/audit): « EOSIO Smart Contract Audits »
- [ImmuneBytes](https://immunebytes.com/): « A Smart Contract Auditing Solution »
- [EosAuditor](https://eosauditor.com/): smart contracts security audits (*doesn't seem very professional*)
- [Hacken](https://hacken.io/): « We make web3 a safer place »
- [Klevoya](https://klevoya.com/): used to provide audit services now acquired by Immunefi
- [Audit+](https://eosnetwork.com/blog/audit-blue-paper/): « Providing an overall framework for security analysis tooling and contract audit for EOSIO-based applications » (*very insightful, also this project could align with goal #1 and #5 of [blue paper](https://drive.google.com/file/d/1hQsN-_4DN5Lj9iDih0N41r8-ZeEpFRlr/view)*)

## Related metrics for context

### EOS
| Metric | Value |
| ------ | ----- |
| Numbers of projects [1] | ~500 |
| Users [1] | ~425k for the top 25 projects (~500 for Pomelo) |
| Type of projects [1] | Slightly more Gaming, DeFi, Exchanges |
| Open-source repos [3] | 670 repos on Github with tag EOS |
| Total EOS [2] | 1,065,284,439 |
| Staked EOS [2] | 354,476,937 |
| Circulating EOS [2] | 710,807,502 |
| Staked to circulation ratio [2] | 50% |
| Number of smart contracts (15 Nov. 2019) [7] | ~55,000 |
| Number of recorded attacks on smart contracts (2018-2019) [6] | 113 |

### WAX
| Metric | Value |
| ------ | ----- |
| Numbers of projects [1] | ~225 |
| Users [1] | 1.5M+ for the top 25 projects |
| Type of projects [1] | Almost exclusively Gaming, some Exchanges and miscs |
| Open-source repos [3] | 50 repos on Github with tag WAX |
| Total WAX [2] | 3,931,361,230 |
| Staked WAX [2] | 1,670,258,769 |
| Circulating WAX [2] | 2,261,102,460 |
| Staked to circulation ratio [2] | 74% |

### ETH
| Metric | Value |
| ------ | ----- |
| Numbers of projects [1] | ~3500 |
| Users [1] | ~400k for the top 25 projects |
| Type of projects [1] | Marketplace, DeFi, Exchanges, miscs  |
| Open-source repos [3] | 15k+ repos on Github with tag ETHEREUM |
| Total ETH [4] | 122,370,574 |
| Staked ETH [5] | 14,441,062 |
| Circulating ETH [4] | 122,370,574 |
| Staked to circulation ratio | 12% |
| Number of smart contracts (15 Nov. 2019) [10] | ~20M |
| Number of recorded attacks on smart contracts (Q1-Q2 2022) [8,9] | 113 |

### References
1. [Top EOS Dapps. (n.d.). DappRadar. Retrieved September 14, 2022](https://dappradar.com/rankings/protocol/eos)
2. [Fastest EOS Block Explorer and Wallet. (n.d.). Retrieved September 14, 2022](https://bloks.io/#statistics)
3. [Build software better, together. (n.d.). GitHub. Retrieved September 14, 2022](https://github.com/topics/)
4. [Sephton, C. (n.d.). Ethereum price today, ETH to USD live, marketcap and chart. CoinMarketCap. Retrieved September 14, 2022](https://coinmarketcap.com/currencies/ethereum/)
5. [Ethereum (ETH) Blockchain Metrics & Charts. (n.d.). Staking Rewards. Retrieved September 14, 2022](https://www.stakingrewards.com/earn/ethereum-2-0/metrics/)
6. [Ningyu He, Haoyu Wang, Lei Wu, Xiapu Luo, Yao Guo, and Xiangqun Chen. 2022. A Survey on EOSIO Systems Security: Vulnerability, Attack, and Mitigation. 1, 1 (July 2022), 34 pages.](https://doi.org/10.1145/nnnnnnn.nnnnnnn)
7. [He, N., Zhang, R., Wu, L., Wang, H., Luo, X., Guo, Y., ... & Jiang, X. (2020). Security analysis of EOSIO smart contracts. arXiv preprint arXiv:2003.06568.](https://www.usenix.org/system/files/sec21fall-he-ningyu.pdf)
8. [HACK3D: The Web3 Security Quarterly Report - Q1 2022 - Blog - CertiK Security Leaderboard. (n.d.). Retrieved September 15, 2022](https://4972390.fs1.hubspotusercontent-na1.net/hubfs/4972390/Marketing/Web3%20Security%20Q1%202022.pdf)
9. [HACK3D: The Web3 Security Quarterly Report - Q2 2022 - Blog - CertiK Security Leaderboard. (n.d.). Retrieved September 15, 2022](https://4972390.fs1.hubspotusercontent-na1.net/hubfs/4972390/Marketing/Web3%20Security%20Q2-2022-v4.pdf)
10. [Ethereum Smart Contracts Creation. (n.d.). Retrieved September 15, 2022](https://dune.com/queries/649454/1207174)

## Design and architecture
As a foreword to the design and architecture of a DAO-like system, it should be noted that such an organization requires quite a few individuals to run efficiently and in a way that the *decentralized* nature of the system would not be compromised.

~~As such, it would be best to first assess if the EOS ecosystem is capable of supporting a security-focused community of developers and auditors before launching any big project towards the creation of a DAO.~~ (*don't worry about this part*)

The goals and mode of operation of the DAO should also be aligned with the needs of day-to-day EOS developers. Developers and their projects comes first with the DAO helping them grow secure and resilient products through code audits.

Since there isn't currently anything like it in the space, this project could also be the spark needed for bringing auditors and raising awareness about the security of on-chain EOS contracts.

### Overview
One thing that started to become very apparent after the first discussions with the team is that **the DAOS project is all about communication**. DAOS acts as the intermediary between *clients* and *auditors* (also known as *the community*).

Clients should not expect DAOS to write code for them, fix infrastructure issues, run pentesting or anything like that. They communicate their need for an audit of a codebase and receive a detailed report highlighting the potential issues found by the community.

Auditors receive the code and start working **on their own**, communicating any findings to the DAO as part of the auditing process. In exchange, they get a reward based on their contribution effort to the overall audit. They should not expect anything else but transparency and communication from the DAO. In particular, no specific training, equipement or tools will be provided although how-to resources and beginner-friendly behavior are to be expected.

### Audit process
Code audit definition: *A software code audit is a comprehensive analysis of source code in a programming project with the intent of discovering bugs, security breaches or violations of programming conventions.* ([Wikipedia contributors. (2021, May 23). Code audit. Wikipedia. Retrieved September 19, 2022](https://en.wikipedia.org/wiki/Code_audit))

The purpose of auditing a smart contract is to eliminate as much as possible the risks of exploits and unexpected behavior that can occur from errors or overlooked issues in the code. The journey of translating a promising idea into code that runs on a public blockchain can be tedious with lots of pitfalls that developers and newcomers may not be aware of. That's why having a dozen or more pair of eyes look through every aspect of the code is useful for making dapps a safer place for users.

Clients are the ones who defines the **scope** of the audit by providing as much resources as they want (code, documentation, etc.). The DAO will be responsible for assessing the feasibility of the audit according to its own resources (available people, time, other audits, etc.). Clients are expected to supply a sufficient amount of context and documentation for the codebase they want to be audited.

Auditors will be provided the material, *potential reward amount?* and a **deadline** for which they have to send in all their work. They are aware of the **rules** (*WIP to be defined / accepted on join, audit start or submission?*) regarding audit submissions and the internal workings of the DAO (reward attribution, etc.). A communication channel (*direct? through DAO?*) shall be at the disposition of auditors for reaching the clients regarding any clarifications they may seek in order to perform the audit work.

\[*Draft flow based on Denis' feedback*\]
1. Project/Protocol/Team needs an audit.
2. It submits a request to DAOS operators who can assess if the request satisfies some minimal audit requirements (documentation, etc.).
3. DAOS operators initiates a Security Audit bounty request to its community. The duration of the bounty can be variable depending on the estimated amount of work required and/or community members availability and/or other factors. 
4. DAOS community accepts or rejects (*explicitly?*) the audit work.
5. DAOS operators rate contributions of effort per community member.
6. DAOS releases audit findings to project/team.
7. Project/Team approves or disapproves (*how to solve conflict ?*) DAOS' audit work
8. Funds released to DAOS community based on their contribution efforts.
9. DAOS releases a final audit report to the public (hosted on IPFS, *with permission?*).

### Governance systems
~~Auditors will probably want a say in how the rewards are distributed, how long the audit should take, what's an acceptable submission, etc.~~

A few possible systems for running the DAO are presented below.

#### Bipartite system (operators/community)
The DAO would be run by a set of **operators** that will be tasked to assess and submit audit requests to the community. They will also be responsible for evaluating the effort provided by community members on an audit as well as release funds and compile a final report to the public.

Initially, the founders of the DAO would act as the de-facto trusted operators. These are people who have the vision for the project and who are willing to put the best effort for running and growing the DAO's operations. In the future, active and well-established members of the community could be able to apply for working as an operator (*community vote?*). 

The rest of the DAO community are the auditors participating in the audit bounty. Anyone would be able to join the effort. A "contribution score" could be used to track members contribution over time (*some privileges?*, *blacklisting some toxic contributors?*).

#### Tripartite system (operators/judges/community)
In the tripartite system, **operators** acts the same way as in the bipartite system except for the part that they no longer evaluate directly the submissions of auditors.

Instead, similar to [Code4rena](#code4rena)'s approach, we separate the operational process of running the DAO and the judging of contests' submissions. **Judges** are the ones that are tasked with determining the individual effort provided by each auditor for a specific audit. They are highly-skilled members of the community (although they can't participate in *any?* audits themselves) who will use their background, judgement and knowledge of the rules (*judging rules used as a reference for judges*) to perform this task.

Judges would be ultimately appointed by operators with the community and other judges being able to recommend people they think would be a great fit. In any case, judges will require to justify from a certain level of experience and audit performance in the DAO (*passing test required?*) prior to being recruited.

#### Eliminating operators
In theory, it would be possible to remove the operator's role entierly:
- Pipelining and automating the whole process from the client's audit proposal to the final report compilation from the auditor's submissions.
- Using smart contracts for the storage, distribution and sending of audit rewards.
- Automating the communication channels setup with eventuals human-support roles for complex interactions.

Decisions requiring judgment such as resolving conflicts or approving a client's audit proposal would be submitted to the community for approval. A reputation-based system would be best suited for weighing each individual opinion that would ultimately decide on the outcome of the decision (see [1] and [2]).

The process of eliminating operators from the system could be the long-term goal of the DAO governance, ensuring that community members working for the best of the organization would be the one that have the most influence on the decisions taken (which should be the case for operators but there is a higher risk of collusion with such a small group of people).

#### Additional considerations
According to [3], one of the main components that differentiates a **D**ecentralized **A**utonomous **O**rganisation (DAO) from just a **D**ecentralized **A**pplication (DA) is *internal capital*. For DAOS, that would be the treasury used to reward auditors (and potentially others) for their work. Hence, mechanisms (such as multi-sig and more) need to be put in place for ensuring the safety and integrity of this internal capital or else the entire DAO structure would be at risk.

The word *Autonomous* is also a key part that caracterize a DAO as opposed to a simpler **D**ecentralized **O**rganisation (DO). There need to be some part of the system that is not prone to human decisions only, running the risk of collusion or malicious exploits of the DAO structure. Rules are one way of enforcing more autonomous evaluations, with invalid or fraudulent submissions/reports exposed to being flagged and rejected (either automatically or manually).

~~The system should allow for an (*active?*) auditor to raise questions of interest to the community and/or make voting proposals.~~

#### References
1. [Moving beyond coin voting governance. (2021, August 16). Retrieved September 21, 2022](https://vitalik.ca/general/2021/08/16/voting3.html)
2. [Levi, A. (2021, December 9). Reputation vs Tokens - DAOstack. Medium. Retrieved September 23, 2022](https://medium.com/daostack/reputation-vs-tokens-6d7642c7a538)
3. [Buterin, V. (2014, May 6). DAOs, DACs, DAs and More: An Incomplete Terminology Guide. Ethereum Foundation Blog. Retrieved September 21, 2022](https://blog.ethereum.org/2014/05/06/daos-dacs-das-and-more-an-incomplete-terminology-guide)

### Reward systems
One of the hardest part of setting up a DAO structure for conducting security audits is the attribution of rewards based on the individual efforts of each community member towards a particular audit. In a traditional audit firm, salaries (and potentially bonuses) are what incentivize auditors to perform to the best of their ability.

With people coming in-and-out of the audit process, from various backgrounds, skill levels and with different abilities to communicate effectively, another system must be put in place that shall be fair and rewarding for all these people.

*What are we measuring exactly ?*
- Resources spent: time, reports length and details
- Attributable results: number of valid findings, criticity, CPU/RAM optimization

#### Self judging

#### Fully automated judging

#### External expert judging
Using well-versed, recognized experts in the auditing field for judging the quality of auditors' submissions is one way of ensuring a fair distribution of rewards.

#### Hybrid approach

\[*WIP to expand further*\]

#### References
1. https://www.sciencedirect.com/science/article/pii/S146290111731273X
2. https://en.wikipedia.org/wiki/Fair_division_of_a_single_homogeneous_resource

### Security aspect
*Who would benefit from it ?*

- **EOS developers** getting relieved of the need to review the code themselves and get better insights into how to build secure applications.
- **Auditors** for getting a chance to contribute efforts on collaborative community audit request and receive financial compensation.
- **Users** for feeling much safer in investing funds or simply interacting with apps in the space.

*What are their requirements ?*
- **EOS developers** (*cost-effectiveness, support, value through skilled auditors*)
- **Auditors** (*worthy of time, non-toxic environnement, sense of community, scaling to skill level*)
- **Users** (*transparency, provable work, possibility of rewarding auditors maybe*)

*Liability, disclosure agreements ?*

\[*Need to dig further into this topic*\]

The DAOS will not assume any responsability for security incidents related to an audited project. Its role is only to report vulnerabilities to the team.

[Reasonable assurance vs. absolute assurance](https://security.stackexchange.com/questions/166236/are-security-auditors-liable-for-breaches)

*Issue of opening source code and open source doctrine in EOS ecosystem ?*

Projects would be required to have their source code open to the public. An added benefit is for auditors (and anyone really) to be able to match the audited code to the actual project code.

If the team does not wish to open source their code, they could always turn to other auditing solutions (like the one presented in [EOS players](#EOS-players)).

*Proving the validity of audits ?*

The report produced at the end of the audit process would serve as the validation and legitimacy of the audit. The scope and hashes of the contracts audited would be provided in the report along with all the findings details. A hash would also be provided to identify the specific audit. 

## Technical specifications
This section goes deeper into the technical aspect of running the DAO (platforms, backend, frontend, etc.).

### Github as a supporting platform
Since the DAO Security project is all about communication (as stated in the [overview](#overview)), a good case could be made for just using the storage, reporting and communication abilities of Github for running the whole operations of the DAO.

A repo containing the audited code would be created and auditors submissions would be processed as issues that could be discussed and resolved on the platform signifying the validity of the finding (and the award that goes with it). This system is what [Code4rena](#code4rena) uses for powering its own audit platform.

\[*More advantages/drawbacks*\]

### Pomelo integration
The goal would be to integrate this platform to the existing [Pomelo](https://pomelo.io/) initiative.

DAOS would be it's own web platform and it would be using Pomelo Bounties for the backend and smart contract capabilities.

The Pomelo platform would also provide funds for setting up the audit bounty. Additionnaly, teams who are requesting an audit could pay a certain fee for sending their request to the DAO.