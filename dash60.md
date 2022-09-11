Episode Name: Tenderdash, consensus, Merkle trees & efficiency 

Episode transcript:

[00.00:00] Citizen Cosmos: Good space-time to you all! Welcome to the 3rd season of Citizen Cosmos. We kick off the season with Samuel Westrich and Ivan Shumkov from Tenderdash. We discuss traveling and cultural challenges, threshold cryptography, SDKs, merkle trees, and… grandmothers. The engineers explain the connection and the difference between Dash and Cosmos and the current options available for any devs out there looking to break some systems! Ivan, and Samuel, welcome to the show! This is going to be an unusual episode! I will ask you to introduce yourself first of all.

[00.02:02] Samuel: I'm Samuel Westrich. I'm the CTO at Dash Core Group. I've been involved in cryptocurrency since 2012. I made one of the first transactions in China long ago when bitcoin was at $2. Then I got involved with Dash at the time; in 2015, it was called Dark Coin. I wrote the IOS wallet, then became the head of the mobile team, and then last year, I became CTO. We’ve been working for quite some time on the Dash platform, Ivan will probably introduce it a little bit later, and inside of Dash platform for our consensus engine, we took Tendermint, forked it, and made some modifications proper to Dash, and this is probably what your listeners will be most interested in.

[00.03:05] Citizen Cosmos: Ivan, what about you?

[00.03:10] Ivan: I am about eighteen years in software development. I was primarily involved in the high load and distributed system development. In 2018 I joined Dash and Sam. My task was to develop the platform, and after some time, I was involved in protocol design and architecture. It was a very cool journey during these 4 years. 

[00.03:45] Citizen Cosmos: Samuel, you said you did one of the first transactions in China. Let's hear the story! 

[00.03:54] Samuel: At that time, my boss made a local bitcoins announcement, and he was a little bit nervous, so I was the one who went on to sell the bitcoins to people. It was a long time ago, and it wasn't that much. It was like $50 worth. It was exciting, I remember some people who had thousands of bitcoins, but nobody knew about bitcoin back then. I’ve lived through the journey, and I, remember how we went from $2 to $264, and back then, the only exchange was Mt. Gox, which was running on PHP and was extremely slow. It did not handle the volume well and was very prone to DDoS attacks. So suddenly started crashing, but you could time where the bottom was based on the lack of the number of transactions that needed to be processed, so I made a calculation, and it lasted about an hour to drop from $266 to $100. I had miscalculated, and I put a massive buy order at $207, and then it went up and down again and stabilized at $50. It was crazy volatility. Nobody knew what was going on. 
[00.06:36] Citizen Cosmos: Before I ask Ivan how he got into crypto, I just want to say this is the difference between developers and non-developers. You measured volatility with the lag
in the buy and sell orders. So, Ivan, how did you get into crypto? 

[00.07:16] Ivan: Before 2018, I held some assets, and one day a friend of mine asked me if I wanted to work at Dash. I was like: sure, why not? I had a two-hour interview with seven other guys who said “Cool, see you tomorrow!” 

[00.07:49] Citizen Cosmos: Were you not afraid to start working on some of the most significant tech projects? 

[00.08:06] Ivan: Not at all. I was looking for something new, and the blockchain technology was pretty interesting, so it was a match. 

[00.08:21] Samuel: I'd like to add to that one thing about Ivan. He's a very confident person. He just charges ahead in new tasks.

[00.08:32] Citizen Cosmos: I think that’s excellent quality for a developer because usually developers, in my experience, are a bit slow on the uptake but also super concentrated and determined, so I think it's rare to have both qualities. Another question, can you tell me a story behind Quantum Explorer?

[00.08:58] Samuel: In the early days, we did not know if China would kick people out because they were in crypto, so I had to stay anonymous around 2018. I did everything without revealing my identity, so I chose a Quantum Explorer nickname because I’m very into physics, so that's about it.

[00.09:30] Citizen Cosmos: It's a good story! Another question. While looking
at your profile, I've noticed that you travel a lot. Vietnam, Israel, China, USA, Russia. Would you call yourself digital nomads, or is that just part of your lifestyle? What’s that?

[00.09:57] Samuel: I wouldn't label myself a digital nomad. I’m more of an ex-pat just because after my internship at the University of Southern California in the USA, I had done my studies in France, and I was looking for something new, so I moved to China. I wanted new experiences in life, and then I stayed there for quite some time after looking for something new, so I moved to Thailand. I now use Thailand as a base and then just cruise around. 

[00.10:38] Citizen Cosmos: How would you recommend Thailand for crypto people, now that the web3 lifestyle allows people to move more and more?

[00.10:56] Samuel: Stay out. It's only for me!

[00.11:03] Citizen Cosmos: Ivan, what about you?

[00.10:06] Ivan: My journey began in 2015 when I moved to work in Vietnam. I worked for 14 years in St. Petersburg in a company we found with one guy. I was also looking for something new: a tropical country, unique culture, and exciting technologies. It was a turning point. After that, I became a digital nomad. Then I traveled crazily, changing locations every month or 2 months. Now I’m a bit tired of this and looking for a place to stay for a longer time.

[00.12:22] Citizen Cosmos: I can relate; that's what I've been doing for about 20 years. Let’s discuss Dash, Evolution, Dash Core, and Tenderdash. Let’s make some sense for myself and people who don’t know much about the project.

[00.12:50] Samuel: I'll start a little bit with the overview, and then Ivan can go into more detail about the Dash platform. So Dash has a payment chain, the primary chain on the main net, and we've been on the main net from 2014 to 2015. We've had a payment chain, it's a fork of bitcoin, and it allows for some extra features. We were 50% invulnerable based on technology that we call chain locks. We have instances in payments that are also using chain lock. These technologies are based on our master node network creating threshold signatures saying that these transactions or blocks can no longer be double signed or replaced by another obstruction in the chain. The Dash platform is a secondary chain that we've been developing. It’s based on the tendermint consensus that we've modified into tenderdash. Tendermint uses nodes that have different powers on the system,  in Dash, all of our master nodes are collateralized with a thousand dash, and they're all at equal power allows us to do something very cool, which is threshold cryptography. It allows for having just one sign to prove either the state or a block or anything, and this can lead to many use cases and new abilities that are not possible on tendermint with the same efficiency. It's a different approach it shouldn't be just different because we don't have the capacity for nodes to have other powers, but we do have the ability to cover threshold signatures that can be very useful for some projects. For now, tenderdash has not been released as a stand-alone service. Still, later this year, we will package it correctly, make a website, probably even rename it, and explain to people why they might be interested in tnederdash instead of tendermint. Ivan, you can clarify what for Dash platform is. 

[00.16:40] Ivan: I think we need to explain first what evolution is and how the history of these products is ending up. So basically, the evolution for that was there the release era which contains several releases and several products, and the main goal was to provide the social wallet that even your grandma could use to send you money using your name instead of cryptographic addresses, and that was the main goal why all these things started. The guys came up with the idea that they need to do specific modifications on-chain just only for this
wallet, but we could make it a platform so anyone can build decentralized applications
and store additional metadata on-chain. I think the concept is still the same even during this year. So Dash platform is the decentralized stock for the development of the applications. So you'll have the storage to store information, your application state on the chain, and be able to verify your clients cryptographically. You can operate it as a shared database. It has some limitations, but you don’t need to learn solidity or how smart contracts work, you can just use data contracts. You will be able to use some additional computation on-chain using smart contracts. The goal is to provide everything the developer needs, like CDN authentication.

[00.20:25] Samuel: It's targeted not only for developers in the long run, but maybe developers will build on top of the platform to create accessible services for users. For example, right now, somebody who wants to use blockchain may just own a restaurant but have no idea how to do it. With the dash platform, it becomes a lot easier. Let's say there's a contract for food delivery. Dash platform makes it very easy for people to use. You need to request data from the state in many blockchains out there. You have to use centralized services. In the dash platform, every one of our nodes responds in linear time to any request based on hierarchical authenticated data structures. It is merkle trees on top of merkle trees, and each of the merkle trees is actually a rotating merklized AVL tree. 

[00.21:45] Citizen Cosmos: Let’s get deeper into that. We can do that!

[00.21:55] Samuel: We were looking at various projects while trying to figure out how we store state. Tendermint uses AVL+ trees. When I say rotating, I mean self-balancing. Another Merk project is different from the solution the tendermint uses because nodes can also be deleted. Is that correct, Ivan?

[00.22:30] Ivan: Yeah, they also try to solve the I/O problems faced by the Tendermint and SDK guys.

[00.22:37] Samuel: Exactly. It got to do with the fact that you’d need to rewrite things on disk. There were some problems with AVL trees, that’s why we didn’t use them. So we kind of went in the direction of using Merk. We cared about secondary indexes in our system, and none of these trees supported them. So we turned to this hierarchical authenticated data structure written by the very smart guy at Google. We didn’t use everything, but our actions have a strong academic basis. It allows the smaller proof size and a lot of other important things. This structure means you can prove anything in the state with the series of merklized trees and then the state signature for the tree. For example, you can ask the platform for things like pizza restaurants in Bangkok, you can quarry the platform for this request, and it will give you back all the pizza restaurants and prove that it’s giving you all the pizza restaurants. No emissions. That’s what we’ve been building. 

[00.24:26] Ivan: It also supports ranges, it’s the most complex part. You can verify on the light client that all data is stored in the state. We should also mention that since we're using the threshold signatures recovered using the long-living master node quorums, it's a feature of the payment blockchain used by the chain logs. Since we already can verify the signatures made by quorum, we don't need to download all headers from the platform chain, we’re just getting back data, the merkle proofs, the miracle root, and the signature of the quorum of this merkle root. On the client’s side, you’re getting the proofs, and everything you need is data in one request, and you don’t need additional synchronization with the chain. That’s the difference from the original tendermint light client.

[00.26:15] Citizen Cosmos: Is there something for developers that allows them to build blocks and modules or use Cosmos SDK quickly?

[00.27:40] Samuel: Yes, we have three SDKs available, one in Javascript, one for IOS, and one for Android. They interact both with our platform chain and with our payment chain. However, we do not currently support the release of smart contracts. Basically, SDK allows you to store and register data contracts, interact with the system, and verify any
information you put in the system. For most projects, that’s enough, no need for smart contracts. Our building started with the use case. We wanted to create a Venmo-type experience that didn’t rely on addresses but relied on identities. When you send between identities, only you and those to you send money to know about the transaction. That was our main use case, and we built Dashpay, the first step we're releasing with the platform. That's why we didn't focus on smart contracts and instead on the quarry ability of data, so in the blockchain space, many projects have focused on smart contracts, we kind of went the other way. 

[00.29:58] Citizen Cosmos: The Cosmos Hub doesn’t have smart contracts. 

[00.30:03] Samuel: Yeah, you’re right. I don’t think it’s smart for every project to do the same thing. As a large crypto community, we should focus on an area of expertise and then build together and use each others’ projects in open source to hopefully advance mankind as much as we can. 

[00.30:30] Citizen Cosmos: I love it. We talk to CEOs and CTOs and always talk about their values and why they do what they do. Hearing the motivation is very important. 

[00.31:10] Samuel: I’ll explain a bit more what Dashpay is. With Dashpay, you can pay between people. Most of those you know register an address on the chain, so when you send money, it’s all trackable. You might not want some of your purchases to be seen, for example, if you buy sex toys. The point of dash pay was that if there's a separation between your identity used to create connections between you and other identities, you create this virtual tunnel that allows for payments between the two identities based on address spaces. If you were to lose your phone or anything or lose anything, everything is recoverable on mnemonic. There’s a derivation from your seed that can restore all the data you've ever had with the help of the blockchain, and it's not stored that much on the blockchain it's more stored in information derived from your mnemonic. It's a very cool system, which I mostly worked on before becoming CTO.

[00.33:30] Citizen Cosmos: Is the reason why Dash is sometimes classified as an anonymous system or not?

[00.33:35] Samuel; No. So back in 2015, I talked about how we had masternodes, the first
the use case that we ever made for the master nodes was (???), the ability to mix
your coins through the mass node network, we still have that feature, and that's why
we're sometimes classified as anonymous. 

[00.34:10] Ivan: The greatest achievement is that there is no connection between the public data and the payments, that's the main goal. We’re not using Cosmos SDK to build the platform chain for legacy reasons. Still, tendermint is a consensus library, and tenderdash is like 90% keeps the same API, so I think they will be able to use Cosmos SDK with tenderdash the same way.  

[00.35:00] Samuel: Here’s the thing. We're releasing our main platform chain this year, and then right after that, we're going to focus on the various projects we've built to do that, including tenderdash. If you can use cosmos SDK with tenderdash right now? I don't believe so. Mainly because there are multiple modifications, it would not take long, but it would take a few days to support them.  

[00.35:45] Citizen Cosmos: If there are developers out there who are ready to prove the opposite, you’re welcome! You talked about application-specific blockchains, and I looked at your road map, of course, but still, when is IBC?

[00.36:16] Samuel: To do IBC, we must do something else first. The most significant change between tendermint and tenderdash is why IBC doesn’t work natively. One uses a threshold signature mechanism, and the other uses DSA, but it’s not a threshold signature. To have IBC, the tendermint and tenderdash have to understand each other. Tenderdash can understand tendermint, but tendermint can't understand tenderdash yet, so we have to make a pull request to tendermint to allow for IBC for tenderdash. That hasn't been done yet, and we will get around to it. 

[00.37:18] Citizen Cosmos: Will it be through a direct relayer? 

[00.37:27] Samuel: Yeah, the chains will communicate like all IBC between tendermint. The difference is that the signature verification is not supported in tendermint for tenderdash. One of the negative aspects of tenderdash that I can come clean on is that we ripped out some stuff from tendermint and replaced it with the stuff we needed. We would not have ripped out everything if we'd done things perfectly. We’d made sure all use cases were covered. Because we ripped out some stuff, we need to repair some of the stuff so it can more easily understand tendermint for IBC.

[00.38:20] Citizen Cosmos: I have another question. If any validators out there who are interested in becoming masternodes or validating the network that is going to be launched, is there anything you can say or add here on what they should look for? 

[00.39:14] Samuel: There are many guides on becoming a masternode. In Dash, we have right now on main, the payment chain and platform will be released coupled with version 19 of our core payment chain. We will provide an installer of the platform and core services on the VPS node, or you can do it manually. There’re guides for installing testnet as well.

[00.40:18] Ivan: I think we should provide some links to documentation for the people. They're two pretty active communities on Discord, one is mainly for investors, and the other is the development community - Dash Incubator, it’s another DAO space in the Dash, they are doing a lot of work around the ecosystem and helping people to join the testing. They also have a very nice bounty program. We welcome all developers to our platform. 

[00.41:13] Citizen Cosmos: I think it's like cool to see more and more developers joining from different places and finally developing this internet of blockchain, in my opinion, rather than stand-alone. 

[00.41:50] Samuel: We are doing a big bounty program to try to break our system. If developers are listening to us right now, soon, in 2-3 months, I’ll call one of you to smash!

[00.43:17] Ivan: One of my biggest wishes for having IBC and providing a light client for tenderdash is a data contract approach for people to test. Since IBC allows to do some cross-chain contract calls, I see a pretty exciting combination. For example, you can use smart contracts on one chain to do some computation in consensus and store and read the state directly in the application without calling smart contracts using IBC and Dash platform. Combining available technologies to provide a better stack for developers will be interesting. 

[00.44:18] Citizen Cosmos: Final question. What keeps you motivated in your daily life?

[00.45:13] Samuel: In my life, I did have a personal event that lasted for like two years where I stopped working, and I was very sick, and after that, you think about what you bring to the world. Before all that, I cared about having fun, getting money, etc. Then, I thought about how my life would matter after I was gone. I think what we’re currently working on will matter, which keeps me going. There’s always doubt, of course, it is healthy to have doubts. You can’t be sure that what you’re doing will matter. But when I think about how I can contribute, I’d prefer using the skills and knowledge I already have rather than spending years learning something like medicine. 

[00.46:45] Citizen Cosmos: That's a great answer! Ivan, what about you?

[00.46:57] Ivan: I’m more selfish, honestly. I have fun doing what I do, my coworkers are my friends, so the pleasure and the contribution are the same things for me. I want to see the project I’m working on thriving and prospering, so I always think of what else I can do to improve it. 

[00.48:13] Citizen Cosmos: That’s some fantastic combination you guys have. It’s been a huge pleasure. Thank you for the conversation!

------------------------------------------------------------------------------------------------------------------------------------------------------------------
If you want to support us in our mission of creating and spreading educational content and aligning the goal of different communities, please stake with us (guide you can find [here](https://www.citizencosmos.space/staking)) 
- [EVMOS](https://www.mintscan.io/evmos/validators/evmosvaloper1mtwvpdd57gpkyejd566s24afr9zm5ryq8gwpvj) 
- [ATOM](https://www.mintscan.io/cosmos/validators/cosmosvaloper1e859xaue4k2jzqw20cv6l7p3tmc378pc3k8g2u) 
- [BOOT](https://cyb.ai/network/bostrom/hero/bostromvaloper1f7nx65pmayfenpfwzwaamwas4ygmvalqj6dz5r)

and join our [Discord server](https://discord.gg/kJaG3EucCX) and help us grow the interest for web3 to the masses.

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fcitizen-cosmos.github.io%2Fblog%2F61epicentertv.html&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com) 
