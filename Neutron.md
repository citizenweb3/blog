Interchain Security is probably one of the most interesting narratives in crypto now. We have researched Neutron, a project that will use Interchain Security in no small way. In this article we will break down 

- Quark Testnet
- What is Neutron
- Interchain Security
- Interchain Accounts
- Interchain Queries


**Quark Testnet**

Neutron will launch Quark testnet to find bugs and fix them. This testnet will not be incentivized and will not use Interchain Security. This testnet is more for advanced users and developers.

Quark will run for 3 weeks. Testnet participants will test the network and report their results and feedback in late November.

Technical сases are broken down in categories (Performance, Interchain Accounts, Interchain Queries, etc.) and their completion is expected.

Kindly note that Quark and the ICS Incentivized testnet are different test networks. The Neutron ICS feature will be tested on the ICS incentivize testnet first.


**What is Neutron?**

Neutron is a secure platform for Interchain DeFi powered by Tendermint and built with Cosmos SDK. Neutron’s tech helps developers to launch smart contracts and gives tools to interoperate with other protocols and appchains. Neutron is incubated by P2P Validator who also were founders of Lido Protocol. Moreover, they received 50k ATOM funding in Prop72.


**Interchain Security**

Interchain Security lets validators from a Provider-Chain produce blocks for a Consumer-Chain. Node operators are rewarded with additional native tokens, that will be distributed from consumer chains fees.

In a nutshell, Interchain Security provides Neutron with the same degree of security as the Cosmos Hub.


**Interchain Accounts**

Interchain Accounts (ICA) let Cosmos blockchains control accounts on remote zones via IBC, instead of local private keys, and write transactions that can be executed on the remote chain.

Neutron will be both a “host” and a “controller” and will launch with a custom implementation that makes Interchain Accounts available to smart contracts.

It means, smart contracts on Neutron will be able to interact with modules and zones from other ICA-enabled Cosmos chains and vice versa.


**Interchain Queries**

Interchain Queries (aka ICQs) are an essential building block enabling devs to securely retrieve data from remote zones. Queries are fundamental to DeFi protocols: They are used by DEXs to calculate swap prices, by Money Market to determine a user’s loan-to-value ratio, etc.
Here’s how Neutron makes Interchain Queries work:
 On the querying zone, the ICQ module collects query requests and makes them available to relayers.
The relayers go to the queried zones, find a “value” for each “key” and package them with cryptographic proofs.





