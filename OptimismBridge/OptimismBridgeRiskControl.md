# The Problem:

### Crypto Bridge Hacks & malfunctions are quite often. In the last year billions of dollars have been lost by bridges in hacks. Here is a list of past bridge hacks for reference:


- [BNB BRIDGE - REKT](https://rekt.news/bnb-bridge-rekt/)

- [RONIN NETWORK - REKT](https://rekt.news/ronin-rekt/)

- [NOMAD BRIDGE - REKT](https://rekt.news/nomad-rekt/)


As a user of bridge, you want to ensure that if a bridge is malfunctioning, you become aware of the hack/malfunction as soon as possible so you can pull out your assets from the Bridge. In order to achieve this goal, you need to continuously monitor the on-chain data related to the Bridge:

#### For this question, we will take the Optimism bridge as an example. Let’s say you wanted to monitor the Optimism bridge functioning using chain data so you can identify a hack as soon as possible.

1. Write a short write-up describing how you would identify in real-time whether the Optimism bridge is working effectively or not.
2. What all on-chain data would you listen for? Please feel free to read through any docs or research online.
3. Write a script (in the language of your choice) to implement your approach and output True if the Optimism bridge is working effectively and False if it is not Working. Feel free to use Etherscan free A.P.I.s for accessing on-chain data.

# The Answers:

#### Patterns Detected in the BlockChain Bridges Exploits Examples provided:
- 2 out of 3 of these are Centralized "BlockChains", having B.S.C. only 21 Validators and Ronin Network just 9.
I would suggest avoiding these Centralized "BlockChains" at all costs in the 1st Place; similarly, the Solana "BlockChain"
had a lot of F.O.M.O. surrounding it besides being Centralized, but finally it also [got Hacked due to its Centralization](https://cointelegraph.com/news/ongoing-solana-based-wallet-hack-has-already-seen-millions-drained).
- The 3rd study case, Nomad Bridge, was Hacked due to an UnSupervised Vulnerable Smart Contracts Upgrade. It was [Audited by Quanstamp](https://certificate.quantstamp.com/full/nomad), but the Audit was not taken Seriously by the Development Team.


- Also, here is an [Example of Optimism Bridge being Hacked](https://cointelegraph.com/news/optimism-loses-20m-tokens-after-l1-and-l2-confusion-exploited).

### 1. Identify if the Optimism Bridge is working effectively in Real-Time or not:
A_Problems and its Consequences:                                                                                                         
- UnAuthorized User Mints Tokens (likely without Backing) in One or Several Sides of the Bridge, that aside of the
Security Breach also can cause Extreme Inflation and Devaluation of that Token.                                                                
- Normal Users get Affected by this if the BlockChain Owners decide to Pause/Turn Off the BlockChain for any amount of Time.                   
- Normal Users not being able to Withdraw their Funds from 1 Side of the Bridge because the other Side Backing Tokens were stolen.             

B_Factors to Detect:
- Doing the Most Convenient Approach as Possible, Optimism counts with a [Status Dashboard](https://status.optimism.io) that tells you in Real-Time if All the Systems are Operational; and a Traditional Web 2.0 Back-End Developer can set up a Script to Listen these Events by
using [WebHooks](https://instatus.com/help/webhooks).                                                                                          
- Regarding On-Chain Data, I would Pay Attention in real-time to the Amount of Tokens Minted/Sent by the Bridge in the Last 7 Days(168 hours): 


1- Taking into account a Reference Transaction Amount which is the highest of that Past Week, I would Monitor every New Incoming
Transaction and Trigger an Alert if the Minted/Sent Amount of this Bridge Transaction is a specific % higher than the Latest
 Weekly Highest Amount Transaction.                                                                                                            
2- That % could be from a Minimum of 50%, a 100% or a 200% more than the Weekly Highest Amount Transaction, depending of the Level
of Precaution that you want to take.                                                                                                           
3- If the New Transaction Amount % is < than the (Weekly Highest Amount Transaction += Higher Determined %), then the Weekly Highest Amount
Value gets Updated.

### 2. OnChain Data Sources to Monitor:                                                                                                        
- [Optimism L2StandardBridge Smart Contract](https://optimistic.etherscan.io/address/0x4200000000000000000000000000000000000010#events) [WithdrawalInitiated Event](), more Specifically its `uint256 _amount` Parameter.                                                              
- [Optimism L2StandardBridge Smart Contract](https://optimistic.etherscan.io/address/0x4200000000000000000000000000000000000010#code) [`withdrawTo` Function](https://optimistic.etherscan.io/address/0x4200000000000000000000000000000000000010#code#F43#L66).                      



### 3. Script:

Doing the Most Convenient Approach as Possible, Optimism counts with a [Status Dashboard](https://status.optimism.io) that tells you in Real-Time if All the Systems are Operational; and a Traditional Web 2.0 Back-End Developer can set up a Script to Listen these Events by
using [WebHooks](https://instatus.com/help/webhooks).

#### Useful Tools that I Researched to facilitate the Job of a Web 2.0 Back-End Developer doing that:

https://public-grafana.optimism.io/alerting/list?dataSource=grafanacloud-optimistic-prom                                                       
https://dune.com/Marcov/Optimism-Ethereum                                                                                                      
https://app.ante.finance/protocol/Optimism%20Bridge                                                                                            
https://www.alchemy.com/notify                                                                                                                 
https://forta.org/developers/                                                                                                                  
