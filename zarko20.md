<iframe src="[https://player.fireside.fm/v2/7d8ZfYhp+EWSIk7HP?theme=dark](https://www.citizencosmos.space/zarko)" width="740" height="200" frameborder="0" scrolling="no"></iframe> 

#citizencosmos

Citizen Cosmos podcast, episode 20

Tushar Aggarwal, Persistence and Institutional DeFi

19h of December 2020

[00:00:00] Anna: Hey, it's Citizen Cosmos, we are Serj and Anna, and we discover Cosmos by chatting with awesome people from various teams within the Cosmos ecosystem and the community. Join us if you're curious about how dreams and ambitions become code. 

[00:00:17] Citizen Cosmos: Hey everyone, welcome to Citizen Cosmos! And today, we have Zarko Milosevic with us, the chief scientist at Informal Systems. Who is, of course, one of the leading contributors to Tendermint and the Cosmos ecosystem? And we will find out all about it from Zarko. Welcome! How are you? 

[00:00:39] Zarko: Welcome guys. So very happy to be here and talking to you. 

[00:00:43] Citizen Cosmos: Yes. How are you today? 

[00:00:47] Zarko: I'm fine. It's a bit of a rainy day in Novi Sad here. So unfortunately, we are kind of... We are locked in the house because of the rain. So luckily, we are not locked for other reasons, but it's a rainy day. I'm looking forward to finishing with work and it's going to be tough. 

[00:01:03] Citizen Cosmos: So I'm not very far away from you geographically. I passed Novi Sad a few weeks ago on the way to Sophia. Glad to hear that you guys are okay because, obviously, the latest European lockdowns do not look good. So, okay. Let's skip that. And Let's start with the obvious thing and, um, a small intro. And I think everybody would love to hear this too. So tell a little bit about yourself, your role at Informal Systems, and what exactly you are working on lately. 

[00:01:37] Zarko: Yes. So I have, let's say, formal training in distributed systems. I did a Ph.D. in Lasagna here at PFL, a few years ago. And, uh, my topic of the thesis was Byzantine fault tolerance protocols and at the time, so this was like before the time of Bitcoin and all the fancy money.
 
And, uh, we just studied there, the protocol. And at that point, it was purely theoretical stuff. And so like there was no potential application on the horizon. And then, as we all know, this has changed radically in the last few years. And, um, and so I'm kind of after a small break in the industry, I am looking very carefully at Byzantine fault tolerance protocols.
 
So what is different in Informal from what I was doing before, is that we added a bit of a formal verification flavor to it. So we have quite an amazing team of formal verification experts. And then we are trying to get there with distributed system engineers to design distributed systems, which will be more reliable and correct.
 
And we kind of try to do this in a team of people with different skills so that we are all on board with the project; we try to have different concerns and then ensure that the final product is more correct and reliable. 

[00:02:50] Citizen Cosmos: When you say final product, what exactly do you mean by that? What exactly is the specification that you're working on right now?

[00:03:01] Zarko: Right now, we are mostly focusing on IBC. So we are working on an IBC handler and, uh, we are also working on the relayer. So we implemented these in Rust. So this is about the Informal internal team.  We design protocols in this case. IBC is like most of it and it's ready, let's say the protocol is there.
 
So what we are doing, is more like trying to formalize the protocol, try to do some kind of more... or let's say a protocol-oriented security audit. And we are working with the GO code base, and we are implementing it in Rust. And we are also trying to, at the moment, if you're involved in designing, a cross-chain staking protocol, so this is kind of something quite hot and new, and also helping, uh, colleagues from Interchain Berlin. For example, with the protocol in Tendermint Go. 

[00:03:48] Citizen Cosmos: You mentioned there for a second - correctness audits, and in our email intro with, Arianne, who's the COO of Informal Systems, for everybody who's listening. She mentioned that what you're working on is something to do with correctness and assurance audits.
 
Now, first of all, for everyone who's listening, and I'm sure somebody does understand what it means, but... what is an assurance audit in simple terms? What is a correctness or a correctness audit, and what is the correct way to say it? 
 
[00:04:18] Zarko: That is a great question, because even internally in Informal, as people come from different backgrounds, we were recently going through the exercise of formalizing this notion.
 
Especially if you talk about distributed protocols, which are like blockchain, essentially, everything is a liability problem. We are interested in not just looking at traditional audits, where you are kind of trying to find some, like maybe, low-level programming issues or like, um, maybe bad programming styles, or discrepancy between the documentation and the code.
 
In addition to all this stuff, we are trying to go a step further and try to formalize. Really understanding what the protocols should be doing. And then we try to ensure whether it does it. So like, as we also don't code ourselves, all the code is in the ecosystem, we are not necessarily able to apply the same techniques we are doing in the internal development, which is more like, what we try to do is have something which is more like correct by design, where we're having parallel the protocol design, formalization implementation.
 
When we look at the different people's codes. And the specs we are trying as the first step to formalize this, we try to understand what the code is supposed to be doing by looking at both, the code in the spec. We write the formal spec in a form of pre-condition and first conditions of the functions in the code.
 
We formalize this in TLA plus and then try to generate with the model checker, interesting test scenarios, which allow us to essentially exercise the path, which you might not be able to do easily with the manual tests. What we try to do really with this is to do with this assurance, is to somehow document traditional audit, where we look at the code, try to find issues with something which is more like, uh, using, let's say formal tools.
 
So that is also at the end of the correctness assurance audit. You have, in addition to the report where you have findings with the list of bugs, or like some, let's say, suspicious stuff in the code, you also have the formal spec, and you have the automated tests, which stay after we finish with the assurance, so you can use this after. 

[00:06:20] Citizen Cosmos: Could I narrow this down and please correct me by all means if I'm wrong, to simplify this down, and, of course, not to underestimate what you guys do, but could we simplify it to the fact that each new blockchain or zone or whatever you want to call it that will come into Cosmos can rely on those outfits in terms how smart contracts in Ethereum rely on security audits. And we can say here's a new blockchain. They run the correctness or assurance audit. And then we see, okay, here and here and here we have some holes. They should do some fixes. Whatever. Is that kind of the thing that we're talking about? 

[00:07:00] Zarko: Yeah, exactly. So this is what we are hoping for as we are seeing an increase in the number of Cosmos-SDK applications, especially with the IBC launch coming soon.
 
Essentially, what we try to do is to try to come up with a framework that will more or less (be sufficient) for people who are developing the key applications, they have this as a kind of building block. So there is the stuff we'd like that sometimes might work in some cases out of the box, like for IBC, we plan on having the modules.
 
So you can have test scenarios generated or if you use IBC like you're developing your application on top of IBC channels. You'll already have like interesting test scenarios just to kind of catch for some correctness audits, but then also with like a small change in the spec where you add the semantic of your particular application, then we can do even more stuff.
 
So we are kind of trying to do it in a more composable way so that you already have something let's say by default, you can only start playing with this and see how it works. And then if we are able to formalize your particular application, then you have kind of full coverage. It's really like the hope is that all zones, which enter Cosmos could have some level of correctness assurance.
 
And then ideally, you know, we'll have kind of almost formally verified code. Like, although this is something which is like, maybe be too ambitious, we are hoping for, and going in that direction. 
 
[00:08:18] Citizen Cosmos: It makes sense. Because I personally said it previously and, I think I'm not the only one to say that of course. There is one personal thing, that as soon as IBC launches completely like I'm not talking about just testing in terms of Stargate and Big Bang or whatever, but where it's not going to be just developers, so we're going to use it. But it's also going to be, let's say... I don't wanna use the words lesser quality, but okay.
 
We all saw the story of smart contracts, and how they evolved, right? And the level of development that was required to launch a contract. What's going down, is that more and more tools were in place. And I think that in Cosmos, we're going to see even a bigger hole of a lot of chains just flow in and flow in and flow in.
 
And I think that what you guys are doing could be important for people to make sure. But the question is that it sounds like what you're working on is not important only to the Cosmos ecosystem. I think that what you do could be used anywhere within DLT or with any DLT technologies used. Do you have any thoughts about that? 
 
[00:09:23] Zarko: Yeah. As with any startup, we are super ambitious. And so we want to conquer the world, but just like the interests of making it, being more operationalized, we have a more official plan. We are targeting Cosmos because this is, first of all - it's our home. And this is where we have most of our understanding and knowledge about how stuff works.
 
And also, this is where we want kind of to, we are incentivized to have, let's say a more correct software that directly outsells. But if you talk about fundamentally what we are trying to do there, we are talking about deterministic state machines. And so essentially in any blockchain applications on top of the blockchain, whatever layer one you have, you have a deterministic state machine, like being in the form of a smart contract or something like the SDK.
 
Or Substrate, you are talking about deterministic state machines, which are the mental knee faced with the same kind of problem. And also applications we have in mind for the first bus will probably be very similar. Like we were talking about talking transfer as a kind of the main driver, and the security models are kind of similar.
 
What we really try to do here is just focus first on Cosmos SDK because in verification, let's say that the run time matters, and we need to sort of focus on stuff in order. And so right now we have primarily to look at Rust and Go. All the model-based testing approaches we are using is a bit language neutral. So we generate interesting scenarios outside the runtime, and then we have a constable driver. So we can, in theory, write a driver for any runtime. It's just a matter of, let's say, having time and knowledge of how it works to be able to write the driver, and then you can already benefit from the test scenario. And so what we are really hoping for is really expanding our view.
 
So we'll start with the Cosmos and then we are definitely interested in looking into other runtimes, like Ethereum, for example, or Substrate. I don't know when, you know, we'll have resources to do this, but it's definitely on our radar. Definitely. 
 
[00:11:16] Citizen Cosmos: Yeah. And it's great that it's language-neutral because obviously, that opens the doors for all sorts of things, rather than just sticking to Go.
 
Cool. And, I'm going to move a little bit and take a step backward here. We do have questions in regard to what you do and the research, but we'll come back to that in a second. 
You mentioned startups there, and we've looked at your history, which is on LinkedIn, of course. Sorry. You know, social networks, say a lot about a person.
 
And you've worked for Intercahin foundation before, you've worked for Tendermint. You worked for a few other companies, but what's your personal blockchain story, especially being a researcher or a scientist? I don't know what word you prefer here. 

Of course, you just said you were doing a Ph.D. before it was popular. So, this is already a huge part of the story, but if you could expand. 
 
[00:12:08] Zarko: So after I did my Ph.D., I worked in the industry as an engineer in Switzerland for a few years, I worked for two companies there, mostly developing distributed systems in Scala and Java. And then essentially, after some period of time living in Switzerland, the family decided to move back to Serbia.
 
And then, I actually joined a university here. The university model in Serbia is let's say not ideal. You normally need to do something aside. And so I was looking for what I could do aside, and then I stumbled upon Tendermint. And so I remember I was looking at the webpage and they had business on state national replication at their front page.
 
Like the landing page, you see this? And I was like, oh my God. These guys are like crazy. Who would advertise themselves as like doing this thing? Because in academia we were sort of like the whole effort was trying to kind to hide this, you know, to say that performance is not too bad, you know, you don't need to see this. You don't need to expose this. And then the guys have a start-up, and they were like putting this on a landing page. And then even more interestingly, they were having a hiring page, they're having a job for, I think it was called research scientists or something like this, where they were asking for people familiar with PBFT and DLS, you know, and someone who could design BFT protocols.
 
And I was like, there's no way that people would be paying me to do this. Like, I will do this for free. And so like, this is how I met Bucky and Jae. And at that time the company was All In Bits or now they're called Tendermint. So I joined and started working with them on Tendermint and this is more or less how I enter the blockchain space.
 
So before that, I was not really into Bitcoin or Ethereum. I was just hearing, you know, something is happening, but, I didn't have time to really look carefully into this, but then decided to remain, I got exposed to the blockchain ecosystem, met people, and then later at one point, with Bucky we focused more on Interchain. Hired a research and engineering team there and then spun it off into Informal. So my blockchain story is pretty much Tendermint or Cosmos-oriented. I was just moving entities, but it's basically a borderless story about Tendermint or Cosmos for me. 
 
[00:14:15] Anna: So how did you find your area of specialization?
 
[00:14:18] Zarko: I wanted to do distributed systems because somehow I was always fascinated by the fact that computation can essentially be executed between multiple computers. Like, just the fact that you are constrained by a single computer resource was, sort of, always a bit ridiculous to me. So I was kind of, from the Bachelor's degree, interested in distributed systems.
 
And then, at TPFL, there were two very strong labs doing fault tolerance and distributed systems. So like during my masters, I get to know basically both of those labs. And then, they had open PhD positions. So then, I joined this old system lab at that time. It was professor Andrew Shipper, who is a very well-known person in the distributed system research community.
 
And then they're like,  byzantine flaut tolerance is the area where the fault scenarios are completely open. It's super arbitrary, essentially anything is allowed. So this was something which was kind of, I was super curious to see what we can do if some people can do whatever they want. It sounds a bit, you know, like impossible and there are some fundamental impossibility results, but just, you know, being in this mental model where, you know, we want to do something together and then a subset of us can do whatever they want. And we still are able to provide some guarantees. It's like you're ethical, I think a fascinating problem. 
 
[00:15:37] Citizen Cosmos: Do you think, as somebody who's not only specialized but also had the chance to, I would say implement it on a bigger scale because, as obviously, Cosmos is not a small project, like on page 25 or whatever of top projects? It's a top project with a lot of other projects working on Tendermint. 

Would you say as somebody who's involved, that the implementation is as good as the idea itself has been or is there still a long, long, long way to go. Where we can say, okay, the implementation of distributed consensus is, I don't know what that place will be - where we can safely say, Oh my God, this is good. It's working. We don't need anything else. Like how far away are we from this step? As somebody who's been involved in it.

[00:16:16] Zarko: This is something that is kind of pretty interesting, in my view. I think that the implementation of Tendermint is super solid. And, so both the protocol-wise and implantation-wise, of course, we can always talk about improvements, but the maturity of the protocol understanding and you know, protocol, design, and maturity of the implementation and testing in Tendermint are pretty amazing.
 
And also, what is interesting is that Tendermint opens the space for, almost a new, what we call the theory system model. It's gossip-based, Byzantine fault tolerant consensus-centric. It was never done before. So essentially, there is a stream of knowledge of understanding, which is going from the industry to academia, where we kind of already did something, and now people in academia are trying to help us and work with us to formalize this and to expand this thing.
 
And so in that sense, I think that in general, I would say the blockchain is an absolutely fascinating area, because you have more or less, a lot of very fundamental computer science fields and research happening on the first line of development. And so in that sense, I think also it's for the young researchers, it's an amazing place to be because you're able to experiment. You're able to design new stuff in a model, which has never been done before, and you're able to directly, you know, implement the stuff and people are using it. And the feedback cycle is super fast. This is amazing. So if you compare this with academia where, you know, you work on something, you go through the review process, you implement a prototype and then people might never look at this or never use this thing.
 
Although it could be a super cool idea and super sound here. If you come up with something interesting. It might be in production like three months later if I can just tell you an anecdote, like what happened in Tendermint, because now we have these multiple entities in the Cosmos ecosystem, and we, of course, collaborate, but we don't necessarily like the common timelines, so we operate in parallel. 

And then we were working on a fork accountability protocol for Tedermin, I mean like formalizing this, designing this thing. And this is also, I think a fascinating theoretical brick. And it will serve not even in a super ready-to-be-used shape. We were working on this, but then there was something else, you know, the IBC focus, so we switched to this thing. And then, we haven't talked with the interchain Berlin team for some time. And then at some point I discovered, you know, they asked me for a peer review, and I looked, and they implemented the stuff already! And I was like, Oh, OMG, you is not done. You know, they implemented this thing.
 
It's amazing. The speed with which we move, from the idea to implementation, is amazing. 

[00:18:43] Anna: It's interesting to speak about product growth. One project that pops into my mind is Cardano. What do you think about this project? 

[00:18:55] Zarko: I was going through their white paper and technical reports at some point.
 
I think it's a really... It's a sound project, and they managed to hire an amazing team. So they are doing super cool stuff. And they are also, I think, In terms of goals, we are pretty aligned. So they also want to have more correct and reliable software. And they're also close to the formula verification. These are, I would say the stuff where we really share the same values on. On the other side, they have a bit of a different approach just in terms of the core protocols they're doing, and the people designing the core protocols come from a security background. I have a bit of trouble, let's say, feeling comfortable reading those papers. Because it's just a different vocabulary. So like, uh, I don't want, let's say to say by any chance that it's not good, it's just that it's not something I get used to. I was a bit struggling to figure out what was really happening there, but I think it's a really good project. Also, they have tight collaboration with academia. This is also something where we are also doing it and trying to expand on this. And I'm really happy to see this kind of project. I really believe that what we are trying to do the way, how I'm thinking more generally about the blockchain is that, we are trying to automate in a kind of distributed way, some tasks we are trying to ultimate more and more of this task.
 
And the way we are coding these automation scripts. It is not ideal if you think about this, like in different programming languages. Like it's super error-prone. The tools given to us have lots of flexibility. And then this flexibility also comes with bugs very frequently. And so I think that we really need if you really want as a society to rely more on these automation scripts for important areas. And there are more and more of our lives. I think we need to be able to do this in a more correct and sound way.

[00:20:45] Citizen Cosmos: And we do have a few questions about that as well, but the question that popped into my head now, is while you were mentioning a lot of academic research, and you mentioned younger researchers as well. So it's kind of an obvious question, I think from my side here. And I'm sure that Anna would ask that as well and so would everybody listening. 
 
What does a day of a researcher look like? What motivates a researcher to find the next research topic and to say, okay, here's distributed consensus. I want to pick this particular thing and not this and write essays on it, test it, or whatever. How does it happen? I mean, do you wake up and just take a random book? Tell me about it. 
 
[00:21:22] Zarko: I can just, of course, talk about the reality, a smaller experience, and people I know, but normally there are some like seminar works, which are, there are like papers, and you always start from there trying to figure out what are, let's say some common laws. And in discipline computing, we also have these frequent possibility results, which are giving us boundaries.
 
You know, what is possible, what is not. In pure academia, you try to figure out some scenario or some use case that is not covered. So it's more like trying some niche, and then you try to develop something more interesting. Their motivations are publishing papers. This is how you get recognition. And this is how you're able to get your teases, if you're able to get promoted to get a professorship position, etc.
 
It's sort of oriented mostly by publications. And this is something which is maybe not ideal, because you are not necessarily having hooks with the real world. So you're trying to come up with something and then, we hope it might be relevant. We don't necessarily need academia to produce only, you know, relevant or practical and relevant results.
 
If you talk about being a researcher in a more industrial concept, it's a bit of a different story because we don't need to invent challenges. Challenges are everywhere. Essentially more or less, whenever you look around there are challenges, and then it's really about trying to figure out what is the sanest way to address them.
 
And also having in mind that people will implement this. So we cannot go fancy with the super complex stuff. Simplicity is a kind of requirement, or it's very important. And also being able to communicate what you do. This is something which is also, I kind of realized this myself after I joined All-in-Bits. If you're not able to talk with the people in their language, you are sort of. You're missing the point. You can design an ideal or beautiful protocol yourself. But if you cannot express it to the engineers in their terms, it will never be used. Like it's a completely lost start.
 
[00:23:18] Citizen Cosmos: This is a very interesting point to see that communication is still communication. Right?  And then another question is: well, when you find a challenge, as you said, the challenge always surrounds us. And when you look for an answer, do you usually try to avoid other people's work previously for the challenge? Or the opposites - you research first what others did, and then try to implement your own solution? What's your way of working?

[00:23:43] Zarko: There is something interesting in the blockchain space. The normal approach I will do is to look for related work. And before we figure out something new, we try to see what people did before and then try to extend it or if possible, you know, reuse the work, being done. What is kind of interesting is that if we talk about most blockchain research, there are some fundamental results there, but then there are a lot of problems which are... the system model has changed. Like we have, for example, many participants, or we have these different sorts of halt months. Now we have rational nodes. Like people are not just arbitrary, bad or good. They are, and there could be a variance. The spectrum is broader there. And then also we're talking about gossip-based networks.
 
So all that stuff is just changing completely. The problem is you cannot easily reuse the algorithms which are designed for different systems. So there is a sound base, and I think it's a good idea to always look at what is done and not reinvent the wheel. But in reality, it's true that in many cases, we need to design things from scratch because it hasn't been done before.
 
And one thing which is sort of also interesting is that the amount of technical reports or papers produced in blockchain space is huge. And I frankly, you know, at some point I stopped following because it's almost impossible to follow what's happening. So I sort of try to do my work and just look at what is related to that bit. Narrow focus. So it's really hard to catch up with everything happening outside. 
 
[00:25:12] Anna: Yes. Definitely. So what sources of information do you use daily? 
 
[00:25:15] Zarko: You mean like in general, like for daily work?
 
[00:25:17] Anna: I mean information about projects, tech, and what is happening in that? Yeah. And in the industry, maybe some resources, research blogs, or any kind of informational resources.
 
[00:25:35] Zarko: I'm registered to a mailing list, where a person is reading a paper per day. It's called the` morning paper,` and it's Adrianne's caller - a guy who is doing this. And it's really cool because he's following top computer science conferences and he's writing summaries, but these are really amazing summaries of the papers. You get a very technical and sound paper summary, and you have the link to a paper. If you don't have lots of time, you can just read the summary. He's not reviewing just the latest papers, but also is looking at seminar onse. Sometimes he has serious interests in papers that are like from the seventies. And then, you know, there are three, four endings. Like with the latest paper at top computer science conference. This is pretty cool. 
 
Also, something which is inside the Informal and the whole ecosystem around, like with these companies, we have people who are much more active on Twitter or other social media than I am. And then I'm getting a lot of these cool hints. Like what should I read from them. Do you know? So they figured out what paper. So I don't know what this is like, but recently had a colleague who is now co-founding the lazyledger project. Ishmail. You guys may have met. Ishmail is an amazing guy. And so he found a paper which is published by some people from Google on essentially how they are thinking about really using formal verification techniques in everyday social engineering.
 
It's fascinating work and super close to what we are trying to do with informal. Bucky is also a source of amazing blogs on relevant papers. So I'm kind of lazy and I have three daughters, so I don't have a lot of, let's say free time. So I'm sort of lazy and relying on them to tell me, you should look at this, and this is how I pick my reading list. 
 
[00:27:12] Citizen Cosmos: That's interesting because you're not the first researcher who has put it the same way. Obviously, you're not talking about specific papers. You mentioned a specific newsletter, sorry, a mailing list, but this is very similar to what I've heard before as well. 
 
Going back to informal systems and to Bucky. When we had Bucky on the show about five months ago, he talked about his vision for informal systems. How one day it will be used by a large amount of organizations. Minimize the bureaucracy and have some standards in place that can modernize outdated protocols of how organizations work underneath the engine. I think you got the idea. 

What's your personal vision for the work that you guys do in informal systems? Obviously, you mentioned distributed systems and that makes perfect scientific sense.  But what's your, like, great vision for what you do and your colleagues do? 
 
[00:28:08] Zarko: There are several elements here and something I am personally mostly interested in. Just what I'm kind of driving in Informal. Let's say a line of product development and research where we are trying to change the way we develop software. And so this is quite a long-term goal, but we start from the premise that the way we developed software today, it's more art and not a serious engineering discipline. And I think we all know this and there's nothing new there. Now the fundamental question we are trying to answer is how we can do this so that it's better, has a better quality. It's more predictable. 
 
If you think about analogy, we want to design and implement software the way we develop bridges. This is also something analogy, which people mention several times, but it should be sound. It should be correct by construction and not like by chains. And the security audit is more like our short-term way to, let's say, have a meaningful impact on the ecosystem. Trying to contribute our expertise, making software more reliable by finding bugs, and trying to have these formal models which people can use to drive their test suites. So they have kind of the sanity net, a unit individually, they can operate and still be secure. This is like a short-term goal. Like right now, we are changing the way we develop software internally. Trying to help other people. 
 
But if you talk about things like the vision or long-term goal, what I would like to see, and I would not mention, you know, when. But the sooner the better, is that we are using as our normal development tools, something which is more, let's say correctly. And our way to address this is to rely on math. So math is a language. If you want it as a clear rule, it's deterministic. And so we can reason about correctness in that language.
 
And we are trying to use these through formal methods to somehow apply those techniques and tools in our everyday development life. We are, of course, just starting this journey. I don't expect to have like super short-term. But we are trying to do it in a reasonable way. Like we want to improve the development experience, let's say every year, it should be better. We should be able to have tools that are more integrated with the development lifecycle. It's very natural that when we develop software, let's say 20 years from now, I can just put some numbers here. That it's more correct. We decide what we want to do, and we have a certainty that when we finish the process, it stays as a bridge, for, it's almost like sure that there is a bug there. It's just a question of when we find it. And so I think that it's fundamentally wrong. 
 
And so this is more or less like the vision. Of course, they're, you know, Informal and Bucky. Bucky always has plenty of ideas.
 
And so of course, we want you to do something with this correct software. So it's not just about developing the correct software. We all have Informal. We share the same values and we are also trying to allow people to use this software to have let's say, secure platforms for coordination, so that, like, the local economies can be able to do something meaningful for them. And that people could coordinate in a more correct and fast and efficient way. 
 
This is more like, I would say a bit orthogonal. So, to be able to do this, I think our tools, coordination tools, and automation scripts need to be more correct. If we talk about vision, then in my head, we have these two paths. We should ideally cross at some point, like, the end goal is not necessarily having correct software because we are human beings. And like we have needs, which don't necessarily have to do anything with software. Society should be there to help us to simplify the staff, to be more efficient, to be able to do stuff we are not able to do without.
 
So the software on its own is not the end goal. So the goal is to allow people to write out automation scripts in a decentralized way. Let's say some community of people can decide what they want to do together, and they can have trust in the automation script, in a software. They put together that it's correct, that it will respect their values. There would be no way for an individual to take advantage in our evil way. And so to be fair, it will be efficient. So this is more or less the dream. And then right now we don't have tools that will allow us to do this, so we need to develop them. And so like, ideally these two paths will cross at some point, and then we would be able to do something meaningful.
 
[00:32:34] Citizen Cosmos: Is that in line with your personal goals as a researcher this is the vision of the company or the project? Of course, it's a silly question because you already did it, but I will ask it anyways. Is that something that calls within you? 
 
[00:32:50] Zarko: No, it's not a silly question. I think that we are doing this stuff. Let's say our professional life is not necessarily aligned with our values. And I think we are facing this daily, and it's a problem. And not many people can do this. So I'm trying to align these values, and I'm happy, you know, that informal also provides this to people.
 
This is also why they are striving for and informal to provide people with such means that their values should align with the company goals. There is a lot of tension there. Like it's not simple, but, personally, I think that we should somehow really take advantage of the technology, which is, let's say, providing to us or which we developed to do more meaningful stuff.
 
Just, you know, developing digital casinos doesn't seem to be a very meaningful goal. I understand that it's a step, and I accepted that. It's a fine on a trajectory, but if we are not incentivized and motivated to do something more meaningful at the end, then it's probably a waste of time. 
 
[00:33:49] Citizen Cosmos: I have so many questions. I'm a bit lost, but okay. Let's take it in the same direction that we're talking about, and you mentioned spectrums as well and goals and achievements and achieving the greater goal. Would you agree with the sentence that decentralization is a spectrum? So in your opinion, where should future companies strive to be on that spectrum? Does that depend on something that they do? Or should there be a standard that says, okay, all companies should be on that side of the spectrum or companies that do casinos, like you just mentioned, should be on that side of the spectrum or - can be. So how does that work out?
 
[00:34:29] Zarko: I don't have an answer to this question. I think that let's say to be clear what is meant here. I also don't think that we necessarily should have an answer to that question. What we are trying to do is to develop technology, which will enable people to do stuff or to choose a context and a setup, which makes more sense for them.
 
And I think that we don't have this right now. So we are more or less what we provide in terms of computing. Is a model where you more or less have centralized infrastructure services, and then you are sort of, you're trusting them. And then they write their computational model. We have many of these third-party companies, which sort of monopolize different communities and govern them, defining the rules. Because, probably, there's no other way right now, or the other way is not appealing enough. So we need to be more like a rural community. I think people who are working in this decentralized infrastructure, need to be better at coming up with the tools, which will give people the possibility to satisfy their needs.
 
And then I really don't believe that it should be sort of mandatory stuff. I don't really think that everything should be decentralized in the future. There are perfect applications which are perfectly fit centralized settings, and it should still be there. But if some company or some community wants to do something differently, there should be a way to do this. And I think that we are, what we are trying to do, is we are trying to develop tools to enable people to do this. 
 
And what we are also hoping for doing more in the future, with Informal - is connecting with different communities which have such needs, and then try to understand how we can help them.
 
And, of course, we are a group of people. It's like 20 of us, we have personal values and gores. So we are more, maybe something is more appealing at maybe some other domain. And so we might be in the future trying to use technology to let's say, implement some of those applications ourselves. We'll try to do something that makes sense for us. But this is one, let's say one side of the goal.
 
But I think that the impact we would like to make will be better. Definitely. If we are able to engage with other communities where people with the needs and drive to enable them to satisfy their needs. 
 
[00:36:45] Citizen Cosmos: I really like what you're saying there, because for somebody who's spent his last 10 years, and I'm not exaggerating here, on researching distributed ledger technologies, consensus algorithms, and so on and so forth... 
 
The biggest question that I always stumble upon for myself, is how far should decentralization or decentralized spectrums be pushed to the world? Where is the boundary? Where I'm like saying, okay. Be decentralized. But by saying, be decentralized, I am not being decentralized. Right... So honestly, it's great to see that this is a big problem that people are working on. 
 
Were you just going to add something there?
 
[00:37:24] Zarko: No, no, maybe I haven't really understood your question as well, but if you talk about like the scale or how far we can go there, I would also like us to be pragmatic and to say, okay, having 10,000 validators or whatever, for the service running our decentralized application is good enough. We don't know. Like if, you realize that it's not good enough, and there is a usecase where we need to scale to 1 million, I will be super happy to work on this. This will be maybe more academic views on the staff. And I know that some labs are working on this. Let's do gossip protocols, which can scale up to, you know, millions of nodes. You know, why not? But I don't know whether there is an interesting usecase for this right now. 
 
[00:38:04] Citizen Cosmos: It's something that... I mean, consensus algorithms and especially proof of stake and the cons and the pros of delegated proof of stake or selected democracy, as I would like to call it, is a whole topic that I would love to discuss with you again.
 
I think that that's going to take us to a separate show. At least, personally, I have so many things to say on that. And I know I have to ask you not to say, but to ask. I love what you're saying here. And I think that it is something I would definitely want to speak about again. 
 
Which is a different question. Sorry. I went completely off track. So, we're going to try to have some wrap-up questions. The first question is as a researcher into DLTs and somebody who's working with instruments for companies. In your personal opinion or your vision, typical company of the future, what does it look like? What are the differences to today's companies?
 
[00:38:52] Zarko: I think that hopefully, we'll be using more, definitely more and more tools to communicate between us. I feel we will be seeing an explosion of all kinds of communication tools. And we are seeing it recently, like with notion or Rome, and I expect to see more and more stuff for different, more particular, let's say subjects.
 
Okay. Maybe something for like software development, something for different kinds of skills or communities. But I still feel that we are fundamental, we are really not communicating efficiently. It's not about being, you know? Like remote for us, to allow now, what if companies are going remote?
 
It's also probably true for companies, which let's sit in the same room just to talk efficiently and know what you mean. It's in my view, most probably, it's the biggest trouble we have right now. And I somehow expect to see more improvement or death from, I think this is really a step we need to sort of overcome.
 
We need to have a more clean and deterministic way to talk with each other and to have, you know, when I'm saying something, people understand what I mean. And like, there is no way for ambiguity there. That's one thing. The other thing is that also, and this is maybe more of what probably Bucky was talking about.
 
Being able to have a better understanding of the company's state. And I also have a small company where it's like a super small, but even for us, it's always a challenge to figure out, you know, what are our obligations? Are we kind of correct?  The laws are continuously changing and then we, if you talk about more complex companies, which have different operations happening in parts, like, you know - hiring marketing sales, development... And having this stuff in sync and listening, having a socially, being able to understand what's happening and to understand, how good or bad you're doing something, or if you are like from a legal perspective, are we correct or not?
 
I also see a lot of improvement on that front. I don't know whether I sort of answered your question, but... 
 
[00:40:50] Citizen Cosmos: I think you're talking in the direction, which makes sense to me anyways, and you talk about the problem. And from that, I can paint the picture in my head. That answers the question - kind of.
 
So hopefully the companies of the future, the first thing for them is to understand much better than we do today, their own goals, their own motivation, and the communication between how to achieve those things if I understand you correctly. Thanks. It's really great. 
 
And I think Anna, you had a wrapping-up question or like a resume question thee.
 
[00:41:19] Anna: What are the 3 projects you are excited about? It can be projects outside of the Cosmos ecosystem, inside the Cosmos ecosystem, whatever. 
 
[00:41:30] Zarko: Probably it would be more politically correct to mention something outside of Cosmos, but, I think that IBC is really the project, which has, let's say most of my attention right now.
 
I think it's the most probably relevant project in the whole ecosystem because, essentially, IBC will enable us to compose the stuff, let's say to integrate different silos, which are right now individual. And it will teach us so much in the space. Like it's, again, a sort of communication problem. We can go to the next level.
 
We will be able to better integrate, to better coordinate, to exchange values in a more like standard and efficient way. And in that sense, I'm looking forward to seeing not just IBC, of course, like we expect IBC to play an important role there. But in general, like how we can collaborate better between these different, amazing communities and locktrain systems. How we can integrate them and how we can provide society with something more meaningful? Develop a society, more natural, you know, something more interesting and useful. 
 
[00:42:35] Citizen Cosmos: Is there a favorite project within the cosmos ecosystem? Not favorites in terms of how they do, but the idea, maybe something that interests you. You don't have to name one.
 
[00:42:46] Zarko: I’m sort of interested in seeing Cosmos integrative material. So there is a project called Peggy, which should allow us this capability. Let's say that for now. This is something which I think it's really super important. Like just having this bridge between these two communities, I think will bring a lot of good stuff to cosmos and also to material. I'm really excited to see this company. 
 
[00:43:07] Citizen Cosmos: I have a question after the last, which wasn't supposed to be. So would you say that Peggy, in your opinion, is bigger in terms of the possibilities than Ethermint? How is it different?
 
[00:43:21] Zarko: Ethermint it's a super important project. Just Peggy is something that I think it's important, too, in a sense that it allows us this, really, like the first bridging capability. And then once we connect these two systems, then we can we are opening a new space for development and interesting possibilities for each element. It's also a very good example.
 
I think that it will probably, you know, like it will play its space potentially, you know, in some synergy with Peggy, or it could be, you know, it will have its bridge. I don't know what the story is there. We also definitely need, in the Cosmos space, more like smart contracts, like platforms. This is something we are looking forward to and seeing more of, in future. 
 
[00:43:58] Citizen Cosmos: Yeah. Hopefully, that's what we will see - a lot of those bridges, not just a theory of development. I like the vision you guys have in Informal. This is not the first time we are hearing it. It's cool to understand that you guys are keeping that vision. Thanks a lot for your time Zarko, and thanks a lot for sharing your vision your opinions. And I hope we can do this again shortly. I think we really haven't touched more than the tip of the iceberg with what you have to say about algorithms and distributed computing. And I think we would love to hear more and more about it if you have time in the future, of course. 
 
[00:44:38] Zarko: Sure. Of course. Like I would be happy, and I really enjoyed talking with you guys thank you once more for having me here. It was really cool. 
 
[00:44:44] Citizen Cosmos: Thanks, everybody, for joining in, and sees you next time on Citizen Cosmos. Thanks, bye-bye!

------------------------------------------------------------------------------------------------------------------------------------------------------------------
If you want to support us in our mission of creating and spreading educational content and aligning the goal of different communities, please stake with us (guide you can find [here](https://www.citizencosmos.space/staking)) 
- [EVMOS](https://wallet.keplr.app/chains/evmos?modal=validator&chain=evmos_9001-2&validator_address=evmosvaloper1mtwvpdd57gpkyejd566s24afr9zm5ryq8gwpvj) 
- [ATOM](https://wallet.keplr.app/chains/cosmos-hub?modal=validator&chain=cosmoshub-4&validator_address=cosmosvaloper1e859xaue4k2jzqw20cv6l7p3tmc378pc3k8g2u) 
- [BOOT](https://wallet.keplr.app/chains/bostrom?modal=validator&chain=bostrom&validator_address=bostromvaloper1f7nx65pmayfenpfwzwaamwas4ygmvalqj6dz5r)

and join our [Discord server](https://discord.gg/kJaG3EucCX) and help us grow the interest for web3 to the masses.

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fcitizen-cosmos.github.io%2Fblog%2Fzarko20.html&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com) 
