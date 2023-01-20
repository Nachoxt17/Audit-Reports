## EthSwarm storage-incentives #01.


### Storage Incentives Smart Contracts Security Audit Report:

| Detail  | Information |
| ------------- | ------------- |
| :man_technologist:Author  | [Ignacio Ceaglio](https://www.linkedin.com/in/ignacioceaglio/)  |
| :watch:Delivery Date  | 2023-01-16  |
| :notebook:Programming Languages  | Solidity  |
| :test_tube:Methods  | Architecture Review, Unit Testing, Functional Testing, Manual Review.  |
| :page_with_curl:Documentation Quality  | High: The Quality of the Documentation could be improved to *Excellent* by correcting its Typos and adding some Emojis, Images and/or Diagrams to make it mor Eye Catching and Attractive (and thus, easier to read) to Non-Technical Users and Potential Investors. The Documentation in the Smart Contracts is very Detailed and Complete. |


### Source Code Audit Reach:

| Repository  | Commit |
| ------------- | ------------- |
| [ethersphere/storage-incentives](https://github.com/ethersphere/storage-incentives)  | [`04be7ba`](https://github.com/ethersphere/storage-incentives/tree/04be7ba384d77e60b2dc99e7c679bf98d529f052)  |


### Findings Severity Levels Classification:

| Risk Level:pirate_flag:  | Description:page_facing_up: |
| ------------- | ------------- |
| :closed_book:Critical Risk  | <ul><li>Any governance voting result manipulation.</li><li>Direct theft of any user funds, whether at-rest or in-motion, other than unclaimed yield.</li><li>Direct theft of any user N.F.T.s, whether at-rest or in-motion, other than unclaimed royalties.</li><li>Permanent freezing of funds.</li><li>Permanent freezing of N.F.T.s.</li><li>Miner-extractable value (M.E.V.).</li><li>Unauthorized minting of N.F.T.s.</li><li>Predictable or manipulable Random Number Generator that results in abuse of the principal or N.F.T..</li><li>Unintended alteration of what the N.F.T. represents (e.g. token URI, payload, artistic content).</li><li>Protocol insolvency.</li></ul>  |
| :orange_book:High Risk  | <ul><li>Theft of unclaimed yield.</li><li>Theft of unclaimed royalties.</li><li>Permanent freezing of unclaimed yield.</li><li>Permanent freezing of unclaimed royalties.</li><li>Temporary freezing of funds.</li><li>Temporary freezing NFTs.</li></ul>  |
| :ledger:Medium Risk  | <ul><li>Smart Contract unable to operate due to lack of token funds.</li><li>Block stuffing for profit.</li><li>Griefing (e.g. no profit motive for an attacker, but damage to the users or the protocol).</li><li>Theft of gas.</li><li>Unbounded gas consumption.</li></ul>  |
| :blue_book:Low Risk  | <ul><li>Smart Contract fails to deliver promised returns, but doesn't lose value.</li></ul>  |
| :green_book:Informational Risk  | <ul><li>Code Development Best Practices.</li></ul>  |
| :grey_question:Unknown Risk  | <ul><li>The impact of the issue is uncertain.</li></ul>  |


### Total Issues Found: 2

| Risk Level:pirate_flag:  | # of Issues Found:1234: |
| ------------- | ------------- |
| :closed_book:Critical Risk Issues  | 0  |
| :orange_book:High Risk Issues  | 0  |
| :ledger:Medium Risk Issues  | 0  |
| :blue_book:Low Risk Issues  | 0  |
| :green_book:Informational Issues  | 1  |
| :grey_question:Unknown Risk Issues  | 1  |

### Findings:

| Finding I.D.:id:  | Description:page_facing_up: | Severity:warning: | Status:repeat: |
| ------------- | ------------- | ------------- | ------------- |
| DOC-01  |  Typos in Documentation  | :green_book:Informational  | Acknowledged:triangular_flag_on_post:  |
| CENTRAL-01  |  Centralization of Privileged Roles and Ownership  | :grey_question:Unknown Risk  | Acknowledged:triangular_flag_on_post:  |


#### :one: DOC-01 | Typos in the Documentation:

#### :page_facing_up:Description:

There are typos in the `README.md` Documentation:

`./README.md`:
```html
<!--Line #7:-->
...resposibility...

<!--Line #11:-->
...particpate...

<!--Line #76:-->
...blockchcain...
```

There are No Technical Risk involved.

#### :hammer_and_wrench:Solution:

- Just correct the Typos. Using the cSpell Visual Studio Code Extension is recommended.

#### :two: CENTRAL-01 | Centralization of Privileged Roles and Ownership:

#### :page_facing_up:Description:

In all the Smart Contracts the Power is assigned to an unique and only Wallet Address:

`./src/PostageStamp.sol`:
```solidity
//- Line #108:
    constructor(address _bzzToken, uint8 _minimumBucketDepth) {
        //...
        _setupRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _setupRole(PAUSER_ROLE, msg.sender);
    }
```

`./src/PriceOracle.sol`:
```solidity
//- Line #38:
    constructor(address _postageStamp) {
        _setupRole(DEFAULT_ADMIN_ROLE, msg.sender);
        //...
    }
```

`./src/Staking.sol`:
```solidity
//- Line #63:
    constructor(address _bzzToken, uint64 _NetworkId) {
        //...
        _setupRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _setupRole(PAUSER_ROLE, msg.sender);
    }
```

`./src/Redistribution.sol`:
```solidity
//- Line #122:
    constructor(
        address staking,
        address postageContract,
        address oracleContract
    ) {
        //...
        _setupRole(DEFAULT_ADMIN_ROLE, msg.sender);
        _setupRole(PAUSER_ROLE, msg.sender);
    }
```

This is a Risk because in the case that the Private Keys or Seed of the Owner Wallet gets compromised, the whole Protocol would now be under Unanimous Control of the Attacker.

#### :hammer_and_wrench:Solution:

- Short Term: Using a Multiple Signature Wallet for the Owner Role is recommended.

- Long Term: Introduce in the Smart Contracts several 1st and 2nd Level Authority Roles to Balance the Power and Tasks between each other.

## SECURITY SUMMARY:

#### This Project is very Safe and Nearly Impossible to Manipulate by Design, because:
- It does not Interacts with any External Protocol (UnSafe `External Oracles`, `De.Fi. Exchanges`, etc) whose Data could be Manipulated
in order to modify the Logic at a local level.
- It lacks of any kind of `fallback function` or Local Balance Check that could react to a Malicious User sending Ether or ERC-20 Tokens with the Purpose of manipulating some specific Outcome on its favor.
- It lacks of any kind of D.A.O. Governance System that an User could Manipulate with the use of `FlashLoans` in order to gain the Power over the Protocol Decisions and its Funds.
- Generally speaking, there are very little opportunities for the Users to Input Data by themselves; most of the Information Processing and Generation is done internally. A good example of this is seen at `./src/PriceOracle.sol` where almost all of the Information Generation is done internally, and the only argument `block.number` that is fed externally is used in a harmless way.



### :clock6:ChangeLog:

- 2023-01-16 - Delivered Initial Report


## DISCLAIMER

This report is based on the scope of materials and documentation provided for a limited review at the time provided. Results may not be complete nor inclusive of all
vulnerabilities. The review and this report are provided on an as-is, where-is, and as-available basis. You agree that your access and/or use, including but not
limited to any associated services, products, protocols, platforms, content, and materials, will be at your sole risk. Blockchain technology remains under development 
and is subject to unknown risks and flaws. The review does not extend to the compiler layer, or any other areas beyond the programming language, or other programming 
aspects that could present security risks. A report does not indicate the endorsement of any particular project or team, nor guarantee its security. No third party 
should rely on the reports in any way, including for the purpose of making any decisions to buy or sell a product, service or any other asset. To the fullest extent 
permitted by law, we disclaim all warranties, expressed or implied, in connection with this report, its content, and the related services and products and your use 
thereof, including, without limitation, the implied warranties of merchantability, fitness for a particular purpose, and non-infringement. We do not warrant, endorse, 
guarantee, or assume responsibility for any product or service advertised or offered by a third party through the product, any open source or third-party software, 
code, libraries, materials, or information linked to, called by, referenced by or accessible through the report, its content, and the related services and products, 
any hyperlinked websites, any websites or mobile applications appearing on any advertising, and we will not be a party to or in any way be responsible for monitoring 
any transaction between you and any third-party providers of products or services. As with the purchase or use of a product or service through any medium or in any 
environment, you should use your best judgment and exercise caution where appropriate. FOR AVOIDANCE OF DOUBT, THE REPORT, ITS CONTENT, ACCESS, AND/OR USAGE THEREOF, 
INCLUDING ANY ASSOCIATED SERVICES OR MATERIALS, SHALL NOT BE CONSIDERED OR RELIED UPON AS ANY FORM OF FINANCIAL, INVESTMENT, TAX, LEGAL, REGULATORY, OR OTHER ADVICE.