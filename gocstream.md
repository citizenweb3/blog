**[A citizen odyssey, ep. XII, special mission: Game of Chains recap](https://www.youtube.com/watch?v=RXMoF18bckU)**

The Interchain Security protocol (ICS) is to be run in Cosmos in January 2023. To test it, an incentivized testnet program called [Game of Chains (GoC)](https://github.com/hyphacoop/ics-testnets/tree/main/game-of-chains-2022#phase-1-two-dummy-chains) was launched.
It’s the third public incentivized testnet in the history of Cosmos, after Game of Stakes and Game of Zones.

Citizen Cosmos, [being a participant](https://provider-explorer.goc.earthball.xyz/validators/cosmosvaloper12zmahaunzfq8w3fwkv6uds69jsqszltyp5tk7m), called members of Testnet [Jury Jehan Tremback](https://twitter.com/JTremback) [(Informal Systems)](https://www.citizencosmos.space/jelena)
 and [Udit Vira](https://twitter.com/UditVira) [(Hypha Worker Co-operative)](https://twitter.com/hyphacoop) to talk about GoC and ask them questions of concern.

***What is GoC?***<br>
First, as part of a brief historical overview, Udit explained what [GoC](https://citizen-cosmos.github.io/blog/gameofchains.html) is and how this game differs from the previous two Cosmos games. 
Game of Stakes was based on testing proof-of-stake mechanism, its goal was to understand all possible attack vectors. 
[Game of Zones](https://www.citizencosmos.space/game-of-zones) came for the launch of IBC, and people were testing how IBC packets were being relayed between the different zones, which provided an
opportunity to actually prove that this IBC ecosystem of sovereign interoperability where we had independent zones working together was something that could come to fruition.
The goal of ongoing Game of Chains is to test Interchain Security. The idea of ICS is that one blockchain (The Cosmos Hub) can share security with another chain. 
This feature was developed by Jehan’s team, by the way. The format of incentivezed testnet basically means that validators come and help run this network completing
certain milestones to surface attack vectors, bugs and other issues. There are rewards for this because it’s a lot of work. 
Also, rewards make this process a lot of fun by providing an environment where participants both compete and still help each other. 
All of this ultimately helps a lot to polish that really complex piece of technology which is ICS.
[![streamgoc.png](https://i.postimg.cc/T17mkjKN/streamgoc.png)](https://postimg.cc/wRN7MmcD)
***Preparation for the testnet***<br>
Of course, it was necessary to prepare thoroughly for the testnet launch. Jehan shared how preliminary testing within the repository was going and about the automated
tests that ran on every pull request. One of the types of tests is setting up a virtual network with several different chains: provider chain, which provides the 
security, and consumer chains which draw security from provider chain. Another type of test is a model based test which uses a reference implementation to generate 
many different scenarios in the form of actions that different actors in the network take. But no matter how sophisticated those tests get, testnets are more thorough
method of testing, because people are unpredictable and they do all kinds of weird crap instead of normal things.
Udit added up that another form of preparation is social planning. What are the tasks? How people are going to hit all the criteria? What are the phases of the game?
So significant work was done in that area of planning. Udit also touched on infrastrucure that has to be used by participating validators, since they have to run 
both on proveder chain and consumer chains, they need to be relayers. For that, GoC has to have quite a few supporting tools. And last but not least, it all requires
communicating. Sometimes things break during a testnet running, and people should know what’s going on and how the plan is being adapted in new conditions.

***Mitigating risks***<br>
How do we make sure that binaries we are being given are not malicious software?<br>
According to Jehan, this is one of the key things.<br>
At least for the first few consumer chains there will be a process of due diligence that Jehan’s team will go through to look at their code. There are a few ways in which consumer chains can harm either The Cosmos Hub or the validators:
1. A Cosmos chain is just a binary that runs on the computer, so it could delete your hard drive or use your computer to send spam out or anything a computer program would do. Jehan and the team are not expecting to have that situation for the first few consumer chains. Everyone would know who they are and who’s building them. As things become more decentralized and there’s a higher volume consumer chains running, you’ve got to run it in its own virtual environment, but validators do that anyway when they are running a new chain. So that’s not a huge concern.
2. Consumer chain could potentially steal the private key given by a validator or sign malicious messages. This potential harm is limited by the process when validators inform The Cosmos Hub saying they want to use this key for this consumer chain and they can do that before the consumer chain even goes live. If you’re a validator and you see a consumer chain proposal is going to pass, you can provision a new box to run it and you’ll go to GitHub, look at the code and try to get the full node running on that virtual server. At the same time you initialize a new private key and then send a message on The Cosmos Hub saying this is the key to be using for this particular consumer chain.
3. The largest vector is that some malicious consumer chain could have hidden the code that would send a ton of downtime slashing packs at once slashing every validator on the Hub and jailing them. Then they could register a bunch of fake validators and that malicious validator set would come in and control all the IBC bridges and be able to steal a lot of money. How to mitigate that? (1) The last form of defence is a circuit breaker which only allows a small percent of the validation power to be jailed per hour and make obvious to everybody that the attack is happening. Then we maybe halt the Hub if it’s really bad and take down the consumer chain. (2) There is a pretty robust capability system within Cosmos SDK as to what modules have the ability to send packets claiming to different other modules. When consumer chains are submitted we can make sure that there’s no possibility of the consumer chain’s own code being able to send packets claiming to be ICS module. This can be automated in the future.

As a conclusion for this part of the discussion, it should be said that there are some other risks too, but they are really not as much concern as those three, because they are more based on mistakes than a deliberate attack.

**Already detected bugs**<br>
Jehan gave a detailed report on one of the bugs:<br>
“There’s something called [iterators](https://en.wikipedia.org/wiki/Iterator), which are kind of functions in the code, which go over a collection of items and you basically have to return from the function, you have to return _true_ or _false_ depending on whether you want to keep going to the next item and look at the next item in the list or whether you want to stop looking at the list. And so we had a situation in our code where we had some iterators you had to return _true_ to keep looking at the rest of the list, so it was either return _true_ to continue or return _true_ to stop. And so some of the iterators are written that you would turn _true_ to stop, and some of the iterators were written that you returned _true_ to continue. And so what actually with the bug happened was basically that there was an iterator over the consumer chains running on the provider chain, so when it’s doing operations involving the consumer chains iterate over the consumer chains, and it was that function was returning the wrong thing, like was returning _true_ when it should have returned _false_ to continue. And what happened is that that iterator would stop after looking at the first consumer chain. Basically, the provider chain was only ever really interacting with the first consumer chain, the second one was being left out. So that was basically the bug, and so we fixed that, and we also went in and we refactored everything so we’re consistent about the stuff, and we got the upgrade.”

There were also some issues in relayers, which have been resolved now.

**Phases of GoC**<br>
Udit gave a quick review on the Game of Chains phased approach.<br>
There are three phases:<br>
I. Testing dummy chains (Apollo and Sputnik), very basic, the most simple chains, to make sure that we can run the provider chain.<br>
II. Testing actual chains. Expecting to see some of the consumer chains that are going to be launching next year (e.g. [Neutron](https://www.citizencosmos.space/neutron)).<br>
III. Asking anybody in the public or validators to submit consumer chains of their own.

In conclusion, a quick Q&A session was held, during which some advantages of Cosmos SDK were pointed out.

------------------------------------------------------------------------------------------------------------------------------------------------------------------
If you want to support us in our mission of creating and spreading educational content and aligning the goal of different communities, please stake with us (guide you can find [here](https://www.citizencosmos.space/staking)) 
- [EVMOS](https://wallet.keplr.app/chains/evmos?modal=validator&chain=evmos_9001-2&validator_address=evmosvaloper1mtwvpdd57gpkyejd566s24afr9zm5ryq8gwpvj) 
- [ATOM](https://wallet.keplr.app/chains/cosmos-hub?modal=validator&chain=cosmoshub-4&validator_address=cosmosvaloper1e859xaue4k2jzqw20cv6l7p3tmc378pc3k8g2u) 
- [BOOT](https://wallet.keplr.app/chains/bostrom?modal=validator&chain=bostrom&validator_address=bostromvaloper1f7nx65pmayfenpfwzwaamwas4ygmvalqj6dz5r)

Join our [community](https://discord.gg/kJaG3EucCX) Lets build a future where communication is decentralized. May the code be with you. 

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fcitizen-cosmos.github.io%2Fblog%2Fgocstream.html&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com) 
