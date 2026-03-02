# 📝 Notes

Mar 2, 2026

## AI Chat

Invited [eldon@veloaviation.com](mailto:eldon@veloaviation.com) [Reed Garrett](mailto:reed@kingsidegroup.com)

Attachments [AI Chat](https://www.google.com/calendar/event?eid=N2RsbXFsbTFuZmM0MWMwYWg0YTg1NGpqZG4gcmVlZEBraW5nc2lkZWdyb3VwLmNvbQ) 

Meeting records [Transcript](?tab=t.a4z9s8dn80wk) 

### Summary

Eldon Thomas and Reed Garrett discussed their respective AI backgrounds, with Eldon Thomas detailing their challenge in automating RFQ responses due to internal constraints on flexible, manually-managed pricing and difficulties integrating with their locked-down ERP system, Quantum Control, which lacked sufficient APIs for quote entry. Reed Garrett proposed an automation flow using N8N for email triage and RAG agents to interact with Quantum Control APIs, suggesting a human-in-the-loop front-end dashboard to allow colleagues, like Greg, to review and manually approve AI-generated proposals before transmission, thus maintaining human control over final quotes. Eldon Thomas agreed to investigate the current API status for Quantum and Air Exchange, while Reed Garrett offered to focus on designing a simple dashboard front-end, emphasizing the project's courtesy nature and aiming for quick execution.

### Details

* **Introduction and Background**: Eldon Thomas provided background on their experience in the dotcom software sector and involvement with AI, including having four agents running on Open Claw, one of which is deployed and interacts daily with their sales team on Teams ([00:00:00](#00:00:00)). Reed Garrett shared that their day job involves leading the machine learning model portfolio for Verizon's base management and communications, managing predictive analytics and generative AI for their massive marketing organization ([00:02:33](#00:02:33)). Reed Garrett is also involved in a side venture with four others, using AI tools to build automations across various work streams and industries ([00:03:35](#00:03:35)).

* **Current AI Use Case and Challenge (RFQs)**: Eldon Thomas described their current AI application which involves triaging RFQs (Requests for Quotation) that come in, highlighting that they have an agent performing this function and flagging alerts. The primary difficulty is having the agents actually respond back with quotes because of internal constraints; a colleague, Greg, wants the pricing to be flexible, negotiated, and managed manually, meaning parts do not have fixed pricing and the dynamics change daily ([00:04:32](#00:04:32)).

* **System Integration Difficulties (ERP and APIs)**: The RFQs often enter their ERP system, which is hosted on AWS and is locked down, making it challenging to run custom code or agents. Although Eldon Thomas has managed to have AIs navigate the system, the process is clunky due to a lack of good API hooks ([00:06:50](#00:06:50)). Eldon Thomas noted that Quantum Control, their system, did not offer full API access for their database or the ability to write back data to the system as of three months ago, which is what Eldon Thomas needed to automate quote entry ([00:07:51](#00:07:51)).

* **Automation and Process Flow Proposal**: Reed Garrett proposed using N8N (N8N) as a backbone for automations, which can look similar to a process flow chart, starting with a trigger event when an email is received. The process would use a retrieval-augmented generation (RAG) agent to classify the email into categories such as "yes response," "no response," or "human intervention/quote required" ([00:10:23](#00:10:23)). For quote requests, the agent could use function calls or tool requests to interface with Quantum Control's APIs to gather necessary data, like a price summary from recent quotes, to create a proposal ([00:11:29](#00:11:29)) ([00:13:12](#00:13:12)).

* **Proposal for Human-in-the-Loop Dashboard**: Due to the reluctance of the colleague, Greg, to fully turn over quoting to an AI agent, Reed Garrett suggested creating a front-end dashboard ([00:11:29](#00:11:29)) ([00:16:21](#00:16:21)). This dashboard would allow a team member to log in, review the automatically generated proposals, and quickly approve or reject them with a click or toggle switch, maintaining human control over the final quote transmission. Additionally, they discussed the importance of recording a history of all interactions, which N8N is capable of doing, providing a traceable receipt for every email sent ([00:12:23](#00:12:23)) ([00:14:29](#00:14:29)).

* **Next Steps and Project Scope**: Eldon Thomas committed to investigating the current API availability for Quantum and Air Exchange ([00:16:21](#00:16:21)). Reed Garrett offered to treat this project as a courtesy, noting the key focus would be designing the front end of the dashboard and confirming API availability, starting with a "super ugly," simple list for quick execution ([00:17:23](#00:17:23)). The conversation also touched upon the value of Open Claw agents, with Eldon Thomas confirming they have four agents running, including one monitoring sales emails that provides alerts to the sales team on Teams, enabling them to focus only on urgent emails ([00:19:10](#00:19:10)).

### Suggested next steps

- [ ] Eldon Thomas will dig into Quantum and Air Exchange APIs to revisit what is available to work with and what is being opened up, and will circle back to Reed Garrett later today or tomorrow with an update.  
- [ ] Reed Garrett will send the Fig Jam diagram to Eldon Thomas.

*You should review Gemini's notes to make sure they're accurate. [Get tips and learn how Gemini takes notes](https://support.google.com/meet/answer/14754931)*

*Please provide feedback about using Gemini to take notes in a [short survey.](https://google.qualtrics.com/jfe/form/SV_9vK3UZEaIQKKE7A?confid=utpNAxXvf5ykigatvzUVDxIXOAIIigIgABgBCA&detailid=standard)*

# 📖 Transcript

Mar 2, 2026

## AI Chat \- Transcript

### 00:00:00 {#00:00:00}

   
**Eldon Thomas:** How's it going?  
**Reed Garrett:** Good. How are you doing? Can you hear me? Okay.  
**Eldon Thomas:** Yep. I can hear you good.  
**Reed Garrett:** Awesome. Nice to meet you.  
**Eldon Thomas:** You you as well, Reed. Let me um maybe a good maybe let me give you a background so you have an idea of where I'm coming from. It might help help be helpful.  
**Reed Garrett:** Okay.  
**Eldon Thomas:** So I I was early in some of the dotcom stuff back in the day with some software companies. Not a coder, but definitely pretty deeply involved in all that kind of world.  
**Reed Garrett:** Okay.  
**Eldon Thomas:** Enough to be dangerous, enough to tell coders what to do.  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** Um we recently a couple years ago also hired a bunch of developers and had a side project doing um analytics for our business. Um been pretty early in all the AI stuff.  
**Reed Garrett:** Okay.  
**Eldon Thomas:** So pretty deep with cloud code and with codeex. I've got four agents running on Open Claw right now.  
   
 

### 00:02:33 {#00:02:33}

   
**Eldon Thomas:** One that's deployed and interacting with our sales team already on Teams every day. Um,  
**Reed Garrett:** Okay.  
**Eldon Thomas:** so pretty far down some of those rabbit holes. So I just want to make sure I give you context for kind of background of of of where I'm at  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** and and what doing and and so that's that's  
**Reed Garrett:** Okay.  
**Eldon Thomas:** a that's a quick that's a quick brief  
**Reed Garrett:** Okay. Yeah. Awesome. That's super helpful. Um, yeah. And I don't know if if Greg told you much about what I'm doing today is or did  
**Eldon Thomas:** He didn't he didn't bunch AI stuff and I got to talk to you.  
**Reed Garrett:** it.  
**Eldon Thomas:** So that's that's that's the only background I  
**Reed Garrett:** Okay. Okay.  
**Eldon Thomas:** got.  
**Reed Garrett:** So, day job is um I I head up the machine learning model portfolio for all of uh Verizon's base management and communications portfolio. So we're the single largest owner of machine learning models for predictive analytics and you know predictive outputs and things like that.  
   
 

### 00:03:35 {#00:03:35}

   
**Reed Garrett:** And then we also uh my team the other half of my team is generative AI. So we build out the generative AI capabilities and tools for same thing for the Verizon's massive marketing organization. And then side hustle stuff is obviously you saw my email. U I got a group of four others who are building out they're using AI tools to build out um AI automations within a variety of work streams. It's it's funny because we had no specific intention. we just recognized like it could really be in any industry, any any vertical and it's like for the first like six months all we could do is talk to dentists because they were just like please make our front office stuff better because it was just so terrible. Um but yeah, so that's kind of my background but that's like all I do is eat, breathe, sleep, drink, whatever AI. Um because I just it's growing so fast it's incredible what it can do and it's just yeah it's going to change everything.  
**Eldon Thomas:** Yeah,  
**Reed Garrett:** So  
**Eldon Thomas:** it is.  
   
 

### 00:04:32 {#00:04:32}

   
**Eldon Thomas:** It's It's definitely consuming me as well. So, for  
**Reed Garrett:** yeah.  
**Eldon Thomas:** sure.  
**Reed Garrett:** So there a specific topic um that you wanted to kind of chat about or just kind of  
**Eldon Thomas:** No,  
**Reed Garrett:** brainstorm  
**Eldon Thomas:** I think I I think I I I didn't know what Greg had mentioned or if there  
**Reed Garrett:** together.  
**Eldon Thomas:** was some issues or or things he was thinking about or or something that he had heard that that got him excited. So I wasn't I wasn't sure if if there was  
**Reed Garrett:** Yeah. That's  
**Eldon Thomas:** anything that I mean on our side right there's a  
**Reed Garrett:** it.  
**Eldon Thomas:** there there is essentially a flow of RFQS that come in and those need to be triaged  
**Reed Garrett:** Yep.  
**Eldon Thomas:** in some way.  
**Reed Garrett:** Yep.  
**Eldon Thomas:** Relatively straightforward. So, I'd say that's I've got a I've got an agent doing that right now and highlights some alerts. You know, it's that's been very easy and straightforward. I think the harder part is the ability to then respond back and have those agents actually respond back for quotes, which is um not possible right now because of Greg.  
   
 

### 00:05:47

   
**Eldon Thomas:** So we can we can give them he doesn't want to he doesn't want to price anything.  
**Reed Garrett:** Oh, okay. Got it.  
**Eldon Thomas:** He wants to have that price be very flexible and only respond to certain people that he has a chance to think about and look at and negotiate with and and manage that. So, our parts that we have don't have pricing.  
**Reed Garrett:** Got  
**Eldon Thomas:** Very fluid and kind of, huh, who came in and talk to so and so and h go ahead and do them a little higher,  
**Reed Garrett:** it.  
**Eldon Thomas:** a little lower. And sometimes it it prices might go up, but it's a very daily changing dynamic, right? So, in the morning,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** we might see something that changes for the next few hours, how we quote, and then it changes back again.  
**Reed Garrett:** Totally.  
**Eldon Thomas:** So that so that's been that's probably a little tricky um to respond that that is so there's that chunk of stuff that we do which is really around triaging RFQS that come in and  
   
 

### 00:06:50 {#00:06:50}

   
**Reed Garrett:** That's from the arrow exchange, right?  
**Eldon Thomas:** then it's really two different places that  
**Reed Garrett:** Those responses that come back  
**Eldon Thomas:** they come in. So the ones that come in through air exchange are are are extra tricky, right? because they come in through air exchange but then they go right into our ERP system and our EAZ system is pretty locked down and hosted on AWS where you know I can't  
**Reed Garrett:** Mhm.  
**Eldon Thomas:** run anything on there and it's you know so so there's ways around that and I've you know I've gotten AIs to go in and be able to click around and you know log on and do stuff but it's it's clunky and tricky and they don't have any good API hooks into anything just yet. Uh that we've  
**Reed Garrett:** And that was quantum control that didn't have that because I when I did like a preliminary look I thought that quantum  
**Eldon Thomas:** seen  
**Reed Garrett:** control was was I guess generous with APIs once you had like a certain I don't know if it was like a tier or whatever within them but I I thought that's what I read but I could be totally wrong.  
   
 

### 00:07:51 {#00:07:51}

   
**Eldon Thomas:** Yeah. You know, and to be fair, I haven't talked to them in about three months on that. Three months ago, they didn't. And I because I wanted I wanted full API access to my  
**Reed Garrett:** for  
**Eldon Thomas:** database, right? And they're like, oh,  
**Reed Garrett:** sure.  
**Eldon Thomas:** that's yeah, we're not there yet. We don't have that. I'm like, well, what are these APIs that we see? And like, well, that's really for just uploading and downloading a few things. So, they're changing pretty quick, too. you know, I should probably go back in and and and check, but it's but as of about three months ago, because I said, "Hey, just give me the APIs. I'll just do everything myself,  
**Reed Garrett:** For sure.  
**Eldon Thomas:** right?" Um,  
**Reed Garrett:** Right.  
**Eldon Thomas:** and they're like, "No, no, no." And especially it was my big deal was they wouldn't let me write anything back to  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** the system through that API. So, I wanted to grab out and put quote details in, you know, because I can get stuff out a variety of different ways.  
   
 

### 00:08:44

   
**Reed Garrett:** Right. Right.  
**Eldon Thomas:** I can send reports, I can do this, I can do that, and do a variety of different things to get data out. It's the it's the real issue that my guys have is all the effort  
**Reed Garrett:** Yep.  
**Eldon Thomas:** and time it takes to put a quote into the system, right?  
**Reed Garrett:** Yep.  
**Eldon Thomas:** So,  
**Reed Garrett:** Yep.  
**Eldon Thomas:** it's just been a lot of clicks putting things, right? And if I had an automated way to do that,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** it'd be it'd be good. We just had some people at a conference for air exchange 2 and they're still, you know, no one wants to give away the keys.  
**Reed Garrett:** I figured that would be pretty locked down. Was Greg was showing me that. I was like, of all the things you showed me, I'm guessing this is going to be the most locked down.  
**Eldon Thomas:** Yeah, I can I can, you know, get on there and like plug co-work and have it go open it up,  
**Reed Garrett:** So,  
   
 

### 00:09:30

   
**Eldon Thomas:** log in and play around and grab stuff and do stuff, right? It's just at scale, right? It's just it's probably still a little right to have everyone have their own agent  
**Reed Garrett:** yeah. Yeah.  
**Eldon Thomas:** who logs in and goes in and does this and have my my team who's not very technical try to manage desktop with their own cloud code walking in and doing something right. It's like it's probably going to be a little  
**Reed Garrett:** Yeah. Well,  
**Eldon Thomas:** Yeah.  
**Reed Garrett:** actually that was the use case I kind of mapped out and I wasn't sure Elden what your level of familiarity was, but sounds like you and I are kind of on the same wavelength here. I'll tell you the one thing that I thought as I kind of was Greg was kind of sharing with me. Can you can you see my screen now?  
**Eldon Thomas:** Yep.  
**Reed Garrett:** I just threw this together w with with Fig Jam, but this is the flow that I thought and I think a lot of this you probably have already thought through as well.  
   
 

### 00:10:23 {#00:10:23}

   
**Reed Garrett:** We there's times that my company like we'll use NAND. Have you ever looked into NAN for a lot of the like the backbone for automations?  
**Eldon Thomas:** No. What was that  
**Reed Garrett:** It's called N8N.  
**Eldon Thomas:** again?  
**Reed Garrett:** I'll I I'll actually send you this fig jam afterwards. N8 is what it's called.  
**Eldon Thomas:** Yeah. No, I've never heard that.  
**Reed Garrett:** So it's essentially it's really simple and it's it's very like a no code sort of friendly. You basically are creating and it actually kind of looks a lot like this. This right here would be sort of the trigger event, right? So this trigger event here, the automation triggers once that arrow exchange email is received. And at that point you basically create another node in which what I would do like a rag agent, right? the retrieval. I've been to generation agent where you could give it as much context as needed to sort of do some email classification. And when I was kind of looking at some of Greg's emails, and I'm this is probably super reductionist, but it was like there was some stuff that he was like, this is a yes response, this is a no response, and then there's like a we need to have a human intervention or we need to provide a quote kind of response.  
   
 

### 00:11:29 {#00:11:29}

   
**Reed Garrett:** Is that sort of like a fair assessment of sort of  
**Eldon Thomas:** Completely fair.  
**Reed Garrett:** like Exactly.  
**Eldon Thomas:** And it's those human intervention ones that are the tricky ones.  
**Reed Garrett:** And so this is where I think we I would hopefully they're  
**Eldon Thomas:** Yep.  
**Reed Garrett:** I guess they're in the process of making this a little bit more friendly. But some of these like simple quote request or not simple quote requests but some of the quote requests or yes or no questions are things that could be called into quantum control that the rag agent would now be able to obviously do a function call. It could do a tool request. It call upon that API knows which API to use and then it would be able to get a response. Now, I think the thing that I had thought about, and this is because I' done had thought about doing frontends for different people that we've worked with in the past, is I can see why someone like Greg would be a little bit reticent to turn the keys completely over to an AI agent on some of those responses.  
   
 

### 00:12:23 {#00:12:23}

   
**Reed Garrett:** So, instead of it just sort of like automatically doing that, and obviously you would want to get there, right? But it's like you could almost have like a dashboard that someone could log into from your team. We'll just say Greg 100%.  
**Eldon Thomas:** and just clicks right through them and so yes go back  
**Reed Garrett:** And you could just see, hey, here's the proposal. Yes. No. Yes.  
**Eldon Thomas:** to the API call right I mean what I can what I can do is I can I can get everything out of the database very  
**Reed Garrett:** No.  
**Eldon Thomas:** easily put it into a CSV file right essentially it's all the keep stuff right and then I can send emails which I'm doing every day right now just hey just here's when you receive the email just app to append it right and it has all my transactional history, quote history. So, it's not real time, but it's, you know, it can be, you know, relatively close. There's a way around there's a way around that,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** right?  
   
 

### 00:13:12 {#00:13:12}

   
**Eldon Thomas:** So,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** is this actually using an agent at all or is this actually just some coding?  
**Reed Garrett:** This would actually be this would this would at least be one agent. So you you'd have the one agent that would be responsible for discerning the classification or the sentiment of that email, right? And then from there, if that if the decision was like, hey, this is one of those this is a this is a quote request. You could have another agent here or just use the same sort of could just be like a script, right? Go into this is a quote request for this particular skew. Go in and get the data. I think Greg and I had talked about too like taking all the sum of the last I don't know so many months and sort of like giving a giving the agent the opportunity to sort of like hey this was sort of your average would you like to quote this you know based off the last three months right so this this is probably another agent right here Elden that would kind of sit here and kind of manage that determine you know go into the quantum control with the full list of APIs um and knowing like hey this is the skew I need to get this skew this is the price summary for the last quotes and getting all that and then it would basically create that proposal and then write that to like a dashboard because I was just sort of envisioning because Greg was showing me his whole list of emails and a lot  
   
 

### 00:14:29 {#00:14:29}

   
**Reed Garrett:** of them were very templatized which makes it really easy as you've as you've seen right because it's just it's so easy to parse through  
**Eldon Thomas:** Yeah.  
**Reed Garrett:** that because it is so templatized but then it's just like a very quickly at a glance with like almost like a toggle switch yes no yes no and if like hey but just change this one thing and then go ahead and send it and then it could just send all  
**Eldon Thomas:** Yep.  
**Reed Garrett:** those emails super quickly.  
**Eldon Thomas:** Nope. I like that.  
**Reed Garrett:** So,  
**Eldon Thomas:** And then I there's a backend side which is once those emails are sent, they got to record what they  
**Reed Garrett:** and that's another thing. I'm glad you brought that up.  
**Eldon Thomas:** did.  
**Reed Garrett:** This is one of the other areas where like we we find ourselves same thing. There's cloud bots, open clause, there's CL, there's all these fantastic things, but what's great about N8 is it actually can record a history of all of the interactions, right? including logs where something was like failed or you know whatever the case may be.  
   
 

### 00:15:19

   
**Reed Garrett:** But every at the end of every email it's almost like there'll be a receipt. There'll be some sort of like transaction where you can trace it  
**Eldon Thomas:** See at the end just give them a all right you just you just send off 31 emails so  
**Reed Garrett:** back.  
**Eldon Thomas:** here's what you got to go enter back into the system and very easy to do or if we could figure out a way to back  
**Reed Garrett:** That would be ideal,  
**Eldon Thomas:** in.  
**Reed Garrett:** right? It just does it for you.  
**Eldon Thomas:** So the triggering event again here you guys have an email so I'm just monitoring an email um triggering event classifying it if I can respond I respond  
**Reed Garrett:** And this is just an offtheshelf Microsoft Outlook API.  
**Eldon Thomas:** yeah something somewhere right now  
**Reed Garrett:** So that wouldn't be hard.  
**Eldon Thomas:** because every every sales email that comes in right now I'm essentially doing doing this although all I'm doing is saying compare it against this list of 10 companies in these 30 parts and if it's one of those then put a chat in  
   
 

### 00:16:21 {#00:16:21}

   
**Reed Garrett:** Mhm.  
**Eldon Thomas:** teams and say take take care of it right we're just not responding not doing a uh a dashboard um interesting  
**Reed Garrett:** So anyways, that was just sort of my proposal just because I just thought the things that I've kind of found useful too.  
**Eldon Thomas:** Yeah.  
**Reed Garrett:** is like if some stuff's locked down, sounds like you're kind of working your way around that as best you can. That's exactly what I would do. But if you were to give someone who's like, you know, exclusively just responsible for this being a part of their job of like responding to these emails coming through, maybe just sort of like a front-end dashboard so that still gives them some, you know, that human in the loop control as to what goes in and what goes out. That would be sort of the only guess recommendation, but  
**Eldon Thomas:** So, let me do some digging. I need to do some digging on on Quantum and Air Exchange APIs just to see and revisit what I have to work with and what they're opening up to me.  
   
 

### 00:17:23 {#00:17:23}

   
**Eldon Thomas:** Um,  
**Reed Garrett:** Mhm.  
**Eldon Thomas:** broadly speaking, what so if we said, "Hey, let's go put something like this together." What type of a project scope  
**Reed Garrett:** Mhm.  
**Eldon Thomas:** is this and time frame? I  
**Reed Garrett:** Honestly,  
**Eldon Thomas:** mean  
**Reed Garrett:** I would just do this as like a courtesy friendship thing for Greg. I I honestly I it shouldn't be hard, right? Because everything to to what you you've kind of built everything else out. It's just like what is available API wise, right?  
**Eldon Thomas:** got some if I got some APIs that might be good. Yeah.  
**Reed Garrett:** But then it's like designing like I guess the real thought is like okay, how how would you want this front end to look, right? because not obviously Greg is just one person but like so that your whole team could kind of use a similar system and you know what would you want that to look like and so that's the part we could kind of like spend some time thinking about that like what would the front end look like um and then obviously again the back end too what does it do at the  
   
 

### 00:18:15

   
**Eldon Thomas:** And it super ugly to start with, right? It super super simple because I think what you're thinking is exactly it's just literally a list. Here's a bunch of emails. Just click click click click click.  
**Reed Garrett:** Mhm.  
**Eldon Thomas:** If you got to go deal something else and skip it and and so allows them to execute, you know, a high number very quickly.  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** Um, no. Very cool. So,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** you guys are starting firm on kind of on the side to go do integration with companies.  
**Reed Garrett:** So I said the question again. We starting what?  
**Eldon Thomas:** You're starting a firm on the side.  
**Reed Garrett:** Oh yeah.  
**Eldon Thomas:** Go and do this with  
**Reed Garrett:** Yeah. Yeah.  
**Eldon Thomas:** companies.  
**Reed Garrett:** Yeah. It's it's amazing just to see how much there. I mean like I I always tell my team it's like it's not just low hanging fruit. Like this is fruit like on the ground right next to the basket.  
   
 

### 00:19:10 {#00:19:10}

   
**Reed Garrett:** There's just stuff that's just ready to go.  
**Eldon Thomas:** Well, yeah.  
**Reed Garrett:** So  
**Eldon Thomas:** And this is a great example. I can um All right. No, very cool. Let me let's let's let me dig a little bit here today,  
**Reed Garrett:** yeah.  
**Eldon Thomas:** tomorrow, and maybe I'll circle back to you later today once I get a better idea of exactly what I've got available to  
**Reed Garrett:** Yeah, just text me whenever.  
**Eldon Thomas:** me.  
**Reed Garrett:** Happy to happy to help. And I mean I I' I'd be curious to how much you guys are using the open claw agents and things like that too. That's pretty awesome that you guys are doing that because that that's that's the phase I think that a lot of people are going to be reluctant  
**Eldon Thomas:** Yeah. Well,  
**Reed Garrett:** to get into,  
**Eldon Thomas:** that's me.  
**Reed Garrett:** but where it's going. It's it's definitely going there,  
**Eldon Thomas:** Yeah.  
**Reed Garrett:** you  
**Eldon Thomas:** I've got I've got four agents up right now.  
**Reed Garrett:** know.  
**Eldon Thomas:** And one agent is the agent that's doing it's just reading my sales  
   
 

### 00:19:54

   
**Reed Garrett:** That's  
**Eldon Thomas:** email and literally just a simple JSON file that looks at  
**Reed Garrett:** awesome.  
**Eldon Thomas:** that I can update, you know, through Telegram. Hey, add this part. Take this part off.  
**Reed Garrett:** Yep.  
**Eldon Thomas:** It's hooked into my teams. And so my my sales team just gets a chat that says, "Hey, you've got a urgent email. Here's here's why it's urgent. Here why it cost urgent." And then once a week we get a summary. Hey, there was 16 alerts this week.  
**Reed Garrett:** Yeah,  
**Eldon Thomas:** This part for this part these customers hit and and they find that super helpful because now they just don't really look at the sales email unless they get an alert,  
**Reed Garrett:** that's right.  
**Eldon Thomas:** right?  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** There's a lot of lot of junk in there. Air exchange is is is the tricky one that I've been struggling with to do. So, this could be really good for that. I have an agent. It's a radar.  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** I call it radar and it just goes out each day and just looks at key news stuff and I'm training it on me on really around transitions,  
   
 

### 00:20:51

   
**Reed Garrett:** Okay.  
**Eldon Thomas:** airplanes getting parked or any big news and it will just hit me up and then it's trying to keep a record of things so it kind of can track a little bit of I've given it some, you know, type parameters. These are the things I'm looking for and, you know, keep track of.  
**Reed Garrett:** Have you built a a headless browser for some of because I he was look we were talking about some areas where like researching stuff too would be helpful for like stuff that's quoted on air exchange and knowing that they were pretty locked down. I was like well we've made headless browsers for people to do research and stuff like that. Have you guys ever messed around with doing stuff like that?  
**Eldon Thomas:** Well, that's is that's exactly where I'm starting to play now and and learn about right and try because again to go into air exchange to go into uh what's called ILS which is the other big big one we have and see if it not get blocked and and and knocked  
**Reed Garrett:** Yep.  
   
 

### 00:21:42

   
**Reed Garrett:** Yep. Yeah.  
**Eldon Thomas:** off right so I'm you know literally  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** playing with that as we speak and and testing out different things to see if I can get in and make it actually work  
**Reed Garrett:** That's cool.  
**Eldon Thomas:** and not get not get blocked in some  
**Reed Garrett:** For sure.  
**Eldon Thomas:** way.  
**Reed Garrett:** Then you just spin up another one. Make another one. So it's like,  
**Eldon Thomas:** Two factor authentication is,  
**Reed Garrett:** Ah, okay.  
**Eldon Thomas:** you know,  
**Reed Garrett:** Yeah, that makes sense.  
**Eldon Thomas:** is is a bugger that I'm struggling with a little bit, right,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** to get through easily,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** especially when it's all geared to me and texting me, you know,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** codes, right? So that's,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** you know, so you know, if I miss if I miss that and don't get right back to it, right, that I'm getting blocked out. So yeah,  
**Reed Garrett:** Yep.  
**Eldon Thomas:** any ideas on that to get through is, you know, be be interesting.  
   
 

### 00:22:32

   
**Eldon Thomas:** We I'd be certainly curious about that.  
**Reed Garrett:** Are your are your openclaw agents running in the cloud or did you go get like a Mac Mini?  
**Eldon Thomas:** Mac Mini.  
**Reed Garrett:** Yep, that's what I did  
**Eldon Thomas:** I just debated back and forth with native more native to Mac  
**Reed Garrett:** too.  
**Eldon Thomas:** to Mac and stuff and few extra little tools and no great.  
**Reed Garrett:** Yep.  
**Eldon Thomas:** So I just literally got codeex up and had it do had session in and just had it literally do everything and then I going back and forth between Claude and and checking each  
**Reed Garrett:** That's amazing.  
**Eldon Thomas:** other's work, right? Like all right, this is what they just did. What are they missing? Oh yeah,  
**Reed Garrett:** Yeah,  
**Eldon Thomas:** I missed, you know, and so it's good. They cut a lot of little things and it's kept the expenses down. I'm only think I'm hitting about 150 bucks a month right now.  
**Reed Garrett:** that's not bad. That's really not.  
**Eldon Thomas:** No,  
**Reed Garrett:** I was gonna ask you what's your token cost for looking  
   
 

### 00:23:18

   
**Eldon Thomas:** as I I want to Well,  
**Reed Garrett:** like  
**Eldon Thomas:** but I've been, you know, cautious and careful. So now I'm starting to ramp up and, you know, I I could see it getting, you know, more into the two or 300 range is probably running if I really run and start to open up. So, I got another one called uh Max, which is just my personal assistant. So, it's going into my Gmail, my regular account, and my calendar,  
**Reed Garrett:** Mhm.  
**Eldon Thomas:** and flagging stuff and reminding me like, "Hey, is this closed or open? You got you got this coming up.  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** You got that coming up." And so, and that's actually surprisingly been a little helpful because I get so many emails,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** you know, hey, you were supposed to file this. Did you file it? Like, ah, yeah.  
**Reed Garrett:** Yep.  
**Eldon Thomas:** you know,  
**Reed Garrett:** Yep.  
**Eldon Thomas:** figuring out how to get it to be more effective than just a messenger service.  
**Reed Garrett:** Actually doing things for you instead of just  
   
 

### 00:24:12

   
**Eldon Thomas:** I know I can, but I,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** you know, that's always the that's always a dilemma. How you move it to the next stage,  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** you know.  
**Reed Garrett:** How much control do you want to give it access to?  
**Eldon Thomas:** Yeah. Right. Because I'm learning my sales agents, it's I keep telling Greg, Greg, give me a price for everything and I'll have a quote directly. That's it's no problem if you'll just I don't not going to do a price.  
**Reed Garrett:** Yep.  
**Eldon Thomas:** Well, then I can't automate for you, buddy.  
**Reed Garrett:** Yeah, that's  
**Eldon Thomas:** But this is a I I think you know, you've hit on if you can if I could bring everything I have into my  
**Reed Garrett:** Yep.  
**Eldon Thomas:** own dashboard, manage off the dashboard. So, every day they're really just driving off that dashboard and the dashboard can actually pull data in, right, is is the key. And um yeah, I need to go back and just find out what I what I what I could do.  
   
 

### 00:25:03

   
**Reed Garrett:** I think an open claw now that you're saying that too combining those two things like an open claw agent nad is fantastic but I I've had a strong sort of prompting that like I feels like the way this is all going though is instead of instead of like building out these complex you know process maps In some cases, just having Python script to Python script makes a ton of sense. You don't have to use a bunch of tokens and stuff like that. Just let it do its thing. But where you really kind of want like an AI co-pilot to kind of help you do certain things, it's I feel like a claw an open claw agent that's kind of writing to this dashboard itself. Like this is where it kind of plays. It's a sandbox.  
**Eldon Thomas:** Yeah. Well, see it is right.  
**Reed Garrett:** That's a good use case.  
**Eldon Thomas:** Again, for example, on the sales thing, I just had it like, hey, you gota you got to cut the code down, right? How you going to do this?  
   
 

### 00:25:52

   
**Eldon Thomas:** And just iterated and it wrote a few little codes where like I can check all the emails coming in against a list without having to activate an agent, right? That's easy. Like do it, right?  
**Reed Garrett:** Yeah.  
**Eldon Thomas:** There's Yeah, it's nice, right? Because it's got its own email. It's got its own account on Teams and it really does make a few things like that  
**Reed Garrett:** Yep.  
**Eldon Thomas:** easy, right? Where if I wanted to take the wheels off, right, it could send emails out. It could interact with my team on Teams. It could get emails directly and respond if I let it respond, right? And that I think is I would agree.  
**Reed Garrett:** Right.  
**Eldon Thomas:** I think that's where it's going. Opal claw may not be it, right? It'll be interesting to see what he does now that he's gone to open AI and they open it up or tools,  
**Reed Garrett:** Yeah,  
**Eldon Thomas:** but it feels like that's where it's going.  
**Reed Garrett:** I agree totally.  
**Eldon Thomas:** I can just sit there and tell it I I now want to I now want you to do this on team. So what do we got to do? Let's go do it right now.  
**Reed Garrett:** Yep. 100%.  
**Eldon Thomas:** I want So figure out how you're going to respond and and go do it.  
**Reed Garrett:** Yeah. Awesome. It was good. It was good chatting with you. It really was. Okay. Sounds good. Thanks, man.  
   
 

### Transcription ended after 00:27:35

*This editable transcript was computer generated and might contain errors. People can also change the text after it was created.*