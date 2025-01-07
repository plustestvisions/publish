---
created: 2024-06-24T10:39
updated: 2025-01-06T16:33
tags:
  - EuroSTARConf
  - testing
---
# Summarizing the Euro STAR 2024 Conference in Stockholm


19 juni 2024
The first keynote speaker, [Abigail Cauchi](https://www.linkedin.com/in/abigailcauchi/), summarized #EuroStarConf for me with a single sentence

> “Tech amplifies what already exists (the good and the bad)”

The two dominant themes I followed during the conference the human factor within our testing profession and on the side board searching for some critical thoughts about what effect the current AI hype is having on our testing profession and check if my testing fundamentals are still in place.

## Human factor
So on day 1 I followed a full day workshop on Think like a tester by [Rikard Edgren](../../../../Persons/Rikard Edgren.md)

So how do testers think differently:
we see errors happening as a good thing
we question assumptions on the product
try to understand what happens
fast learning is needed as looking at the complete picture is a lot of information.

As testing happens in your head, you decide what to test and how, you evaluate and communicate the result, so it is your thinking that determines how good your testing will be. 
One of the most important risks about this is bias. As every person has it's own model of his/her reality and so we have different biases on reality. Next to a risk, you could argue that is also a benefit, to see things differently and for sure the more people are looking at reality, and talk and report to each other about their model of reality, we get more information about reality. So you can't avoid bias, but you can handle it by categorizing it
What kind of biases 
- Confirmation bias - we look for confirmation supporting our beliefs
- Availability bias - we explain by recent experiences
- Spectacular Explanation Fallacy - testers tend to believe there is a spectacular explanation to a tricky problem
- Correlation Does Not Prove Causation - relations can have effects in different ways

### Heuristics:
- What if....
	- What would happen if....
- Rule of 3 (Jerry Weinberg)
	- If you can not come up with 3 things that might make the idea bad, you have not thought enough about it
- What you see is all there is (Kahneman)
	- know that there are things that matter you do not know about (yet)
- Question everything, especially this statement
	- testers are skeptical, but within limits

so it is all about questions and follow up questions and act upon the answers
What are you afraid might happen (PO), what part of the code are you unsure of? (DEV), what do you think we should test more (support)
Where do you dig deeper into details? Where you understand more about the reasoning, and what matters...and 

What are signs to be self critical?
Too many problems, Too easy and or bored, fatigue. Act by second opinion other people..

The test Eye:
Wants to see problems, sees many sorts of things, looks at many places, looks often, focus on what's important and has an eye for others

So in professional circle:
distribute 2+2 program and split into groups of 2-3 and let them look for planted bugs 10 of them

### Types of logical thinking
Deductive reasoning-->Based on requirements we know what to expect
Inductive reasoning-->Reproduction of problems are summarized in bug report
Abductive reasoning-->Based on the results of tests we decide to test more

It's ok to be wrong, and we test some more ;-)

Testing can not prove that the software works
Testing can prove that software works
Testing can give examples of situations where the software works
May be it is better to say Testers make their best efforts to falsify then say we are verifying

### Creative thinking
qualifications, cultural diversity, trust, tolerance, humor, discipline, generosity, a sense of community, curiosity, freedom of spirit, small scale, equality-->
how to achieve:
- Mind Mapping,, pair testing, lateral thinking (the opposite0, brain storming)
- free Brolin role-> Swedish soccer player that got a free role from his coach
- serendipity-->luck
- checklist for quality characteristics, cheat sheets, www
- creative environment
- new combinations-->steal ideas, details big picture

Software testing is an empirical, technical and human investigation conducted to provide stakeholders with information about the quality of the product or service under test

## Testing fundamentals

The need to focus on testing fundamentals and the basic testing approaches. These were the highlights from some talks I attended, and they become a good backdrop to put the talks about AI against:

[Michael Bolton](https://www.linkedin.com/in/michael-bolton-08847/) reminded us again what it means to be a tester, what testing is, the skills needed and how we humans differ from machines in his talk _“Futureproofing Testing in the Age of AI”_. The thinking that a skilled tester, the skills and understanding of the human context simply cannot be replicated by and AI today.

These speakers talked about the need to focus on the basic skills, the scientific process and not to get lost in focusing on the tools and new technologies. This is important in today’s AI landscape; Without understanding what good approach to testing is, the AIs won’t be able to amplify the results in a valuable way.

## Can an AI test? Amplification of the not so good

There were plenty of talks about different aspects of AI and of course a lot of that talk was about Large Language Models (LLM) such as ChatGPT. What struck me was that there was a big discrepancy between speakers who understood testing and speakers who lacked deeper knowledge in the testing topic.

An AI can generate as many test cases as you like, you can get thousands of them over night, but if you don’t know what questions to ask to understand how good the test cases are then you won’t have a choice but run all the tests not knowing if they provide any value at all. An even more important question would be if using test cases would be the best approach to test a feature or a product. And how do you certify that the AI understands and take into consideration the human aspect and context? For people we have processes for that but for AI this is still a challenge that needs to be considered.

The same questions apply for AI generated test reports. If you don’t know enough to ask the LLM what browser engine it used for the testing it based its test report on, then you might miss the answer “Oh, I didn’t actual perform any testing with real browser…”. If that test report is then passed along to decision making meetings, then the wrong conclusions could be made leading to bad decisions. The AIs have the power to amplify the good but there is a risk that lack of knowledge is amplified.

## Amplifying the good

I saw two fantastic speakers who demonstrated understanding of software quality and use of AIs. The first speaker was [Adam Tornhill](https://www.linkedin.com/in/adam-tornhill-71759b48/) in his one-day tutorial “Test your Code as a Crime Scene” where he took us through how he built a software that can analyze code using forensic psychology as inspiration. The tool, CodeScene, draws data from the versioning system and the bug-reporting system can build a clear and easy overview of all the files in the project:

- Large files were illustrated as large circles.
- If the files were changed frequently, they were marked as hotspots by turning the colour towards red.
- A map was presented of who had contributed to which files, thus making it possible to pinpoint what the knowledge gap would be if the coder left the project.
- A health score was created by, amongst other metrics, looking at how nested the code was. Code that is difficult for a human to interpret can have a higher risk of introducing errors when that code is changed and therefore gets a lower health score.

All of these findings were also backed by peer reviewed research articles that I found very fascinating to read.

At the end, he gave a quick demo where he let an LLM refactor code. Re-factored code that failed the unit tests (refactoring had lost the initial capability of the code) or had a lower health score was discarded. The remaining 30% of the code had a higher health score that indicated a higher readability for a developer. Since a developer can spend up to 70% of the time understanding code that needs to be changed this is not bad at all since this was automated!

The second great speaker was Benjamin Johnson Ward and his _“Adversarial Testing for AIs: Get Ready to Fuzz Things Up!”_.

He took the audience on a ride through the engineering technicalities in how he tested LLMs in his context and how he utilized them for testing. I liked the engineering approach to limit the problem space that was under test, the number of possible outputs from an LLM are enormous, but you can focus on the outputs that are obviously wrong. When using fuzzing of test data to test the problem space he could find issues with output that for example is an empty string.

Benjamin also covered some optimizations of his process were for example the DOM of a webpage was optimized before sending to the LLM to make sure the limited context window did not overflow. All in all, it was a great system with a mix of different techniques, code and LLM’s that formed a whole.

Both Adam and Benjamin showed how deep knowledge software can be amplified by a good usage of AIs. Without deeper knowledge you will be stuck at doing what the AI suggest and you might be unable to assess the value of the output. AIs won’t replace testers, but the divide between a skilled and unskilled tester will accelerate with them.

## Some of the other great stuff

On the topic of test reporting, I got to listen to [Ezanne Grobler](https://www.linkedin.com/in/ezanne-grobler-26926a12/) and her presentation of _“Testing Metrics: The Good, the Bad and the Ugly”_ and I loved how she divided her test reporting into different dimensions: Product, Project, Process, People, Risk, Coverage and Confidence. It got me to rethink how I perform my reporting to adjust the information, and how it is packaged, so different stakeholders get the information they need.

Right before my own talk I got to listen to [Ina (Radostina) Tsvetkova](https://www.linkedin.com/in/inatsvetkova/) and her talk about “_Manual Accessibility Testing: Why, What, and How”_. It was an eye opener for me regarding how little I knew about the subject of software accessibility. I was amused when she took Eurostar’s own conference site as examples of different kinds of accessibility issues. Everyone in the room had of course looked at the site multiple times but I guess that most people just like me hadn’t an idea how challenging it could be to use for people with an accessibility challenge. Some things seemed easy to address, such as correct headline definition in the html-code and wouldn’t have taken any extra time to implement if the right knowledge is there. Doing accessibility right from the start seems cheap since it can be expensive if it comes as an afterthought, especially when there are laws and regulations that put accessibility requirements on a product.

_“Testing the Gripen E Fighter Aircraft”_ by [Torvald Mårtensson](https://www.linkedin.com/in/torvald-martensson/) was also an interesting talk though maybe it was a little bit disappointing he couldn’t share more interesting issues or failures of the fighter jets but the reason for that is obvious I guess. What was most interesting for me was how they worked with Hardware In the Loop (HIL) rigs in similar fashion as other project I’ve been in. The fighter and its system might a special type of context, but the challenges are the same as in other contexts. If you are interested in fighter jets specifically, I can also recommend the excellent article by House of Tests own [Alexandre Bauduin](https://www.linkedin.com/in/alexandre-bauduin/) called [“Testing Software in Weapons: Challenges and Considerations”](https://www.linkedin.com/pulse/testing-software-weapons-challenges-considerations-alexandre-bauduin-lx5re/?trackingId=K%2B9Bt8TqRJqxwdl1OhehOQ%3D%3D.) (though of course not quite as cool fighters as the JAS 39 Gripen).

  
## The love for the community

I was reminded by [Maria Kedemo](https://www.linkedin.com/in/maria-kedemo-299b16/)s talk _“Why I Left Software Testing – and Why I Came Back”_ why I love the testing community how empowering and developing it has been for me. She shared a lovely story about her journey, her challenges and how she overcame them, all with a colorful presentation illustrated by herself. Though she ventured away from testing for some time she was drawn back to testing.

Myself, I love this community because of the humanity in it in combination with focus on skills, improving oneself and the interesting challenges I face when the human and technological complexity meet. Wherever I went I talked about a wide range of topics with different people such as [Vipin Jain](https://www.linkedin.com/in/alwaystesting/), [Ru Cindrea](https://www.linkedin.com/in/rucindrea/), [Ina (Radostina) Tsvetkova](https://www.linkedin.com/in/inatsvetkova/), [Hristina Koleva](https://www.linkedin.com/in/hriskoleva/), [Michael Bolton](https://www.linkedin.com/in/michael-bolton-08847/), [Mats Olsson](https://www.linkedin.com/in/mats-olsson-2b108b18/) and many more. Everyone eager to meet, talk, discuss and share experiences from the field. It was a positive atmosphere during the conference that was amplified by the fun activities the organizers had planned for us. The highlight was the dinner in the City Hall where the Nobel Prize dinner is held every year. It was fun to get to visit that place and to share this historical place with everyone coming to visit from other countries.

## In summary

Tech amplifies what is already there, the good and the bad. Testers need to focus on learning about different testing approaches, way of thinking and skills to become effective today so they can be amplified by the technology tomorrow. If a tester does not know what questions to ask a AI and cannot asses the quality of the answers, then the AIs won’t amplify the tester nor bring value to the projects.

My final suggestion is to pick up a book about software development and software testing and start reading! If you want tips where to start, I suggest _“Perfect Software: And Other Illusions About Testing”_ by Gerald Weinberg, or _“Jävla skitsystem”_ by [Jonas Söderström](https://www.linkedin.com/in/jonassoderstromkornet/) (unfortunately only available in Swedish).