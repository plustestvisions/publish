---
created: 2024-06-07T16:07
updated: 2024-09-17T12:41
excalidraw-plugin: parsed
excalidraw-open-md: true
tags:
  - excalidraw
  - testing
  - checklist
  - quality_engineering
title: Software Characteristics FRC
Week: "38"
Month: "09"
Year: "2024"
sticker: emoji//1f9ea
banner: Planon/_resources/635638d090bc27a2e80eae7821d5c5b6.png
---

### Capability 
Can the product perform valuable functions? The set of bigger and smaller things you can accomplish with the software. This is usually covered by requirements or similar, and with the addition of some help from developers telling about small or hidden features, you can cover this with thorough and hard work. I suspect some test efforts stop here.
The most lightweight testing approach is to ignore this totally, it has been considered by others, and you will cover parts in more interesting ways when performing other testing.
- Completeness: all important functions wanted by end users are available.-->CSE Voting system; other CSE is not working due to capacity/responsibility issue, also requests by other teams are difficult to achieve-->during testing tester discuss with PO about possible small improvements and try to see the complete picture. For our domain that is not easy by default. Risk here we are depending on our PO and lead developer, but see that even these very Planon experienced persons do not oversee everything
- Accuracy: any output or calculation in the product is correct and presented with significant digit--> As Planon is very customer oriented and has solution teams that have the liberty to make decisions about this we see that different rounding types are used, making it almost impossible to consistently check if something is correct or not. From our generic perspective only 1 method would make maintaining framework easier and the risk of different perspectives and confusion for customers  less. Also you could consider that financial perspective is not happy working with different rounding types. Example: While working on https://planon.atlassian.net/browse/FRC-3010?focusedCommentId=342674 we discovered we use different types of rounding in the UI. So the UI is using Round Even method, and Money fields use Round up. In the database we use big decimals with length 28 and 14 after the comma, when a number is entered having more then 14 after the comma, we also use Round Up method. The UI restricts input to 2 or 3 after the comma, so only issues occur when importing/uploading via other services like SDIM/EnterpriseTalk and API/TMS. As we lack knowledge and information on how other teams (financial) are using this and we see different solutions it is difficult to say we are responsible. From our perspective: just have 1 rounding rule and 1 default way of represent results from calculations makes it generic better maintainable. Currently it is definitely not. Also the concept of calculated fields is causing confusion for customers, as they see a field and think it is stored, but actually it is not stored, so it is not easy to get that in to the report concept.
- Efficiency: performs its actions in an efficient manner (without doing what it’s not supposed to do.)???? Lately we noticed that our QF testing tools makes certain parts of our application very slow (opening tsi field definer, layoutmanager). So we did some extensive checks together with team DS, but no conclusive reason is found. A likely candidate is the element list on the ever growing list of BO's is not paged, but here again, to convince PM/PO we need proof for this, and that takes time, that is only spend in rare occasions. If team is less occupied fixing customer related stuff, this could be one of the first efforts to achieve a lot of resource time of lots of tests and also customer would notice considerable improvements in responsiveness. But this is not a simple change and certainly will have unexpected and unwanted impact on solutions and or customers.
- Interoperability: different features interact with each other in the best way.-->As Planon is a highly integrated box of tools that can be configured in many different manners and we want solution teams to use the tools as flexible as possible, this makes working from the generic perspective very difficult and sometimes it seems that a part is not generic anymore, but still is in our responsibility. So impact analysis is difficult, so risk is that we are overlooking some dependency or featured solution, creating extra work, as culture states you broke it, you fix it. Also her allowing other teams to work in framework terretory makes it very difficult to feel responsible for works done by others not focusing on generic aspects. As impact analysis in code base is not using tools, it becomes more and more impossible to know what is interacting with each other. All teams created confluence pages to identify dependencies with other teams, as framework you can state we are in the middle of that web.
- Concurrency: ability to perform multiple parallel tasks, and run at the same time as other processes.--> due to larger customers the load on the system increases, as we also limit resources on cloud for financial reasons and limited knowledge on parallel testing tools, and also lacking clear requirements for different scenario's makes it very difficult to and less appealing to deep dive in to this. From framework perspective we lack real life scenario's and risk analysis is not possible without extensive collaboration with other teams. 
- Data agnosticism: supports all possible data formats, and handles noise.-->recently we had an issue on special characters in other languages like in French "Français"  or German see ![[2024-08-22#FRC-3241 Description of "Français" is wrongly spelled]]
- Extendibility: ability for customers or 3rd parties to add features or change behavior.-->API heritance of former API team, we lack good documentation and knowledge transfer, we decided to accept learning curve while fixing incoming issues, but that currently bites hard focusing on customer calls and upgrading libraries on this moment. May be creating apps using PAAP is a good way in learning this, but still your are developing software, so still this is a complete developers party from that perspective. As we open doors to existing stuff in our framework for APP developers and TMS consultants testing is limited to checking if the door is open and modules can be used, but for that part only PAAP Ide is available, so joint effort is needed with developers, but limited as we lack developer skills and they are the end users after all.  
### Reliability
Can you trust the product in many and difficult situations? Does the product work well all the time?
- Stability: the product shouldn’t cause crashes, unhandled exceptions or script errors.-->incoming customer calls will be picked up asap, but system starts crashing also due to extended usage from 3rd party implementations API being used with more data then what is expected/tested/checked and no restrictions in place.
- Robustness: the product handles foreseen and unforeseen errors gracefully.-->mostly yes see previous bullet too
- Stress handling: how does the system cope when exceeding various limits?-->see previous bullet, as performance is very expensive and knowledge specific we are struggling company wide, also something we like to forget being to busy with this. As it is a complex system, and most risk in msql statements versus database and mostly only 1 database for customer so load on that part of the environment is notorious for performance and limits. As we do not like to restrict our customers, we do not restrict at all it seems. Also the increasing number of customers with increasing data sizes on a system that is designed for smaller customer needs seems to be a risk waiting for us as Planon. Now it is just random issue solving, focusing to solve customer specific issues; mostly very expensive in time and people as multiple teams are needed for specific knowledge.
- Recoverability: it is possible to recover and continue using the product after a fatal error->Cloud team is improving our backup service, also file storage has our attention so that it is not on the application or webserver, so backup time is reduced and recovering data is less tricky
- Data Integrity: all types of data remain intact throughout the product.-->challenge/risk now we more and more allow external systems to enter data to our system, together with no restrictions on this like mentioned earlier this makes more focus on this necessary. Via UI this risk is limited as we use restrictions on input fields, like rounding is max 3 behind the comma
- Safety: the product will not be part of damaging people or possessions.-->We are not having a product/system that directly endangers peoples health
- Disaster Recovery: what if something really, really bad happens?-->as we are driven by very positive minded sales oriented people looking at revenues only, I doubt there is enough in place for this, but that is an assumption. See cloud backup improvements and object store solution in development for file storage and more agile backups
- Trustworthiness: is the product’s behavior consistent, predictable, and trustworthy?-->For now I think the major part of our application is behaving consistent and predictable, trustworthy, improving on WCAG will improve on specific area, but also makes UI experience more consistent, but easy to maintain is a big challenge as we use and rely to much on css that is not very suitable to maintain our scenario's
### Usability
Is the product easy to use?
- Affordance: product invites to discover possibilities of the product.-->huge learning curve with some hints to use it more easy, but I think we are not inviting people to discover stuff, may be new customers are by default, but as it is highly configurable and not that easy to understand configuration it is a technical driven application. For regular daily users I think we have an agreeable solution, but not to discover other possibilities
- Intuitiveness: it is easy to understand and explain what the product can do.-->nope flexible configuration for multiple area's of customers, makes it difficult to explain, but we have solution teams and specialist facing the market. For framework team this is almost not visible and we are lacking that information to explore these scenario's. Yes I as a teste are allowed to visit and talk to front people, but not for to long as during sprint or multiple sprints this affects our teams velocity and looking at our new goals that is not really realistic
- Minimalism: there is nothing redundant about the product’s content or appearance.-->Depends on configuration, but I guess this true for most scenarios
- Learnability: it is fast and easy to learn how to use the product.-->not at all
- Memorability: once you have learnt how to do something you don’t forget it.-->limited true as you need to know to many exceptions and may stuff to actually finding the correct configuration for you. Then depending on the users of the system and how many times the customer changes configuration you can use it as is. But the risk for Framework is that we are not aware of how the user/customer configures their system and also not how to use it.
- Discoverability: the product’s information and capabilities can be discovered by exploration of the user interface.-->see bullet 1
- Operability: an experienced user can perform common actions very fast.-->yes I think so, but assuming that this will take years for configuration, but daily users of PSS forms can use them very fast as they are designed for that, daily users of web ui depending on the bo and experience of the the user.
- Interactivity: the product has easy-to-understand states and possibilities of interacting with the application (via GUI or API).-->GUI depending on configuration for API do not know, may be for TMS consultants to decide or APP developers. As our framework teams lack real knowledge on API's and learn by fixing issues we can not make a statement on that. Only that we see documentation by API team is not that to clear for us. From API teams perspective I guess when daily working with this topic it was clear for them at that time, but no cooperation with the teams that will be responsible for maintaining them.
- Control: the user should feel in control over the proceedings of the software.-->due to massive configurability and high learning curve having control is depending on both configuration and learning capacity
- Clarity: is everything stated explicitly and in detail, with a language that can be understood, leaving no room for doubt?-->Graphos is in control, customer facing departments are too, we as framework we can not tell
- Errors: there are informative error messages, difficult to make mistakes and easy to repair after making them.-->the logging is massive and is restricted and is not keeping track of every user action or api action (assumption)
- Consistency: behavior is the same throughout the product, and there is one look & feel.-->Mostly true for web ui, but for PSS this can not be stated as this can be configured in many manners, but the elements are highly the same
- Tailor ability: default settings and behavior can be specified for flexibility.-->highly true by configuration
- Accessibility: the product is possible to use for as many people as possible, and meets applicable accessibility standards.--> improving in progress WCAG focus
- Documentation: there is a Help that helps, and matches the functionality.-->complex product configuration so huge help available, maintained by graphos with technical input from development teams, including framework.
### Charisma
Does the product have 'it'
- Uniqueness: the product is distinguishable and has something no one else has.-->Framework does not have any clue's on this.
- Satisfaction: how do you feel after using the product?-->as a tester I think most of time it is boring, the most exiting part is always how to configure the product to see behavior that is specified.
- Professionalism: does the product have the appropriate flair of professionalism and feel fit for purpose?-->I think it has, but do not know the perspective of customers. Talking to consultants and commercial people, they do not have a lot of trouble selling it and make it fit for use.
- Attractiveness: are all types of aspects of the product appealing to eyes and other senses?-->majority is not, CAD drawings and dashboards and graphical representations are appealing.
- Curiosity: will users get interested and try out what they can do with the product?-->again as framework we do not have any clues on this
- Entrancement: do users get hooked, have fun, in a flow, and fully engaged when using the product?-->again as framework we do not have any clues on this
- Hype: should the product use the latest and greatest technologies/ideas?-->we are not very fast in adapting stuff, and I think that is a good safety practice. Exploring AI and looking at Micro front ends-->but not by framework team due to focus on customer calls and library upgrades.
- Expectancy: the product exceeds expectations and meets the needs you didn't know you had.-->again as framework we do not have any clues on this, it does for our own expectations but what is the value of that?
- Attitude: do the product and its information have the right attitude and speak to you with the right language and style? I think we have to many warnings and messages that are shown to user after an invalid input, also user must click a lot
- Directness: are (first) impressions impressive?-->in possible configuration options we can imagine yes, about using it yes impressive as learning curve is steep
- Story: are there compelling stories about the product’s inception, construction or usage?
### Security
Does the product protect against unwanted usage? 
- Authentication: the product’s identifications of the users.-->not directly in our team, TEC team is looking at oauth and keycloak
- Authorization: the product’s handling of what an authenticated user can see and do.-->as Planon uses a non typical authorization design, it raises lots of questions for customers.
- Privacy: ability to not disclose data that is protected to unauthorized users.-->is possible but needs improvement, but not quickly due to other prio's PM
- Security holes: product should not invite to social engineering vulnerabilities.-->increasing amount of security calls coming in, since we have a security team checking pen test results and veracode is used.
- Secrecy: the product should under no circumstances disclose information about the underlying systems.-->does not have our focus as we lack knowledge in this area and fully rely on security team
- Invulnerability: ability to withstand penetration attempts.-->rely on security teams effort
- Virus-free: product will not transport virus, or appear as one..-->rely on security teams effort
- Piracy Resistance: no possibility to illegally copy and distribute the software or code..-->rely on security teams effort
- Compliance: security standards the product adheres to..-->rely on security teams effort
### Performance
Is the product fast enough? 
- Capacity: the many limits of the product, for different circumstances (e.g. slow network.)-->query to database is highest risks and have attention of our developer, but depending to much on 1 senior here, as developers are not always database experts or query experts, also our product is creating very complex queries on the fly, so also here learning curve is high. Sometime we feel as non-framework teams do not understand the generic concept, it is far to complex and only few know how it is working exactly
- Resource Utilization: appropriate usage of memory, storage and other resources.-->rely on other teams that have that information, so again we react to incoming issues as we lack this kind of information from customers and if it is available we lack knowledge how to understand and change that. When focusing we learn, but it only has focus when customer calls come in.
- Responsiveness: the speed of which an action is (perceived as) performed.-->depending on customer and configuration it is difficult to state what is acceptable, and due to other priorities this is not getting real serious attention until customer call is coming in.
- Availability: the system is available for use when it should be.-->cloud team is responsible for this
- Throughput: the products ability to process many, many things.-->risk is increasing as it is designed as a UI driven system, but more and more external non UI driven scenario's are created that have increasing amount of things happening in the system. As most of these things are done using api's that we did not developed our selves and where it is not clearly stated what requirements on this should be, and no restrictions are build in, here a big risk is waiting for all of Planon. We have a performance A team, but this is only having people that are mainly focused and dedicated to their product team. So not really a daily focus.
- Endurance: can the product handle load for a long time?-->risk is increasing as it is designed as a UI driven system, but more and more external non UI driven scenario's are created that have increasing amount of things happening in the system. As most of these things are done using api's that we did not developed our selves and where it is not clearly stated what requirements on this should be, and no restrictions are build in, here a big risk is waiting for all of Planon 
- Feedback: is the feedback from the system on user actions appropriate?-->too extensive as our system is kept as flexible as possible to serve all kinds of scenario's and restrictions are scarcely used. So most of the time we can only warn the user for possible effects.
- Scalability: how well does the product scale up, out or down?-->some have been taken multiple web and app servers, but not really in control of the framework, also depends on cloud and tec team knowledge

### IT-ibility
Is the product easy to install, maintain and support
- System requirements: ability to run on supported configurations, and handle different environments or missing components
- Install ability: product can be installed on intended platforms with appropriate footprint
- Upgrades: ease of upgrading to a newer version without loss of configuration and settings-->is possible, but not easy to maintain->upgrading is causing lots of issues that are not always due to framework changes, seems also too complex for other teams
- Uninstallation: are all files (except user’s or system files) and other resources removed when uninstalling?-->no clue about that-->not for framework, but TEC team
- Configuration: can the installation be configured in various ways or places to support customer’s usage?-->yes for sure
- Deploy ability: product can be rolled-out by IT department to different types of (restricted) users and environments-->yes
- Maintainability: are the product and its artifacts easy to maintain and support for customers?-->no as configuration is that complex and have that much flexibility Planon is not easy to maintain, also a lot of legacy parts where knowledge is lacking, and also lot's of code we do not know if it is used by customers
- Testability: how effectively can the deployed product be tested by the customer?-->mostly a Planon consultant configures the product for the customer, then customer can choose for learning how to work with the product or just do it them selves. Next to that consultant can make TMS solutions using API's. For us it is always challenging when issues are related to TMS, as we lack information about what the purpose of the tms is, we only receive code, logging, but never functional specifications. This is very time consuming and is not very testable either as we lack knowledge and risks for the specific customer, so I guess a consultant from Planon can do that better, but have no clue on how they work
- 
### Compatibility
How well does the product interact with software and environments?
- Hardware Compatibility: the product can be used with applicable configurations of hardware components.-->no in our domain, but we always check for cloud environment as most of our customers use this and there we have almost no issues. On premise customers however can use oracle db too and you never know what hardware is used. So that is difficult and takes more effort for framework to check
- Operating System Compatibility: the product can run on intended operating system versions, and follows typical behavior.-->other teams are working on it to get our software working on linux too, but we are lacking knowledge and tools to check
- Application Compatibility: the product, and its data, works with other applications customers are likely to use.-->API's and other tools; see previous remarks on API's and TMS and performance for risks
- Configuration Compatibility: product’s ability to blend in with configurations of the environment.-->no idea
- Backward Compatibility: can the product do everything the last version could?-->that is the intention, but we can not know for sure as we are not aware of all customers configurations and how they use the system.
- Forward Compatibility: will the product be able to use artifacts or interfaces of future versions?-->no idea
- Sustainability: effects on the environment, e.g. energy efficiency, switch-offs, power-saving modes, telecommuting-->no idea.
- Standards Conformance: the product conforms to applicable standards, regulations, laws or ethics.-->sustainability (not yet), accessibility WCAG; security; GDPR. Is also a burden for framework, as WCAG project proofs we need to learn on it, GDPR is done by other team so only our product owner knows about it, team does not know what legally is needed. So we depend on PO completely, also the current implementation seems very confusing and also sets limits customers do not like. 
### Supportability. 
Can customers’ usage and problems be supported?
- Identifiers: is it easy to identify parts of the product and their versions, or specific errors?-->logging is not that good, Planon talks about products in jira, but technically we talk another language and in a non consistent manner, so that means a high learning curve for newbies but also for oldies it is confusing.
- Diagnostics: is it possible to find out details regarding customer situations?-->difficult as we depend on support
- Trouble shootable: is it easy to pinpoint errors (e.g. log files) and get help?-->sometimes depends on what.
- Debugging: can you observe the internal states of the software when needed?-->developer can mostly use debug, and in exceptional cases it is possible in customer environments too-->but we can not control this as framework team
- Versatility: ability to use the product in more ways than it was originally designed for.-->due to flexible configuration this is certainly true, but this is conflicting with maintainability
### Testability. 
Is it easy to check and test the product?
- Traceability: the product logs actions at appropriate levels and in usable format-->no lot's of exceptions, and lots of technical things that help developers, but functional usage in UI or API is not logged as it is regarded to expensive on cloud storage somehow
- Controllability: ability to independently set states, objects or variables-->junit testing and selenium testing have more control on this, but requires developers guidance strongly.
- Observability: ability to observe things that should be tested-->no cumbersome as impact analysis is only based on experience of engineers
- Monitorability: can the product give hints on what/how it is doing?-->yes but out of our control, we rely on other teams for this information and is highly controlled by process and regulations
- Isolate ability: ability to test a part by itself-->developers can, but this does not check for impact in other parts. So framework is to big to have complete overview and next to that we are expected to consider specific solutions by other teams and tms.
- Stability: changes to the software are controlled, and not too frequent.-->daily changes to software by multiple teams with different purposes are controlled by team city build street mostly and relying heavily on thousands of automated checks
- Automation: are there public or hidden programmatic interface that can be used?-->yes we can create automated checks
- Information: ability for testers to learn what needs to be learned...-->confluence should be leading, but for legacy only extract from caliber is available, but big parts are lost. As the system is complex and we are adding new stuff daily the learning curve is very long and increases. And documentation is one of the first things by default that is skipped when teams feel pressure of any kind. In framework we have enough engineers who are aware that documentation is important and are working on this on daily basis; but for newbies this is difficult
- Auditability: can the product and its creation be validated?-->yes but not always as there are lots of exceptions and we do not know them all.
### Maintainability. 
Can the product be maintained and extended at low cost?
- Flexibility: the ability to change the product as required by customers-->highly configurable, but also needs lots of experience
- Extensibility: will it be easy to add features in the future?-->seems so
- Simplicity: the code is not more complex than needed, and does not obscure test design, execution and evaluation.-->nope see remarks on exceptions, legacy. Also the fact that solution teams are able to directly change code in what is framework makes it a hell of a job, so simple, nope it is certainly not.
- Readability: the code is adequately documented and easy to read and understand.-->nope large parts are not, legacy for sure is not, but as the organization only looks ahead and not back cleaning up code is done on the fly but has not the highest prio.
- Transparency: Is it easy to understand the underlying structures?-->architectural overviews are lacking also difficult to get that overview as architects belong to teams with separate goals and amount of pressure, so they are first looking at that and when possible to the whole picture, but not on daily basis.
- Modularity: the code is split into manageable pieces-->yes but still every team can change all over the place also in other domains, so that has an effect on maintainability
- Refactorability: are you satisfied with the unit tests?--> real units are considered to be dangerous for build time, so are not used a lot, so we rely heavily on junit integration test, and we have that many it lacks an real overview what is covered and why.
- Analyzability: ability to find causes for defects or other code of interest-->difficult, no impact analysis tool, relying on experienced developers
### Portability. 
Is transferring of the product to different environments enabled?
- Reusability: can parts of the product be re-used elsewhere?-->yes
- Adaptability: is it easy to change the product to support a different environment?-->not easy but we support cloud, on premise also oracle and working on Linux too-->but not by our teams
- Compatibility: does the product comply with common interfaces or official standards?-->we rely mostly on Planons interpretation of standards, now working on WCAG
- Internationalization: it is easy to translate the product-->we have the tools to maintain translations, but changes are needed is also partly too technical process. 
- Localization: are all parts of the product adjusted to meet the needs of the targeted culture/country?-->Most of it yes, but not multi currency complete
- User Interface-robustness: will the product look equally good when translated?-->yes, but due to way we use wicket and rely heavily on CSS makes the UI vulnerable for any kind of change




%%
# Text Elements
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.1.4",
	"elements": [
		{
			"type": "rectangle",
			"version": 55,
			"versionNonce": 1708554334,
			"isDeleted": false,
			"id": "QU2KmpA3h179tZp78nU-y",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -190,
			"y": -283.21875,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 422,
			"height": 290,
			"seed": 543369950,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1714398302016,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 8,
			"versionNonce": 1358606366,
			"isDeleted": true,
			"id": "tdmDjerI",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 62,
			"y": -116.71875,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 10,
			"height": 25,
			"seed": 1597929694,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1714399189633,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "",
			"rawText": "",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.25
		},
		{
			"id": "9DoHPD2p",
			"type": "text",
			"x": 77,
			"y": -108.828125,
			"width": 10,
			"height": 25,
			"angle": 0,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"fillStyle": "solid",
			"strokeWidth": 2,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"seed": 1489543234,
			"version": 2,
			"versionNonce": 1282060574,
			"isDeleted": true,
			"boundElements": null,
			"updated": 1714399193984,
			"link": null,
			"locked": false,
			"text": "",
			"rawText": "",
			"fontSize": 20,
			"fontFamily": 1,
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "",
			"lineHeight": 1.25
		}
	],
	"appState": {
		"theme": "light",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#1e1e1e",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "solid",
		"currentItemStrokeWidth": 2,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 20,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 297.5,
		"scrollY": 369.109375,
		"zoom": {
			"value": 2
		},
		"currentItemRoundness": "round",
		"gridSize": null,
		"gridColor": {
			"Bold": "#C9C9C9FF",
			"Regular": "#EDEDEDFF"
		},
		"currentStrokeOptions": null,
		"previousGridSize": null,
		"frameRendering": {
			"enabled": true,
			"clip": true,
			"name": true,
			"outline": true
		}
	},
	"files": {}
}
```
%%
