# Staking Rewards

## Token Emission Schedule

* **Following the fundraising commitment**: The total number of tokens at the genesis block is 55 million TOMO tokens for circulation; 12 million additionally are reserved for the team vested over 4 years; and another 16 million are reserved for strategic partners and as part of an ecosystem building fund. The final 17 million are reserved as block rewards for 8 years. The amount of tokens in circulation at the end of the 8th year after the genesis block is 100 million TOMO. After the mainnet: the block reward for the first and second year is 4 million TOMO annually; the block reward for the 3rd, 4th, 5th year is 2 million TOMO annually; and the block reward for the 6th, 7th and 8th year is 1 million TOMO annually. Subsequently, the block reward will be halted, or activated at a number less than or equal to 1 million TOMO annually.
* **Implementation**: Each epoch consists of 900 blocks, which will reward a total of 250 TOMO in the first two years. 250 TOMO will be divided across all Masternodes proportional to the number of signatures they sign during the epoch. The reward achieved by each Masternode will be divided into three portions. The first portion of 40%, called the “Infrastructure Reward,” goes to the Masternode. The second portion of 50%, called the “Staking Reward,” goes to the pool of all voters for that Masternode shared proportionally based on the number of tokens staked out of the total number of tokens staked. The last portion of 10%, called the “Foundation Reward,” goes to a special account controlled by the Masternode Foundation, which is run by TomoChain Lab Pte Ltd. initially.
* **Reward frequency**:  Every epoch (\~30 minutes), Voters and Masternodes automatically receive rewards.

## Reward Calculation Formula and Details

Note that, for simplification of illustration:

* The total amount of staked TOMO for all Masternodes is equal
* The signatures for all Masternodes in the scenarios are equal

With these assumptions, all Masternodes receive the same divided reward (R) and the same infrastructure reward. Furthermore, the reward for Voters with 1,000 staked TOMO is equal regardless of which Masternode is voted for.

### Scenario 1: 50 Masternodes, 2.5 million token voting, a total of 5 million token locked.

**Reward per epoch:**

* MN infrastructure reward = 0.4 \* 5 = 2 TOMO
* For Voters with 1k staked = (0.5 \* 5 \* 1000) / 100k = 0.025 TOMO
* MN staking reward with 50k TOMO deposited = 50 \* 0.025 = 1.25 TOMO

**Reward per week:**

* MN infrastructure reward = 336 \* 2 = 672 TOMO
* For Voters with 1k staked = 336 \* 0.025 = 8.4 TOMO
* MN staking reward with 50k TOMO deposited = 336 \* 1.25 = 420 TOMO

**Reward per year:**

* MN infrastructure reward = 17,520 \* 2 = 35,040 TOMO
* For Voters with 1k staked = 17,520 \* 0.025 = 438 TOMO
* MN staking reward with 50k deposited = 17,520 \* 1.25 = 21,900 TOMO
* Total reward per MN with 50k deposited = 35,040 + 21,900 = 56,940 TOMO

### Scenario 2: 100 Masternodes, 3 million token voting, a total of 8 million token locked.

**Reward per epoch:**

* MN infrastructure reward = 0.4 \* 2.5 = 1 TOMO
* For Voter with 1k voted = (0.5 \* 2.5 \* 1000) / 80k = 0.015625
* MN staking reward with D = 50k deposited: 50 \* 0.015625 = 0.78125 TOMO

**Reward per week:**

* MN infrastructure reward = 336 \* 1 = 336 TOMO
* For Voter with 1k voted = 336 \* 0.015625 = 5.25 TOMO
* MN staking reward with D = 50k deposited: 336 \* 0.78125 = 262.5 TOMO

**Reward per year:**

* MN infrastructure reward = 17,520 \* 1 = 17,520 TOMO
* For Voter with 1k voted = 17,520 \* 0.015625 = 273.75 TOMO
* MN staking reward with D = 50k deposited: 17,520 \* 0.78125 = 13,687.5 TOMO
* Total reward per MN with D = 50k deposited: 17,520 + 13 687.5 = 31,208 TOMO

### Scenario 3: 150 Masternodes, 12.5 million token voting, a total of 20 million token locked.

**Reward per epoch:**

* MN infrastructure reward = 0.4 \* 1.6667 = 0.6667 TOMO
* For Voter with 1k voted = (0.5 \* 1.6667 \* 1000) / 133,333 = 0.00625 TOMO
* MN staking reward with 50k deposited: 50 \* 0.00625 = 0.3125 TOMO

**Reward per week:**

* MN infrastructure reward = 336 \* 0.6667 = 224 TOMO
* For Voter with 1k voted = 336 \* 0.00625 = 2.1 TOMO
* MN staking reward with D = 50k deposited: 336 \* 0.3125 = 105 TOMO

**Reward per year:**

* MN infrastructure reward = 17520 \* 0.6667 = 11,680 TOMO
* For Voter with 1k voted = 17520 \* 0.00625 = 109.5 TOMO
* MN staking reward with D = 50k deposited: 17,520 \* 0.3125 = 5,475 TOMO
* Total reward per MN with D = 50k deposited: 11,680 + 5,475 = 17,155 TOMO
