---Validation process and some additional resources.---
https://docs.near.org/docs/roles/validator/hardware

----------Validator Requirements------------
1. Min Hardware Requirements
CPU: 2-Core, RAM: 8GB DDR4, Storage: 100GB SSD (Note: HDD will not work), Linux 18.04 or 20.04
2. Choose VPS and price)
GCP,AWS,Azure, Vultr, Hetzner, Oracle

-----------Soliving some problems and useful informataion -----------
3. This document will address the most common issues you may have while running Stake Wars and setting up your node.
https://github.com/nearprotocol/stakewars/blob/master/troubleshooting.md
4. Check current seat price - proposals, next epoch and current
near proposals -- shows new staking tx proposals and rollover validators
near validators next -- shows validators in the next epoch, with reward that will be added
near validators current -- shows current validators, which % online / seats
5. I was thrown out for not producing blocks, I solved the problem, how do I get back into the lists as a validator?
near call POOL ping '{}' --accountId OWNER
POOL- the account you want to ping
OWNER - the account that you will ping from (you must have a private key for this account  in folder .near-credentials)
6. When I try to use near login, I get an error that such an account does not exist 
You may be on the wrong network. To change the network, use the command:
export NODE_ENV=betanet (testnet, mainnet)
7. How long does it take to become a validator?
It takes 3 epochs to become a validator. 
In the first era you get into proposals. In the next epoch you will be included in the next validators and then you will be included in the list of current validators
8. What is the acceptable percentage of losses of produced blocks?
If you produce less than 90% of the blocks, then your validator will be thrown out after one epoch.
How long does an epoch last?
Betanet - 10,000 blocks
Testnet - 43,200 blocks
Mainnet - 43,200 blocks
9. How can I view the current server availability statuses
https://status.nearprotocol.com/
10.How can I find out the minimum price to become a validator?
near validators next | grep "seat price"
11. How can I create a wallet?
https://wallet.betanet.near.org/create/
https://wallet.testnet.near.org/create/
12. How can I view my validator key?
cat ~/.near/betanet/validator_key.json | grep public_key
13. How can I withdraw my tokens?
First you need to make an unstake
near call stakingPool_ID unstake '{"amount": "100000000000000000000000000"}' --accountId account_ID
Wait for 3 epochs, after which the tokens can be withdrawn
near call stakingPool_ID withdraw '{"amount": "100000000000000000000000000"}' --accountId account_ID
14. Can I delete my account?
Yes, the NEAR network allows you to do this. Delete an account and transfer funds to beneficiary account.
near delete <accountId> <beneficiaryId>
15. How can I check version NEAR RPC and my server?
echo rpc.betanet.near.org; curl -s https://rpc.betanet.near.org/status | jq .version; echo;echo 127.0.0.1:3030; curl -s http://127.0.0.1:3030/status | jq .version
You will need a package to display it correctly
sudo apt install jq
If you encounter a problem for which there is no solution in this guide, please create an issue on github https://github.com/nearprotocol/stakewars/issues or ask your question on https://stackoverflow.com/
