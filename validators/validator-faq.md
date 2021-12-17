# Validator FAQ

### General Concepts <a href="#general-concepts" id="general-concepts"></a>

#### What is a Validator? <a href="#what-is-a-validator" id="what-is-a-validator"></a>

A Validator is someone who operates a full node and validates transactions to secure the BitSong blockchain in return for rewards. Validators operate a full node on the BitSong network and participate in consensus by voting on the validity of blocks. Validators also participate in governance by voting on proposals.&#x20;

#### What is Staking? <a href="#what-is-staking" id="what-is-staking"></a>

Staking is the act of depositing cryptocurrencies to help secure the BitSong blockchain, either as a Validator or Delegator. Delegators stake their BTSG tokens to a Validator for a share of the Validator rewards. Validators stake BTSG tokens, which may include their own tokens and staked tokens from Delegators, to be able to participate in the BitSong network as a Validator and earn rewards.&#x20;

Users may declare their intention to become a validator by sending a `create-validator` transaction. From there, they become validator candidates.

The total amount of staked tokens determines the weight of the Validator's voting power and the probability that they are selected to produce a block.&#x20;

Currently, only the top 64 Validators by staked BTSG will be able to participate in consensus.&#x20;

#### What is a full node? <a href="#what-is-a-full-node" id="what-is-a-full-node"></a>

Full nodes on the BitSong network are running the current version of the BitSong software to be able to validate transactions and blocks.&#x20;

Operating a full node simply means running a non-compromised and up-to-date version of the software with low network latency and with no downtime.&#x20;

BitSong welcomes any users who want to run a full node, even if they do not plan to become a Validator.&#x20;

#### What is a Delegator? <a href="#what-is-a-delegator" id="what-is-a-delegator"></a>

A Delegator is someone who delegates their BTSG tokens to a Validator to help secure the BitSong blockchain in return for a share of rewards. Unlike becoming a Validator, which has prerequisites in terms of hardware and connectivity, anyone who holds BTSG can become a Delegator.&#x20;

However, delegating does require participation from Delegators, who should actively monitor their stake and the performance of their chosen Validator(s). Delegators should also participate in governance votes, to ensure their wishes are reflected in the future development of the BitSong ecosystem.&#x20;

Delegators also bear some risk. If their chosen Validator(s) engage in behavior that goes against the interests of the network, the Validators stake may be slashed. Therefore, Delegators are advised to do their own research before staking BTSG to a Validator, and manage risk, for example, by staking to multiple Validators.&#x20;

For more information, go to the [Delegators section](../delegators/).&#x20;

### Becoming a Validator <a href="#becoming-a-validator" id="becoming-a-validator"></a>

#### How to become a validator? <a href="#how-to-become-a-validator" id="how-to-become-a-validator"></a>

If someone wishes to become a Validator, then they need to send a `create-validator` transaction. They will be asked to complete the following:

* **Validator's `PubKey`:** The private key associated with this Tendermint `PubKey` is used to sign _prevotes_ and _precommits_.
* **Validator's Address:** Application level address. This is the address used to identify your Validator publicly. The private key associated with this address is used to delegate, unbond, claim rewards, and participate in governance.
* **Validator's name (moniker)**
* **Validator's website (Optional)**
* **Validator's description (Optional)**
* **Initial commission rate**: The commission rate on block rewards and fees charged to delegators.
* **Maximum commission:** The maximum commission rate which this validator can charge. This parameter cannot be changed after `create-validator` is processed.
* **Commission max change rate:** The maximum daily increase of the validator commission. This parameter cannot be changed after `create-validator` is processed.
* **Minimum self-delegation:** Minimum amount of BTSG the validator needs to have bonded at all time. If the validator's self-delegated stake falls below this limit, their entire staking pool will unbond.

Once a Validator is created, BTSG holders can begin delegating to them immediately. The Validators total stake is the amount of their own bonded BTSG plus the amount of BTSG staked to them by Delegators.&#x20;

The 64 Validator candidates with the largest total stake will be selected as Validators on the BitSong network. If a Validator's total stake falls below the threshold set by the top 64 candidates, they will cease to become a Validator until their stake becomes enough to qualify for the top 64 Validator candidates again.&#x20;

Validator candidates who fail to reach the top 64 and become a Validator will no longer qualify for Validator privileges and will lose the right to earn Validator rewards.&#x20;

The total number of Validator slots available on the BitSong network may change periodically according to a governance vote.&#x20;

### Testnet <a href="#testnet" id="testnet"></a>

#### How can I join the testnet? <a href="#how-can-i-join-the-testnet" id="how-can-i-join-the-testnet"></a>

We recommend that you test your Validator setup on the Testnet before launching on the BitSong mainnet. Testnet participation also signals to the community that you're ready to become a member of the Validator network.&#x20;

You can find all relevant information about the testnet [here](https://hub.cosmos.network/main/gaia-tutorials/join-testnet.html) and [here (opens new window)](https://github.com/cosmos/testnets).

#### What are the different types of keys? <a href="#what-are-the-different-types-of-keys" id="what-are-the-different-types-of-keys"></a>

There are two types of keys:

* **Tendermint Key**: This is a unique key used to sign consensus votes.
  * It is associated with a public key `cosmosvalconspub` (Get this value with `gaiad tendermint show-validator`)
  * It is generated when the node is created with gaiad init.
* **Application key**: This key is created from `gaiad` and used to sign transactions. Application keys are associated with a public key prefixed by `cosmospub` and an address prefixed by `cosmos`. Both are derived from account keys generated by `gaiad keys add`.

Note: A validator's operator key is directly tied to an application key, but uses reserved prefixes solely for this purpose: `cosmosvaloper` and `cosmosvaloperpub`

#### What are the different states a validator can be in? <a href="#what-are-the-different-states-a-validator-can-be-in" id="what-are-the-different-states-a-validator-can-be-in"></a>

Once you create your Validator with the `create-validator` transaction, it can be in one of three states:

* `in validator set`: Validator is included in the active set of 64 and is participating in consensus. Validator is earning rewards and may be slashed if they misbehave.
* `jailed`: Validator misbehaved and is in jail. The Validator is no longer participating in the active set of 64 or earning rewards. If the jailing happened because the Validator was offline too long, they can send an `unjail` transaction to re-enter the Validator set. If they were jailed due to a double signing, the Validator cannot unjail.
* `unbonded`: Validator is not in the active set, so doesn't participate in consensus, sign blocks, or earn rewards. The Validator also cannot be slashed. Delegators can still delegate BTSG to unbonded Validators, but if they unbond, their BTSG are released immediately without any unbonding period.&#x20;

#### What is 'self-delegation'? How can I increase my 'self-delegation'? <a href="#what-is-self-delegation-how-can-i-increase-my-self-delegation" id="what-is-self-delegation-how-can-i-increase-my-self-delegation"></a>

Self-delegation is the amount of BTSG bonded from a Validators own wallet to themselves. Validators can increase this amount by sending a `delegate` transaction from your validator's `application` key.

#### Is there a minimum amount of BTSG that must be delegated to be an active (=bonded) validator? <a href="#is-there-a-minimum-amount-of-atoms-that-must-be-delegated-to-be-an-active-bonded-validator" id="is-there-a-minimum-amount-of-atoms-that-must-be-delegated-to-be-an-active-bonded-validator"></a>

The minimum is `1 btsg`.

#### How do delegators choose their validators? <a href="#how-will-delegators-choose-their-validators" id="how-will-delegators-choose-their-validators"></a>

Delegators can choose any Validator according to their own criteria. However, some important factors to consider are:

* **Amount of self-delegated BTSG:** Validators with a larger amount of self-delegated BTSG have more "skin in the game." If they misbehave and get slashed, their own funds are just as much at stake as their Delegators'.&#x20;
* **Amount of delegated BTSG:** The total amount of delegated BTSG indicates the amount of voting power and influence the Validator has in the community. A Validator with a large amount of delegated BTSG is more likely to get chosen to produce more blocks and earn more rewards, but those rewards will be shared with more other Delegators. Bigger validators also decrease the decentralisation of the network by concentrating voting power.
* **Commission rate:** The higher the commission rate, the more the Validator earns, but the lower the rewards paid to Delegators.&#x20;
* **Track record:** The track record shows data about the past performance of the Validator, allowing a Delegators to view seniority, past votes on proposals, historical average uptime and how often the node was compromised.

Validators may also take measures of their own to establish their reputation and credentials among the Delegator community. For instance, many Validators run their own websites and stake on other networks. Some have their setups audited by third parties. Delegators should conduct their own research on Validators before staking their funds.&#x20;

To read more about how to conduct due diligence as a staker, see [this blog post (opens new window)](https://medium.com/@interchain\_io/3d0faf10ce6f)

### Responsibilities <a href="#responsibilities" id="responsibilities"></a>

#### Do Validators need to be publicly identified? <a href="#do-validators-need-to-be-publicly-identified" id="do-validators-need-to-be-publicly-identified"></a>

There's no requirement to identify any individual or entity operating as a Validator. Delegators are required to evaluate Validators based on their individual merits. Validators can link their Validator setup to a website, where they can choose which information they share with the public. &#x20;

#### What are the responsibilities of a Validator? <a href="#what-are-the-responsibilities-of-a-validator" id="what-are-the-responsibilities-of-a-validator"></a>

Validators have two main responsibilities:

* **Actively participate in consensus:** Validators must run the correct version of the BitSong software, ensure that servers and equipment are always online, and that Validator private keys remain secure
* **Actively participate in governance:** Validators must vote on governance proposals.

However, Validators are also part of a community and as such, participation is key. Joining the relevant groups and social channels, and participating in discussions ensures that Validators are always up-to-date with events and the current state of the ecosystem.&#x20;

#### What does 'participate in governance' involve? <a href="#what-does-participate-in-governance-entail" id="what-does-participate-in-governance-entail"></a>

BTSG holders can propose and vote on proposals regarding the development and running of the BitSong ecosystem. Examples of decisions may be to change the number of Validators in the active set or to pass a particular upgrade.&#x20;

While any BTSG holders can participate in governance, Validators play a particularly valuable role in governance and must vote on all proposals. Not only is it likely that all proposals will affect them to some degree, but more importantly, they also represent the vote of their absent Delegators.&#x20;

#### What does staking imply? <a href="#what-does-staking-imply" id="what-does-staking-imply"></a>

Staking BTSG is comparable to placing a safety deposit on validation and the overall security of the BitSong network. Anyone can choose to stake or unstake as much of their BTSG as they wish. When a Validator or Delegator wants to unstake their BTSG, they send an`unbonding` transaction.&#x20;

Then, the staked BTSG undergo a **3-week unbonding period.** During the unbonding period, the staked BTSG may be subject to slashing, if the misbehavior that prompted the slashing took place before the Delegator initiated the unbonding transaction.

Validators and Delegators are eligible to receive block rewards and a share of transaction fees, and have the right to vote on governance matters. However, if a Validator misbehaves, then their total stake is subject to slashing. As such, all the Delegators who staked BTSG to the slashed Validator will also have a proportionate share of their stake slashed.&#x20;

Therefore, it's important that Delegators only stake their BTSG to Validators who they trust to behave in a way that won't result in their funds being slashed.&#x20;

#### Does a Validator have access to the Delegator's BTSG? <a href="#can-a-validator-run-away-with-their-delegators-atoms" id="can-a-validator-run-away-with-their-delegators-atoms"></a>

When a Delegator stakes their BTSG to a Validator, they're delegating their voting power to the Validator. So Validators with the most staked BTSG will have the most influence over governance decisions.&#x20;

However, the Validator never has access to the BTSG staked to them and cannot take custody of any staked funds. To be clear, there is no way that a Validator can steal delegated funds.&#x20;

Nevertheless, Delegators may still lose funds through slashing if their Validator misbehaves.&#x20;

#### How often will a validator be chosen to propose the next block? Does it go up with the amount of bonded BTSG? <a href="#how-often-will-a-validator-be-chosen-to-propose-the-next-block-does-it-go-up-with-the-quantity-of-bo" id="how-often-will-a-validator-be-chosen-to-propose-the-next-block-does-it-go-up-with-the-quantity-of-bo"></a>

The Validator chosen to propose the next block is called the proposer. Proposers are selected deterministically, and the proportional amount of bonded BTSG determines the frequency of being selected as the proposer. So if a validator holds 10% of the total bonded BTSG across all validators, they will be selected as the block proposer 10% of the time.&#x20;

#### ~~Will validators of the Cosmos Hub ever be required to validate other zones in the Cosmos ecosystem?~~ <a href="#will-validators-of-the-cosmos-hub-ever-be-required-to-validate-other-zones-in-the-cosmos-ecosystem" id="will-validators-of-the-cosmos-hub-ever-be-required-to-validate-other-zones-in-the-cosmos-ecosystem"></a>

~~Yes, they will. If governance decides so, validators of the Cosmos hub may be required to validate additional zones in the Cosmos ecosystem.~~

### Incentives <a href="#incentives" id="incentives"></a>

#### What is the incentive to stake? <a href="#what-is-the-incentive-to-stake" id="what-is-the-incentive-to-stake"></a>

Incentives are made up of two different revenue streams:

* **Block rewards:** Each block, new BTSG are minted according to the inflation algorithm and paid as staking rewards
* **Transaction fees:** Fees to transact on the BitSong network are paid in BTSG and used as staking rewards.&#x20;

The total revenue from each stream is distributed among Validators' staking pools according to the weight of their pool. Within each pool, the revenue is distributed again to each Delegator according to their individual stake.&#x20;

Validators also apply their commission to Delegators' revenue before it is allocated.

#### What is the incentive to run a Validator ? <a href="#what-is-the-incentive-to-run-a-validator" id="what-is-the-incentive-to-run-a-validator"></a>

Validators are incentivized through revenues and responsibility. Validators earn commission, which means they earn proportionately more revenue than Delegators to reflect their additional responsibilities and overheads. &#x20;

Validators have significant responsibilities within governance because if one of their Delegators doesn't vote, the Validator inherits their vote. Therefore, Validators can hold substantial voting power depending on the size of their delegation.

#### What is the Validator's commission? <a href="#what-are-validators-commission" id="what-are-validators-commission"></a>

Before revenues are allocated to Delegators, the Validator can apply a commission to it, expressed as a percentage. Validators can choose their commission rates and change them if they wish; however, they're competing in a market for Delegators to stake their BTSG. Therefore, the appropriate commission rate is defined by the market.&#x20;

#### How are block rewards distributed? <a href="#how-are-block-rewards-distributed" id="how-are-block-rewards-distributed"></a>

Let's illustrate block reward distribution using a simplified example. We can assume we have 10 Validators with equal voting power and a commission rate of 1% each. We can also assume that the block reward is 1000 BTSG and each Validator's pool comprises 20% self-bonded BTSG.&#x20;

Reward tokens do not go directly to the proposer. Instead, they are evenly spread among validators at each block. Based on the last block produced which generated 1000 BTSG rewards, each of the ten Validator pools has a reward allocation of 100 BTSG. These 100 BTSG will be distributed according to each participant's stake:

* Commission: `100*80%*1% = 0.8 btsg`
* Validator gets: `100\*20% + Commission = 20.8 btsg`
* All delegators get: `100\*80% - Commission = 79.2 btsg`

Then, each Delegator can claim their part of the 79.2 BTSG in proportion to their stake in the validator's staking pool.

#### How are fees distributed? <a href="#how-are-fees-distributed" id="how-are-fees-distributed"></a>

Fees are similarly distributed according to the weighted model. However, there is one exception – the block proposer can earn a bonus on the fees of the block they propose, only if they include more than the strict minimum of required precommits.

A Validator proposing the next block must include at least two-thirds of the precommits of the previous block. However, Validators can earn a bonus if they include more than two-thirds of the precommits.

The amount of the bonus ranges from 1% if the proposer includes the required minimum two-thirds precommits, which is also necessary for the block to be deemed valid. The proposer can earn up to 5% if they include 100% of the precommits.

The proposer should not delay too long though, or they risk the scenario that other validators may timeout and move on to the next proposer. So, validators must strike a balance between the time it takes to gather the most signatures and the increasing risk of losing out on any bonus at all by being the proposer of the next block.&#x20;

Let's take another concrete example where we have 10 validators with equal stake. Each of them applies a 1% commission rate and has 20% of self-delegated BTSG. The next block is ready and it's about to generate 1025.51020408 BTSG in fees.

First, the 2% [Community Pool](../features-and-modules/community-pool.md) levy is applied. The Community Pool exists to fund community proposals, which must go through governance.&#x20;

* `2% * 1025.51020408 = 20.51020408` BTSG go to the Community.

1005 BTSG now remain. Let's assume that the proposer included 100% of the signatures in its block so it could earn the maximum bonus of 5%.

We must now solve this equation to find the reward R for each validator:

`9*R + R + R*5% = 1005 ⇔ R = 1005/10.05 = 100`

* For the proposer validator:
  * The pool obtains `R + R * 5%`: 105 BTSG
  * Commission: `105 * 80% * 1%` = 0.84 BTSG
  * Validator's reward: `105 * 20% + Commission` = 21.84 BTSG
  * Delegators' rewards: `105 * 80% - Commission` = 83.16 BTSG (each Delegator will be able to claim their portion of these rewards in proportion to their stake)
* For each non-proposer validator:
  * The pool obtains R: 100 BTSG
  * Commission: `100 * 80% * 1%` = 0.8 BTSG
  * Validator's reward: `100 * 20% + Commission` = 20.8 BTSG
  * Delegators' rewards: `100 * 80% - Commission` = 79.2 BTSG (each Delegator will be able to claim their portion of these rewards in proportion to their stake)

#### What are the slashing conditions? <a href="#what-are-the-slashing-conditions" id="what-are-the-slashing-conditions"></a>

Slashing results from misbehavior on the part of a Validator. There are currently two actions classed as misbehavior:&#x20;

* **Double signing:** If a Validator is found by someone on chain A to have signed two blocks at the same height on chain A and chain B, and if chain A and chain B share a common ancestor, then the Validator will have their stake slashed by 5% on chain A.
* **Downtime:** If a Validator is down for more than 95% of the last 10.000 blocks, they will have their stake slashed by 0.01%.

#### Do Validators need to self-delegate BTSG? <a href="#do-validators-need-to-self-delegate-atoms" id="do-validators-need-to-self-delegate-atoms"></a>

Yes, there is a requirement for Validators to self-delegate at least `1 btsg`. Validators are not obliged to self-delegate more, but they should be able to demonstrate that they have skin in the game to Delegators.&#x20;

Validators can also signal a commitment to maintaining their self-delegated BTSG by setting a minimum amount for the self-delegation. Should the self-delegated BTSG fall below the minimum, the Validator and all of its Delegators will unbond automatically.&#x20;

#### How to prevent the concentration of stake to a few top validators? <a href="#how-to-prevent-concentration-of-stake-in-the-hands-of-a-few-top-validators" id="how-to-prevent-concentration-of-stake-in-the-hands-of-a-few-top-validators"></a>

Blockchain communities usually naturally migrate to a position that preserves decentralization, as a means of self-preservation. However, there are a few other ways to help promote this position:&#x20;

* **Penalty-free re-delegation:** Delegators can easily switch their stake from one Validator to another&#x20;
* **UI warning:** Wallets can display warnings to users if they try to delegate to a Validator that already has a substantial amount of staking power.

### Technical Requirements <a href="#technical-requirements" id="technical-requirements"></a>

#### What are the hardware requirements? <a href="#what-are-hardware-requirements" id="what-are-hardware-requirements"></a>

Validators can anticipate needing one or more data center locations equipped with redundant power, networking, firewalls, HSMs, and servers.

While hardware requirements may be relatively modest at first, they may rise as network usage increases. Prospective Validators are strongly encouraged to participate in the testnet as a means of establishing the current requirements.&#x20;

#### What are software requirements? <a href="#what-are-software-requirements" id="what-are-software-requirements"></a>

In addition to running a BitSong full node, Validators should also utilize monitoring, alerting, and management solutions for their setup.

#### What are bandwidth requirements? <a href="#what-are-bandwidth-requirements" id="what-are-bandwidth-requirements"></a>

Compared to chains like Ethereum or Bitcoin, BitSong has the capacity for very high throughput.

We recommend that data center nodes only connect to trusted full nodes in the cloud or other validators that know one other socially. This relieves the data center node from needing to mitigate denial-of-service attacks which will consume bandwidth.

Ultimately, as BitSong becomes more established and acquires more users, multigigabyte per day bandwidth is plausible.

#### What are the logistical requirements of becoming a Validator? <a href="#what-does-running-a-validator-imply-in-terms-of-logistics" id="what-does-running-a-validator-imply-in-terms-of-logistics"></a>

Successful Validators are usually run by multiple highly skilled individuals who share the responsibility for providing continuous attention to the operation. It takes considerably more effort, resources, and skill than running a mining ASIC, for example.&#x20;

#### How to handle key management? <a href="#how-to-handle-key-management" id="how-to-handle-key-management"></a>

Validators will need to run a hardware security module (HSM) that supports ed25519 keys. Here are some of the potential options:

* YubiHSM 2
* Ledger Nano S
* Ledger BOLOS SGX enclave
* Thales nShield support

BitSong does not recommend one solution over another.&#x20;

#### What can validators expect in terms of operations? <a href="#what-can-validators-expect-in-terms-of-operations" id="what-can-validators-expect-in-terms-of-operations"></a>

Validators who run their operation like a tight ship will avoid unexpected unbonding or being slashed. Validators must be available to respond to attacks or outages and to be able to maintain security and isolation in the data center.&#x20;

#### What are the maintenance requirements? <a href="#what-are-the-maintenance-requirements" id="what-are-the-maintenance-requirements"></a>

Validators are required to perform regular software updates to accommodate upgrades and bug fixes. When new modules or functionality are introduced to BitSong, there may be issues that require vigilance on the part of the Validator community.&#x20;

#### How can validators protect themselves from denial-of-service attacks? <a href="#how-can-validators-protect-themselves-from-denial-of-service-attacks" id="how-can-validators-protect-themselves-from-denial-of-service-attacks"></a>

Denial-of-service attacks or DoS attacks refer to the scenario where an attacker sends a flurry of internet traffic to an IP address. In doing so, they prevent the server at the IP address from being able to connect to the internet.

In the blockchain scenario, the attacker scans the network in an attempt to discover the IP addresses of validator nodes. It then tries to disconnect them from communication by flooding them with traffic.

Validators can mitigate these risks by carefully structuring their network topology in a so-called sentry node architecture.

Validator nodes should only connect to full nodes they trust - either because they operate the nodes themselves or because the nodes are run by other validators they know socially.&#x20;

A validator node typically runs in a data center, most of which are linked directly to the networks of major cloud providers. The validator can use those links to connect to sentry nodes, which run in the cloud.&#x20;

This setup shifts the responsibility of denial-of-service from the validator's node directly to its sentry nodes. It may require new sentry nodes be set up to mitigate attacks on existing ones.

It's possible to spin up sentry nodes or change their IP addresses relatively quickly. Because the links to the sentry nodes exist in private IP space, an internet-based DoS attack does not affect them directly. Thus, this setup will ensure that validator block proposals and votes are always transmissible to the rest of the network.

For more on sentry node architecture, see [this (opens new window)](https://forum.cosmos.network/t/sentry-node-architecture-overview/454).
