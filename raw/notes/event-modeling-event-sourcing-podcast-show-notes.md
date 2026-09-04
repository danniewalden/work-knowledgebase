---
source_url: https://podcast.eventmodeling.org/ (episodes + https://podcast.eventmodeling.org/index.xml)
title: "The Event Modeling and Event Sourcing Podcast — show notes, episodes 1–46"
author: Adam Dymitruk, Martin Dilger
publication: The Event Modeling and Event Sourcing Podcast
published: 2024-11-04 to 2026-04-27
retrieved: 2026-06-17
type: note
---

CAPTURE NOTE (not part of the source): Dannie asked to transcribe the podcast's
YouTube videos and ingest them. Full transcripts could not be retrieved — YouTube's
bot-protection (proof-of-origin token) blocked transcript access from the automated
browser session (transcript API → `failedPrecondition`; the on-page transcript panel
hangs on a spinner; direct caption fetch returns empty), and the sandbox cannot reach
YouTube or the podcast MP3s (network allowlist). The richest available text substitute
is the published **show notes**, captured verbatim below. Episodes **32–46** come from
the RSS feed (`index.xml`) and carry an AI-generated Summary plus a timestamped Chapters
list; episodes **1–31** come from each episode page and carry shorter notes (the show
adopted the longer Summary/Chapters format around late 2025). Each video is reachable
from its episode page (which embeds the YouTube player) and from the channel playlist
<https://www.youtube.com/playlist?list=PLYNJUeYuZDAP0luNOf5MZAbnzPWRCnZyp>.

Host sites/links recurring across episodes: Adam Dymitruk — adaptechgroup.com;
Martin Dilger — nebulit.de; book — leanpub.com/eventmodeling-and-eventsourcing;
method — eventmodeling.org; podcast — podcast.eventmodeling.org.

---

# The Event Modeling and Event Sourcing Podcast — Episodes 1–46

A weekly podcast hosted by **Adam Dymitruk** and **Martin Dilger** on Event Modeling and
Event Sourcing. First episode 2024-11-04; "Season Two" begins at Episode 23 (2025-11-08).

## Episode 1 — Destroying the Aggregate
2024-11-04 · https://www.youtube.com/watch?v=L9FSmSaQWuQ

In this episode of the Event Modeling and Event Sourcing Podcast, Adam Dymitruk and Martin Dilger introduce the podcast and where the topics will come from in the future episodes. The debut of Martin's book at #2 on LeanPub is discussed and why it's such a draw to people in the industry. A discussion of breaking the Domain Driven Design Aggregate pattern is what the show ends with and sets up the next episode to begin with a discussion on Behaviour Driven Design tests for automation steps in Event Modeling and Event Sourcing.

## Episode 2 — Destroying the Aggregate part 2 and more
2024-11-13 · https://www.youtube.com/watch?v=EUydf8OdNDc

This episode's topics: Privacy issues with Event Sourcing like GDPR or Right to be Forgotten; Given When Then / Arrange Act Assert / Specifications by Example / Behaviour Driven Development; Source Control and Event Sourcing comparing Branch Per Feature and Trunk Based Development; Continuation of Destroying the Aggregate from Domain Driven Design.

## Episode 3 — AI, GWTs on a timeline, Security in Event Sourcing
2024-11-17 · https://www.youtube.com/watch?v=uX4_03cbJtU

In this episode Adam and Martin discuss: generating event sourcing code from an event model using AI; a new format for GWTs that use their own timeline; security in event sourcing.

## Episode 4 — Keeping things simple
2024-11-26 · https://www.youtube.com/watch?v=EOPh8rTg_dA

In this episode we discuss: Command - Event - State; Removing Sagas.

## Episode 5 — A Case Against Upcasters
2024-12-01 · https://www.youtube.com/watch?v=W7mpfjW7nhw

In this episode Adam and Martin recap the Workshop from November 30th and talk about the different topics that were brought up. This includes not using upcasters in event sourcing thanks to Yordis Prieto, keeping things simple, the discipline it takes to unlearn old lessons and not reuse any models across the workflows in your system, how this negatively affects coupling and other topics.

## Episode 6 — Event Modeling Scope and more
2024-12-10 · https://www.youtube.com/watch?v=JZWHv-V7Xeg

Topics: gdpr; security; event upcasters; identifiers in EM; reservation pattern; complexity in command handlers; multiple events from a command; scope for event modeling; reusing read models.

## Episode 7 — Pure Command Handlers and Sparse Timelines for GWTs
2024-12-18 · https://www.youtube.com/watch?v=F02n6qntPAA

We discuss keeping command handlers as pure functions, and using timelines to define GWT specifications.

## Episode 8 — Event Sourcing Frameworks and more
2025-01-10 · https://www.youtube.com/watch?v=e_IzVh15unc

In this episode we discuss event sourcing frameworks, fake events and refining testing. #EventModeling #cqrs #dddesign

## Episode 9 — Maintaining Event Models and More
2025-01-13 · https://www.youtube.com/watch?v=uUVHR75ORl4

In this episode we talk about the changes that occur early on in Event Modeling as well as lookups for state views and an Event Modeling future in the eyes of Agile founders.

## Episode 10 — Avoiding the Patterns Soup and more
2025-01-22 · https://www.youtube.com/watch?v=-m9hXz_wQXk

In this episode we cover Todo list complexity and how Event Modeling takes care of backlog grooming. (link discussed: no-kill-switch.ghost.io/the-secrets-of-an-effective-grooming/)

## Episode 11 — No Code Reviews and less
2025-01-28 · https://www.youtube.com/watch?v=D84blR0TVno

In this episode we discuss why code reviews can be very bad, accepting all pull requests and how to think about aggregates in domain driven design. (Collective Code Construction Contract: rfc.zeromq.org/spec/42/)

## Episode 12 — Slice, slice baby!
2025-02-06

In this episode we cover what makes a slice so special in Event Modeling and Event Sourcing. We also discuss how to tackle legacy systems without drowning in the old messy code. And the last topic is error handling in event sourced solutions. All resource links can be found at eventmodeling.org

## Episode 13 — Stop. Collaborate and Listen!
2025-02-12 · https://www.youtube.com/watch?v=7MPi2PqTuME

In this episode Adam Dymitruk and Martin Dilger discuss: guiding event modeling in an organization; how to model long running, distributed processes; allowing information influx to design your events for you.

## Episode 14 — AI Nightmares and Expert Help
2025-02-22 · https://www.youtube.com/watch?v=AJgMPcvlhqs

In this episode Adam Dymitruk and Martin Dilger tackle the hard topics of AI generating really messy solutions and the problem with getting expert help in organizations.

## Episode 15 — Skills Issues and Simplifying Sagas
2025-03-05 · https://www.youtube.com/watch?v=vwJkHAnRen4

In this episode we talk about how incomplete knowledge can derail your Event Sourcing adoption and how to convert Sagas to TODO lists.

## Episode 16 — Dealing with varieties of APIs and millions of events
2025-03-11 · https://www.youtube.com/watch?v=5HUpQwOKpj4

In this episode Adam Dymitruk and Martin Dilger explore how different APIs are dealt with in Event Modeling and how we avoid dealing with millions of events in Event Sourcing.

## Episode 17 — Too many events!
2025-03-14 · https://www.youtube.com/watch?v=i_xPWdwQKPg

In this episode, Adam and Martin discuss the intricacies of event sourcing, focusing on the challenges of replay times, the importance of metrics, and the role of infrastructure in event sourcing systems. They explore the concept of monkey patching as a temporary fix for critical bugs, the significance of natural business cycles in managing event streams, and the advantages of event sourcing over traditional systems. The conversation also touches on unit testing, the evolving nature of software development, and the impact of their book on the field.

Takeaways: Replay every event is a powerful feature of event sourcing. Long replay times can be unacceptable in production systems. Temporary fixes like monkey patching can be necessary. Metrics are crucial for optimizing event sourcing systems. Natural business cycles can help manage event streams effectively. Event sourcing provides a clearer path to debugging and fixing issues. Unit testing can be simplified with event sourcing. Infrastructure should be minimal to avoid complexity. Event sourcing allows for better handling of schema changes. Boring software development can lead to more reliable systems.

## Episode 18 — The Future of Event Sourcing
2025-03-28 · https://www.youtube.com/watch?v=2V_7ecELcDU

Takeaways: Dynamic consistency boundaries can enhance event sourcing practices. Hydration and state views share similar logic in event sourcing. Commands should be treated as objects rather than functions. Simplifying event sourcing patterns can lead to better code quality. Testing in event sourcing can be streamlined through property comparisons. The future of event sourcing may involve AI integration. Experimentation is key to discovering new solutions in software development. Framework limitations can hinder innovation in event sourcing. Understanding the core concepts of event sourcing is crucial for improvement. Challenging established ideas can lead to significant advancements in the field.

Chapters: 00:00 Introduction and Weather Talk; 03:06 Wildlife Encounters in Vancouver; 06:07 Time Zone Challenges and Daylight Savings; 09:12 Updates on Workshops and Courses; 12:08 Dynamic Consistency Boundary in Event Sourcing; 15:13 Patterns in Event Sourcing and Hydration; 18:05 The Role of AI in Code Consistency; 21:10 Hydration and State Views; 24:14 Dynamic Context Boundaries; 27:19 Command Handlers and Event Handlers; 30:21 Simplifying Event Sourcing Practices; 33:22 The Future of Event Sourcing; 45:10 Exploring Dynamic Consistency Boundaries; 51:20 State Views and Command Handlers; 56:59 Simplifying Code Structure; 01:03:14 The Future of Event Modeling; 01:10:19 Reflections on Event Sourcing; 01:17:04 Concluding Thoughts on Experimentation.

## Episode 19 — Vibe Modeling, Event Models for the C-Suite
2025-04-23 · https://www.youtube.com/watch?v=nVPfDLHrqkY

In this episode of the Event Modeling and Event Sourcing Podcast, hosts Adam and Martin discuss the growth of event modeling and event sourcing, the launch of an online course, and upcoming workshops. They delve into the new trend of vibe coding, its implications for software development, and the concept of vibe modeling as a collaborative approach to system design. The conversation also touches on the challenges of managing large event models and the importance of maintaining readability and navigability in modeling tools. In this conversation, Adam Dymitruk and Martin discuss the intricacies of event modeling, focusing on workflows, the lifecycle of slices, and the importance of effective communication with C-level executives.

Takeaways: Event modeling and event sourcing are gaining traction in the industry. The online course complements the book and enhances learning. Vibe coding allows non-developers to create applications but poses risks. Understanding the underlying concepts is crucial for effective coding. Vibe modeling can enhance collaboration among stakeholders. Event models should be manageable and navigable for clarity. Miro has improved its performance for large event models. Splitting event models can lead to usability issues. The future of coding may involve more modeling and less traditional programming. A lot of workflows are trivially short, so it makes sense to combine them. The event model can serve as a living document that stays in sync with production. Slices are self-contained pieces of work that support a workflow. Feature toggles can be used to manage unfinished code in production. The definition of ready for a slice is crucial for client approval. C-level executives need high-level overviews, not detailed event models.

Chapters: 00:00 Introduction and Weather Banter; 03:09 Event Modeling and Event Sourcing Growth; 06:12 Course Launch and Learning Resources; 09:24 Book Updates and Future Chapters; 12:08 Vibe Coding: A New Trend; 24:13 Vibe Modeling: The Next Evolution; 24:53 Defining Goals and Vision in Application Development; 27:27 The Importance of Event Modeling; 29:21 Splitting Event Models: To Split or Not to Split?; 32:46 Scalability of Event Modeling in Fintech; 40:56 Maintaining Event Models: Keeping Them in Sync; 41:57 Understanding the Life Cycle of a Slice; 55:39 Navigating Agile Challenges; 58:13 The Importance of UI in Slices; 01:01:12 Team Collaboration and Skill Sharing; 01:05:01 Eliminating Subjectivity in Development; 01:07:25 Empowering Junior Developers; 01:10:40 Integrating AI in Development; 01:13:01 Communicating with C-Level Executives.

## Episode 20 — Learning Using Slices
2025-05-21 · https://www.youtube.com/watch?v=-tjrPx2aISI

In this episode, Adam and Martin discuss the growing popularity of event modeling and its relationship with Agile methodologies. They explore the importance of effective communication about event modeling within organizations, the use of swim lanes in event modeling, and the creation of new event models. The conversation also touches on the limits of event sourcing, particularly in relation to GDPR compliance, and emphasizes the need for clear workflows and documentation in software development.

Chapters: 00:00 Introduction and Personal Updates; 03:19 The Rise of Event Modeling; 06:15 Understanding Fixed Costs in Agile; 09:05 Experiences with Fixed Cost Models; 12:13 The Importance of Communication in Organizations; 17:06 Workshops and Community Engagement; 22:57 Advanced Workshop Insights; 23:23 Q&A on Swim Lanes; 26:10 Microservices vs Monoliths: Lessons Learned; 30:00 Creating New Event Models: When and Why; 38:26 The Limits of Event Sourcing: When Not to Use It; 53:55 GDPR Compliance and Event Sourcing: A Complex Relationship.

## Episode 21 — Simplicity is the Goal
2025-11-02 · https://www.youtube.com/watch?v=1XRNMPkXOZU

Topics covered: Exploring the Impact of In-Person Workshops; Event Modeling Conference Insights; The Power of To-Do Lists in Software Engineering; Reflections on Recent Workshops and Future Events; Understanding Event Modeling Trends Globally; The Importance of Face-to-Face Communication; Navigating the To-Do List Pattern; Event Modeling: A Growing Global Interest.

## Episode 22 — SQL is an Anti-Pattern
2025-11-04 · https://www.youtube.com/watch?v=NPB38JgSLeU

Takeaways: Event modeling reveals the hidden complexities of systems. Most companies lack a true understanding of their systems. Automation can significantly improve business efficiency. Event modeling helps identify areas for automation. Value stream analysis and event modeling are closely related. Shared understanding is crucial for organizational success. Event modeling enhances empathy among team members. Improvement requires change in processes. SQL has limitations as a programming language. Event sourcing aligns with how databases maintain consistency. SQL can be harmful if misused in integration projects. Refactoring tools are essential for effective TDD. Event sourcing offers a better approach than traditional models. The shift from cloud to on-prem solutions is gaining traction. AI is disrupting traditional software development practices. Making a big leap in development is often more effective than small changes. Event modeling can significantly enhance development efficiency. Organizations should embrace change incrementally within teams. Community support is vital for adopting new methodologies. The importance of focusing on the right 20% of tasks for significant improvements.

## Episode 23 — AI Takes Your Job
2025-11-08 · https://www.youtube.com/watch?v=sKS_WKHvy9w

In this episode, Adam and Martin kick off Season Two of the Event Modeling and Event Sourcing podcast, discussing upcoming workshops, reflections on recent conferences, the importance of networking, and the launch of their new event modeling company. They emphasize the significance of personal connections made at conferences, the benefits of smaller gatherings, and the future of event modeling tools, including the need for standardization in the field. In this conversation, Adam Dymitruk and Martin discuss the future of event modeling, the integration of various tools, and the optimistic outlook for humanity's evolution in the age of AI. They explore the necessity of change in event modeling practices, identify common anti-patterns, and emphasize the importance of managing complexity in UI design and command patterns. The discussion also touches on the challenges of refactoring and the need for transparency in event modeling to foster better communication and understanding among developers.

## Episode 24 — Cheap AI Is All You Need
2025-11-26 · https://www.youtube.com/watch?v=XlhH_Ld9xbg

In this episode of the Event Modeling and Event Sourcing Podcast, hosts Adam Dymitruk and Martin discuss the evolution of Event Modeling, introducing Event Modeling 2.0, which aims to provide clearer guidance for developers and business stakeholders. They explore the critical distinction between the 'what' and the 'how' in event modeling, emphasizing the importance of focusing on information flow rather than implementation details. The conversation also touches on the need for simplicity in modeling to accommodate complexity, the role of automation, and how to effectively communicate with business stakeholders about system functionality. In this conversation, Adam Dymitruk and Martin discuss the evolution and simplification of event modeling, focusing on information flow, automation, and the importance of timelines. They explore the given-when-then format, the role of refinements and projections, and how these concepts can be applied in AI systems.

Chapters: 00:00 Introduction and Webinar Insights; 01:31 Event Modeling 2.0: Evolution and Guidance; 06:19 The What vs. The How in Event Modeling; 10:11 Understanding Information Flow and Business Needs; 14:12 Simplicity and Complexity in Event Modeling; 19:52 Automation Changes and Information Flow; 26:37 Information Flow and Processing in Event Modeling; 29:04 Automation and Simplification in Event Modeling; 30:37 Given-When-Then Format and Its Evolution; 33:29 Refinements and Projections in Event Modeling; 37:14 Timelines and Human-Centric Event Modeling; 40:55 Simplicity and the Future of Event Modeling; 46:14 Event Modeling in AI and Future Applications.

## Episode 25 — Conceptual Structure of Code
2025-11-30 · https://www.youtube.com/watch?v=i31z4OUy9rI

In this episode, Adam and Martin discuss their recent experiences with workshops, the challenges of event modeling, and the impact of AI on software development. They explore the struggles developers face with implementation versus modeling, the benefits of event modeling in managing legacy code, and the future of software in the context of AI integration. The conversation also touches on community engagement and the public's perception of AI. In this conversation, Martin and Adam discuss various themes surrounding technology, market dynamics, and software development practices. They explore the concept of a market bubble, the implications of AI adoption, the importance of domain-driven design (DDD), and the advantages of event sourcing as a default practice. The discussion also delves into the differences between event modeling and event storming, emphasizing the significance of timelines.

Takeaways: Event modeling serves as a communication mechanism for developers. The struggle between implementation and modeling is a common challenge. AI is changing the landscape of software development. Legacy code can be rejuvenated through event modeling and AI. There will be a lot of shifting of money in the market. 85% of companies have realized no benefit from AI. The 15% that did are going to grow 10 times faster. DDD is about understanding business processes, not just technology. Event sourcing should be the default for storing state. Event modeling encompasses the entire software development lifecycle. Event modeling provides a clear timeline for events. Simplicity in design leads to better software solutions.

Chapters: 00:00 Introduction and Weekly Updates; 02:49 Workshop Insights and Automation Discussions; 05:57 Challenges in Event Modeling and Implementation; 09:07 The Impact of AI on Development Practices; 11:56 Legacy Code and Event Modeling; 14:50 Future of Software and AI Integration; 18:04 Community Engagement and Upcoming Workshops; 20:57 AI's Role in Healthcare and Society; 24:01 Public Perception of AI and Its Future; 37:29 The Bubble and Market Shifts; 39:50 AI Adoption and Its Impact; 41:00 Understanding Domain-Driven Design (DDD); 51:57 Event Sourcing as a Default; 01:04:31 Event Modeling vs. Event Storming.

## Episode 26 — A New Programming Language
2025-12-02 · https://www.youtube.com/watch?v=XhwG39VF1BY

In this episode, Adam and Martin discuss their experiences with learning and mastering Git, the importance of immersion in a subject, and the complexities of feature toggles in software development. They explore the role of event sourcing in providing clarity in specifications and the challenges of using natural language in requirements. In this conversation, Adam Dymitruk and Martin explore the connections between Git and event sourcing, emphasizing the importance of immutability and simplicity in software development. They discuss how AI is reshaping the industry, the challenges of enterprise software, and the potential future of AI in relation to traditional database companies. In this conversation, Martin and Adam delve into the intricacies of event modeling, focusing on the importance of vertical slices, the limitations of CRUD architecture, and the advantages of event sourcing.

Takeaways: Teaching others is a powerful way to learn. Immutability is a core principle in both Git and event sourcing. Simplicity in systems design leads to better understanding and implementation. Event sourcing allows for a clear history of actions taken within a system. Event sourcing can be implemented without traditional databases. The future of AI may disrupt traditional database companies. Vertical slices provide clarity in project scope and progress. CRUD architecture is inherently limited and prone to failure. Event sourcing offers freedom from concerns about future changes. The shift from CRUD to event sourcing allows for more flexible architecture. Collaboration in event modeling is essential for community growth.

Chapters: 00:00 Introduction and Reflection on Learning; 07:00 The Journey of Mastering Git; 14:08 Understanding Event Sourcing and CI/CD; 20:56 Feature Toggles: A Necessary Evil?; 30:00 Navigating Specifications and Requirements; 31:11 The Intersection of Git and Event Sourcing; 36:43 Immutability and Stability in Software Development; 42:53 Simplicity in Event Sourcing and Git; 49:13 AI's Impact on Software Development and Event Sourcing; 56:23 The Future of AI and Its Implications for the Industry; 01:06:16 Understanding Vertical Slices in Event Modeling; 01:11:30 The Satisfaction of Completing Slices; 01:13:15 The Limitations of CRUD Architecture; 01:19:01 The Cost of Maintaining CRUD Systems; 01:25:21 The Freedom of Event Sourcing; 01:31:17 Collaborative Future of Event Modeling.

## Episode 27 — AST: An Endangered Species
2025-12-06 · https://www.youtube.com/watch?v=Hb9NESFKTHs

In this episode, Adam and Martin discuss the evolving landscape of event modeling and event sourcing, highlighting the challenges of adoption, the importance of in-person workshops, and the impact of AI on software development. They explore how event modeling can serve as a powerful prototyping tool, bridging the gap between business requirements and technical implementation. In this conversation, Adam Dymitruk and Martin discuss the integration of AI in software development, particularly focusing on event modeling and sourcing. They explore the shift from traditional coding practices to more efficient methods, the impact of AI on development speed and clarity, and the evolving role of IDEs.

Takeaways: Event modeling is gaining traction but faces adoption challenges. In-person workshops foster better connections and understanding. Prototyping can be effectively done through event modeling. AI is a reflection of human practices in coding. The transition from JSON to more efficient formats like Toon is underway. Lightweight tools are preferred over heavy IDEs for efficiency. Local models can streamline development processes. Event catalogs may not be necessary with effective event modeling.

Chapters: 00:00 Introduction and New Beginnings; 01:57 Event Modeling Adoption Challenges; 05:59 The Importance of In-Person Workshops; 10:07 The Role of AI in Event Modeling; 14:03 Prototyping with Event Modeling; 18:06 The Shift in Software Development Paradigms; 22:07 The Future of Event Modeling and AI; 26:07 Refactoring and Productivity in Development; 30:04 The Disconnect Between Business and Development; 34:07 Event Modeling as a Continuous Process; 39:30 Legacy Code and AI Integration; 41:04 The Shift from JSON to More Efficient Formats; 43:03 AI's Impact on Event Modeling and Sourcing; 44:59 The Cultural Shift in Development Practices; 48:01 The Future of IDEs and AI Tools; 50:51 The Role of Local Models in Development; 53:45 The Evolution of AI and Its Economic Implications; 57:11 Event Catalogs vs. Event Modeling; 01:00:59 The Future of AI in Development.

## Episode 28 — Scientific Proof That Event Modeling Works
2025-12-07 · https://www.youtube.com/watch?v=TwL6IvM237U

In this episode, Adam and Martin discuss the upcoming workshop on event sourcing, the importance of various learning resources, and the role of AI in content creation. They explore contrarian thinking in technology and investing, emphasizing the significance of event sourcing in financial systems. The conversation also touches on innovative IoT projects, the scientific validation of event modeling, and the practical applications of the Maker Framework. In this conversation, Adam Dymitruk and Martin discuss the transformative impact of AI on various industries, emphasizing the importance of adapting to new methodologies such as event sourcing and event modeling. They explore the limitations of traditional practices like test-driven development (TDD) and advocate for a shift towards more efficient, slice-based approaches.

Chapters: 00:18 Introduction to Event Sourcing and Upcoming Workshop; 03:22 Exploring Learning Resources and Community Engagement; 06:24 The Role of AI in Content Creation and Learning; 09:15 Contrarian Thinking in Tech and Investing; 12:05 Event Sourcing in Financial Systems; 15:24 Innovative IoT Projects and Event Sourcing; 18:06 Scientific Validation of Event Modeling; 21:22 The Maker Framework and Practical Applications; 24:30 Concluding Thoughts on Event Sourcing and Future Directions; 32:59 The Impact of AI on Industry Standards; 35:02 Evaluating New Perspectives in AI Research; 37:07 Understanding Event Sourcing and Its Benefits; 41:13 The Importance of Slicing in Software Development; 44:17 Transitioning from Traditional to Event-Driven Architectures; 49:01 Challenges in Adopting New Methodologies; 53:14 The Limitations of Test-Driven Development; 56:56 The Future of Event Sourcing and AI Integration.

## Episode 29 — Leading Your Thoughts
2025-12-08 · https://www.youtube.com/watch?v=g9FCrbQ3Y4E

In this episode, Adam and Martin discuss the challenges of dealing with legacy code and the importance of having a solid plan for migration. They emphasize the need for modeling the current system using event modeling to understand its complexities and inform future decisions. The conversation also touches on the significance of incremental changes over big bang migrations and the role of effective communication with stakeholders. In this conversation, Martin and Adam delve into various aspects of software development, focusing on the shelf pattern in processes, the breakdown of complexity, and the nuances of charging for read models. They discuss the importance of project management and corporate culture, particularly in terms of credit attribution and the implications of thought leadership in the industry.

## Episode 30 — Tech Saves You From Inflation
2025-12-17 · https://www.youtube.com/watch?v=tjEQ9tCVb6s

In this episode, Martin and Adam discuss the intersection of technology, economics, and software design. They begin by reviewing a recent Event Modeling workshop, referencing key takeaways such as the importance of naming lookup models specifically for their slice to avoid coupling, and the visual placement of processors. The conversation then shifts to "Vibe Coding" and AI, with Adam sharing his experiment in building a Yahtzee game using LLMs. He highlights how AI struggles with scope—breaking existing features when asked to make small changes—and how Event Modeling provides the necessary structure to solve this. The core of the episode explores why technology should save you from inflation. Adam argues that software consultancies using a "pay-per-slice" fixed-price model shouldn't need to raise rates with inflation. Instead, increased efficiency and better tooling should allow developers to complete slices faster, effectively raising their hourly yield without charging clients more. They conclude with updates on tooling (Miro vs. custom tools), new book announcements, and the "musical score" analogy for reading Event Models.

Timestamps: [00:00] Intro & Christmas Market Chat; [01:58] Workshop Review: Processors & Lookup Models; [13:20] Vibe Coding: Building Yahtzee with AI; [27:40] Event Modeling as a Musical Score; [33:40] Why Tech Saves You From Inflation (Pay-Per-Slice); [53:50] Selling Fixed-Price Consulting in Europe vs. NA; [01:00:00] Tooling: Miro Pricing & Custom Tools; [01:04:20] Adam's Upcoming Book.

## Episode 31 — The Issue Trackers Are The Issue
2025-12-22 · https://www.youtube.com/watch?v=zCYW5r2WI6w

In this episode, Adam and Martin discuss their experiences with programming, AI, and event modeling. They explore how AI is making programming more accessible, the importance of version control, and the challenges of integrating issue tracking with event modeling. The conversation also touches on the chaos of documentation in repositories and the future of event modeling in the context of AI advancements. In this conversation, Adam Dymitruk and Martin Dilger explore various themes related to event modeling, plant growth, and the integration of security in software development. They discuss the evolution of their understanding of event modeling practices, the challenges of adapting to new requirements, and the importance of community engagement.

Chapters: 00:00 Introduction and Personal Updates; 02:57 Exploring Programming with AI and Event Modeling; 06:01 The Evolution of Programming and AI's Role; 08:54 Discussion with Linus Torvalds and Version Control; 11:58 Integrating Issue Tracking with Event Modeling; 14:52 Visualizing Bugs in Event Models; 18:09 The Chaos of Documentation in Repositories; 20:52 The Future of Event Modeling and AI; 23:46 The Challenge of Event Modeling Clones; 28:15 Challenging Traditional Knowledge in Plant Growth; 30:12 The Evolution of Event Modeling Practices; 32:49 Integrating Security into Event Modeling; 34:42 Reflections on Tooling and Licensing Issues; 36:06 Enhancing AV Setup for Better Streaming; 39:32 Innovations in Automated Plant Care; 40:57 Modeling User Interactions in Event Sourcing; 44:20 Successful Project Management with Event Modeling; 48:39 Adapting to Last-Minute Requirements; 51:30 The Impact of Legacy Systems on Modern Development; 56:31 Community Engagement and Future Workshops.

## Episode 32 — 2026 is the Year of the Event Modeling Desktop!
2025-12-31 · https://www.youtube.com/watch?v=Kadn6CGX7I0

In this episode, Adam and Martin reflect on the past year, discussing their personal projects, including programming with children, Raspberry Pi experiments, and the exciting world of 3D printing. They explore the role of AI in learning and development, the accessibility of technology, and their plans for the upcoming year, including a focus on event modeling and sourcing. In this conversation, Adam Dymitruk and Martin Dilger discuss the future of event modeling, focusing on the development of new tools, the growth of the event modeling community, and the integration of AI into the process. They reflect on their experiences and the importance of simplicity and reliability in event modeling, while also exploring the potential of DIY engineering innovations. The discussion highlights the significance of value stream analysis and the role of BPMN in enhancing event modeling practices.

Chapters: 00:19 Year-End Reflections and Charity Initiatives; 03:19 Exploring Programming with Kids and AI; 06:29 Diving into Raspberry Pi Projects; 09:14 Revisiting Circuit Design and Home Automation; 12:17 3D Printing and Maker Culture; 15:11 The Intersection of FreeCAD and Event Sourcing; 18:14 Plans for the New Year and Future Projects; 32:19 The Future of Event Modeling Tools; 34:18 Growing the Event Modeling Community; 36:05 The Shift from Traditional to Innovative Approaches; 39:31 Exploring DIY and Engineering Innovations; 42:21 Leveraging AI in Event Modeling; 45:18 Stability and Reliability of Event Modeling; 48:18 Value Stream Analysis and Event Modeling; 51:28 Integrating BPMN with Event Modeling; 54:28 Looking Ahead to 2026 and Beyond.

## Episode 33 — Simplicity Builds Confidence
2026-01-07 · https://podcast.eventmodeling.org/episodes/episode-33/

In this episode, Adam and Martin discuss the importance of community support, the development of event modeling tools, and the need to rethink practices in event modeling. They explore the significance of information integrity, automation in workflows, and how event modeling can be applied in everyday life. The conversation also touches on managing ADHD in project management and the simplicity required in consulting practices. Finally, they delve into the role of event modeling in financial systems, emphasizing its importance in understanding information flow and decision-making. In this conversation, Adam Dymitruk and Martin Dilger explore the intricacies of FinTech, the significance of event modeling, and the psychological aspects of productivity in software development. They discuss the fears and challenges faced in the industry, the importance of simplicity in tech stacks, and share lessons learned from game development.

Chapters: 00:18 Community Support and Giving Back; 03:13 Event Modeling and Tooling Development; 06:05 Rethinking Practices in Event Modeling; 09:07 The Importance of Information Integrity; 12:21 Automation and Workflow Management; 15:22 Managing ADHD and Project Management; 18:19 Event Modeling in Everyday Life; 21:26 Simplicity in Consulting and Event Modeling; 24:12 The Role of Event Modeling in Financial Systems; 37:10 Understanding Risk in FinTech; 39:19 The Power of Event Modeling; 41:15 The Psychology of Productivity; 45:03 Fear and Confidence in Software Development; 49:28 Navigating Industry Changes and Fears; 55:04 Simplicity in Tech Stacks; 01:18 Lessons from Game Development.

## Episode 34 — Slicing the Solution
2026-01-12 · https://podcast.eventmodeling.org/episodes/episode-34/

In this episode, Adam and Martin discuss various topics ranging from project updates in event modeling and AI integration to personal DIY engineering projects and culinary adventures. They explore the ideal size for meaningful systems, the liberating nature of deleting unnecessary features, and the challenges of effectively prompting AI. The conversation also touches on winter activities and family bonding, as well as reflections on programming and the future of AI in event sourcing. In this conversation, Adam Dymitruk and Martin Dilger discuss the advancements in event modeling and sourcing, emphasizing the integration of AI to enhance user experience and streamline processes. They explore the future of distributed systems, making predictions for 2026, and the necessity of adapting to new technologies.

Chapters: 00:18 Introduction and Project Updates; 03:24 Integrating AI in Event Modeling; 06:19 Personal Projects and DIY Engineering; 09:19 Culinary Adventures: The Lasagna Project; 12:15 Winter Fun and Family Activities; 14:20 Discussion on Coupling and Event Sourcing; 17:25 Experimenting with AI and Event Sourcing; 22:14 Challenges with AI Prompting; 25:25 Reflections on AI and Programming; 30:29 Conclusion and Future Directions; 33:01 The Evolution of Event Modeling and Sourcing; 39:05 Enhancing User Experience with AI in Event Modeling; 45:16 The Importance of Simplifying Event Modeling; 51:21 Predictions for Distributed Systems by 2026; 01:19 AI's Role in Schema Evolution and Business Opportunities.

## Episode 35 — Programming Languages Don't Matter
2026-01-21 · https://podcast.eventmodeling.org/episodes/episode-35/

In this episode, Adam and Martin discuss the recent workshop focused on event modeling and event sourcing, highlighting the implementation aspects and the rapid learning curve of participants. They explore the importance of frameworks, the polyglot approach to development, and the evolving role of AI in modern programming. The conversation also touches on the significance of teaching and making a difference in learners' lives. In this conversation, Adam Dymitruk and Martin Dilger explore various innovative projects involving Raspberry Pi, the integration of AI in everyday applications, and the potential of event sourcing and event modeling. They discuss the Ralph Loop, a coding experiment that allows AI to learn and improve over time, and the implications of AI on business processes and open-source software.

Chapters: 00:18 Workshop Insights: Event Modeling and Sourcing; 07:18 Learning and Implementation: Fast-Paced Progress; 12:18 Frameworks and Languages: The Polyglot Approach; 18:18 AI and Modern Development: Evolving Standards; 24:17 Reflections on Teaching: Making a Difference; 32:11 Innovative Raspberry Pi Projects; 34:31 Event Sourcing and Sensor Technology; 36:18 AI in Everyday Applications; 38:11 Leveraging AI for Business Processes; 39:28 AI-Assisted Learning and Event Modeling; 42:17 Exploring Google's Guided Learning; 45:53 The Ralph Loop: A Coding Experiment; 51:41 Learning from Iteration: The Ralph Loop Explained; 56:15 Reverse Engineering Legacy Code with AI; 01:19 The Future of Open Source and AI.

## Episode 36 — Getting Left Behind
2026-02-10 · https://podcast.eventmodeling.org/episodes/episode-36/

In this episode, Adam and Martin discuss their recent experiences with event modeling workshops, the integration of AI tools in software development, and the ethical implications of AI automation. They explore how AI has transformed their workflows, enabling rapid application development and the importance of maintaining ethical standards as technology evolves. In this conversation, Adam Dymitruk and Martin discuss the evolution of event sourcing and event modeling, emphasizing the importance of automation and AI in software development. They explore the challenges faced by developers in adapting to new tools and methodologies, the resistance within the industry to embrace these changes, and the potential for AI to revolutionize coding practices. The discussion highlights the need for efficient workflows and the inevitability of change in the tech landscape, urging developers to adapt or risk being left behind.

Chapters: 00:18 Introduction and Personal Updates; 02:19 Workshop Insights and AI Integration; 05:26 The Evolution of AI Tools; 10:13 Automation and AI Agents; 14:19 Ethical Considerations of AI; 20:16 Event Modeling and AI Collaboration; 35:59 Transitioning to Event Sourcing; 38:45 The Power of Event Modeling; 41:09 Overcoming Bottlenecks in Event Modeling; 42:58 The Industry's Resistance to Change; 44:58 The Future of Coding and Automation; 46:23 AI's Expanding Role in Development; 49:01 The Shift in Software Development Paradigms; 51:05 The Impact of AI on Major Companies; 52:39 Adapting to New Tools and Workflows; 56:29 Challenges in Current Tooling; 01:19 The Importance of Automation in Development.

## Episode 37 — Version 2 of Everything: The Looming Schema Migration Nightmare
2026-02-12 · https://podcast.eventmodeling.org/episodes/episode-37/

In this episode, Adam and Martin discuss the latest developments in event modeling and event sourcing, focusing on the Ralph Loop technique and its integration with AI. They explore the challenges and successes of implementing these technologies, share insights from their recent experiments, and outline plans for upcoming workshops. In this conversation, Adam Dymitruk and Martin discuss the transformative impact of AI and automation on the software development landscape. They explore how AI can replace mundane tasks, the future of code generation, and the significance of event modeling as a new programming paradigm. In this conversation, Martin and Adam explore the evolving landscape of skills and AI in the workplace, discussing the importance of breaking down complex tasks into manageable pieces for learning. They delve into the implications of AI on business models and the nature of work, emphasizing the need for human insight in system design.

Chapters: 00:18 Introduction and Overview of Recent Developments; 03:19 Exploring the Ralph Loop Technique; 06:07 Integrating AI with Event Modeling; 09:12 Workshop Planning and Community Engagement; 12:21 Challenges in AI Implementation; 15:17 Refining Skills and Local AI Solutions; 18:13 The Ralph Loop in Practice; 21:23 Iterative Development and Learning; 24:23 Future Directions and Tooling for Event Modeling; 27:37 Automation and AI Integration; 30:33 The Changing Landscape of Work; 31:54 The Future of Code Generation; 38:13 Event Modeling as the New Programming Language; 43:34 AI in Event Modeling and Code Generation; 51:52 The Role of AI in Modern Development; 58:52 Breaking Down Skills for Learning; 01:19 The Evolving Role of AI in Work; 01:20 Business Models in the Age of AI; 01:24 Creating Beyond AI: Personal Projects and Innovations; 01:27 Community Engagement and Future Directions; 01:30 Automation and Event Modeling in Real-World Applications; 01:32 Frameworks vs. Custom Solutions: A Developer's Dilemma; 01:35 The Balance of Control and Convenience in Development.

## Episode 38 — Co-Evolution In Software
2026-02-16 · https://podcast.eventmodeling.org/episodes/episode-38/

In this episode, Adam and Martin discuss the evolving landscape of consulting in the age of AI, highlighting the challenges faced by consultants in securing budgets as companies increasingly allocate resources to evaluate AI tools. They draw parallels between the current AI trend and the early .com era, emphasizing the importance of event modeling and event sourcing as stable foundations for navigating rapid technological changes. The conversation also delves into the implications of DCB (Domain Command Bus) in software development, the risks of unnecessary coupling in aggregates, and the need for clear articulation of system requirements to effectively integrate AI into business processes. In this conversation, Martin and Adam delve into the concepts of Dynamic Consistency Boundaries (DCB) and their implications for software development. They discuss the evolution of sagas, the importance of simplifying processes, and the need for better communication between technical and business teams. They explore the concept of 'moats' in business, the challenges of maintaining legacy systems, and the importance of community and collaboration in the tech industry.

Chapters: 00:18 Introduction and Exciting Updates; 02:05 The Impact of AI on Consulting Budgets; 05:57 Navigating the AI Landscape; 10:40 The Challenges of AI Integration; 15:56 Reflections on DCB Discussions; 21:04 Understanding DCB and Its Implications; 26:41 Introducing Dynamic Consistency Boundaries (DCB); 28:23 The Evolution of Sagas in Software Development; 30:43 Understanding Dynamic Consistency Boundaries (DCB) and DDD; 34:28 Bridging Technical and Business Perspectives; 34:39 Discussions on Logic Placement in Automation; 39:44 The Future of Human-Generated Software; 41:39 Reflections on Middleware and Legacy Systems; 48:36 The Simplicity of Complex Workflows; 50:23 The Evolution of Middleware and Automation; 53:12 The Disappearing Moats in Business; 55:50 Experimentation and the Role of AI; 57:28 Islands of Knowledge in the Tech Community; 01:01:01 The Dangers of AI-Driven Development; 01:03:30 The Future of Development and AI; 01:05:51 The Role of Event Modeling in Software Development; 01:11:19 Workshops: Bridging the Knowledge Gap.

## Episode 39 — Event Sourcing Predates Anything in Computing
2026-03-01 · https://podcast.eventmodeling.org/episodes/episode-39/

In this episode of the Event Modeling and Event Sourcing Podcast, hosts Adam and Martin discuss recent developments in AI and its impact on workflow automation. They explore the innovative integration of live coding with event modeling, the challenges of arrow layouts, and the importance of understanding slice-based architecture. The conversation also delves into community perspectives on event sourcing, critiques of AI implementation in organizations, and the significance of experience in navigating these new paradigms. In this conversation, Martin and Adam discuss various aspects of event sourcing, including its relationship with domain-driven design, the evolution of communication tools, and the importance of simplifying complex terminology. They delve into the debate surrounding event tagging and indexing, emphasizing the need for clarity in understanding event sourcing concepts. The discussion also highlights the portability of events and the significance of accounting principles in managing information effectively.

Chapters: 00:18 Introduction and Weekend Updates; 03:17 AI in Event Modeling and Code Generation; 04:23 Arrow Layouts and Event Modeling Challenges; 05:17 AI Solutions for Event Modeling; 06:18 Event Model Visualization Techniques; 07:18 Managing Connections and Arrow Crossings; 08:18 Leftness Index and Arrow Organization; 09:11 Event Sourcing and Architecture Discussions; 10:30 Slice-Based Architecture Insights; 11:22 Agent Interactions and Future Directions; 12:28 Industry Shifts and AI Integration; 13:27 Critiques of AI Implementation in Organizations; 14:15 Event Modeling Community Perspectives; 15:13 Understanding Slice-Based Architecture; 16:18 Navigating Feedback and Misunderstandings; 17:07 The Importance of Experience in Event Sourcing; 18:15 Abstractions and Coupling in Architecture; 19:24 DCB Discussions and Community Opinions; 20:20 Event Store and Indexing Mechanisms; 21:16 Event Modeling and Technical Discussions; 22:13 Conclusion and Future Considerations; 30:23 The Evolution of Communication Tools; 32:02 Event Sourcing and Domain-Driven Design; 34:26 The Debate on Event Tagging; 38:39 Understanding Event Indexing; 49:23 Simplifying Event Sourcing Concepts; 55:28 The Portability of Events; 57:29 The Importance of Accounting in Event Sourcing; 01:00:34 Preparing for the Upcoming Workshop.

## Episode 40 — Specification Driven Development, the New Thing from 2006
2026-03-08 · https://podcast.eventmodeling.org/episodes/episode-40/

In this episode, Adam and Martin discuss their experiences with workshops on event modeling and event sourcing, emphasizing the importance of adapting content to audience needs. They explore the challenges of using SQL databases for event sourcing and the innovative use of Git as an event store, highlighting the dynamic nature of software development and the necessity for continuous learning and adaptation. In this conversation, Adam Dymitruk discusses the evolution of version control systems, particularly the transition from GitLab to Git-T, emphasizing the importance of open-source solutions. He shares his journey of moving from Windows to Linux, highlighting the benefits of open-source software and the freedom it provides. The discussion also delves into the integration of AI in software development, the significance of modularity and coupling, and the future of event modeling as a reliable system design approach.

Chapters: 00:18 Introduction and Episode Overview; 07:28 Balancing Workshop Content and Audience Needs; 13:15 SQL and Event Sourcing Challenges; 18:22 Using Git as an Event Store; 29:33 The Evolution of Version Control Systems; 35:47 The Impact of Open Source on Development; 42:45 Event Modeling and AI Integration; 50:12 The Future of Event Modeling and System Design; 55:28 AI's Role in Software Development; 01:01:56 The Value of Event Sourcing and Accountability.

## Episode 41 — Reverse Engineering Using Event Modeling
2026-03-15 · https://podcast.eventmodeling.org/episodes/episode-41/

In this episode, Adam and Martin discuss the evolving landscape of work in the age of AI, emphasizing the shift from traditional coding to a focus on specifications and event modeling. They explore the benefits of automating legacy code analysis with AI, the importance of accurate documentation, and the challenges faced in implementing event sourcing. In this conversation, Martin and Adam discuss the challenges and opportunities in academia and industry, particularly in the context of event modeling and software development. They explore the disconnect between traditional academic approaches and modern industry practices, emphasizing the need for flexibility and openness to new ideas. The discussion also touches on the importance of optimizing performance in AI, the shift towards open-source solutions, and the future of event modeling tools.

Chapters: 00:18 The Evolution of Work in the Age of AI; 03:16 Event Modeling: A Tool for Understanding Specifications; 06:22 Automating Legacy Code Analysis with AI; 09:23 The Role of Documentation in Software Development; 12:19 AI's Impact on Software Development and Event Sourcing; 15:23 Challenges in Implementing Event Sourcing; 18:24 The Future of AI and Event Sourcing in Software Development; 35:13 Defending Old Paradigms in Academia; 38:32 The Disconnect Between Academia and Industry; 40:18 Challenging the Majority Mindset; 42:15 Event Modeling Conference Insights; 46:52 Dynamic Consistency Boundaries and Aggregates; 53:13 Optimizing Performance in AI and Event Modeling; 01:00:38 The Shift Towards Linux and Open Source; 01:07:42 The Future of Event Modeling Tools.

## Episode 42 — Who Trusts Event Modeling with Billion Dollar Projects
2026-03-22 · https://podcast.eventmodeling.org/episodes/episode-42/

In this episode, Adam and Martin discuss the significance of event modeling and event sourcing in software development. They explore the integration of AI in event storming, the importance of coupling in event sourcing, and the real-world applications of these concepts in large projects. The conversation highlights the renewed interest in event modeling and its potential to de-risk complex projects, emphasizing the need for collaboration between developers and non-developers. In this conversation, Martin and Adam discuss their ongoing projects, focusing on the integration of AI in event modeling and the importance of user experience. They explore the challenges of managing change in software development, particularly with AI, and emphasize the need for structured approaches to ensure productivity.

Chapters: 00:18 Introduction and Weather Talk; 03:23 Event Modeling and AI Integration; 06:16 Event Sourcing vs Traditional Methods; 09:07 The Importance of Coupling in Event Sourcing; 12:04 Event Modeling in Large Projects; 15:09 Real-World Applications of Event Modeling; 18:26 Future of Event Modeling and Sourcing; 21:19 Conclusion and Reflections; 36:11 Project Updates and Client Engagements; 38:57 AI Integration in Event Modeling; 41:38 User Experience Enhancements in Event Modeling; 46:51 The Role of AI in Event Sourcing; 55:08 Navigating Change Management with AI; 01:01:26 Future of Event Modeling and AI Collaboration.

## Episode 43 — Working Without Electricity
2026-03-29 · https://podcast.eventmodeling.org/episodes/episode-43/

In this episode, Adam and Martin discuss the evolving landscape of consulting in the age of AI, highlighting the challenges faced by consultants in securing budgets as companies increasingly allocate resources to evaluate AI tools. They draw parallels between the current AI trend and the early .com era, emphasizing the importance of event modeling and event sourcing as stable foundations for navigating rapid technological changes. The conversation also delves into the implications of DCB (Domain Command Bus) in software development, the risks of unnecessary coupling in aggregates, and the need for clear articulation of system requirements. In this conversation, Martin and Adam delve into the concepts of Dynamic Consistency Boundaries (DCB) and their implications for software development. They discuss the evolution of sagas, the importance of simplifying processes, and the need for better communication between technical and business teams. They explore the concept of 'moats' in business, the challenges of maintaining legacy systems, and the importance of community and collaboration.

Chapters: 00:18 Introduction and Exciting Updates; 02:05 The Impact of AI on Consulting Budgets; 05:57 Navigating the AI Landscape; 10:40 The Challenges of AI Integration; 15:56 Reflections on DCB Discussions; 21:04 Understanding DCB and Its Implications; 26:41 Introducing Dynamic Consistency Boundaries (DCB); 28:23 The Evolution of Sagas in Software Development; 30:43 Understanding Dynamic Consistency Boundaries (DCB) and DDD; 34:28 Bridging Technical and Business Perspectives; 34:39 Discussions on Logic Placement in Automation; 39:44 The Future of Human-Generated Software; 41:39 Reflections on Middleware and Legacy Systems; 48:36 The Simplicity of Complex Workflows; 50:23 The Evolution of Middleware and Automation; 53:12 The Disappearing Moats in Business; 55:50 Experimentation and the Role of AI; 57:28 Islands of Knowledge in the Tech Community; 01:01:01 The Dangers of AI-Driven Development; 01:03:30 The Future of Development and AI; 01:05:51 The Role of Event Modeling in Software Development; 01:11:19 Workshops: Bridging the Knowledge Gap.

## Episode 44 — Hermes Crab 🦀🐚
2026-04-12 · https://podcast.eventmodeling.org/episodes/episode-44/

In this episode, Adam and Martin discuss various topics related to event modeling, event sourcing, and the impact of open-source technologies on software development. They share personal updates, explore new projects, and critique traditional Agile methodologies. The conversation also touches on the elitism within domain-driven design (DDD) and the importance of collaboration in software development. They highlight success stories in event modeling and the shift towards more personalized and efficient software solutions. In this conversation, Adam Dymitruk and Martin discuss the transformative power of event sourcing and event modeling in software development. They emphasize the importance of eliminating unnecessary meetings and status updates, advocating for a more streamlined approach to project management. The discussion also touches on the pitfalls of AI solutions that merely replicate existing workflows without addressing underlying issues. The conversation concludes with insights into branching and merging in event models.

Chapters: 00:18 Welcome Back and Personal Updates; 03:25 Exploring New Technologies and Projects; 06:03 The Impact of Open Source on Software Development; 09:23 Event Sourcing and Its Benefits; 12:26 The Secret Club of DDD and Elitism in Design; 15:18 Workshops and Real Conversations in DDD; 18:20 Dungeon Masters and Knowledge Gatekeeping; 21:29 Success Stories in Event Modeling; 24:22 Critique of Agile Methodologies; 27:23 The Future of Software Development and Personal Projects; 34:39 The Power of Event Sourcing; 39:26 Transforming Meetings with Event Modeling; 44:20 The Illusion of AI Solutions; 51:17 The Future of Event Modeling and Collaboration; 01:01:18 Branching and Merging in Event Models.

## Episode 45 — Mind-Reading 🧠 as a Job Description
2026-04-19 · https://podcast.eventmodeling.org/episodes/episode-45/

In this episode, Adam and Martin discuss the growing importance of event modeling in the software development industry, sharing insights from recent workshops that highlight the learning outcomes and gaps in understanding among participants. They explore the transformative impact of AI on software practices, emphasizing the need for clear specifications in development. The conversation also touches on the open-source philosophy, the evolution of tools in event modeling, and the current market trends influenced by AI. The hosts stress the significance of community collaboration and hands-on learning. In this conversation, Adam Dymitruk and Martin discuss the challenges and opportunities in software development, particularly focusing on event modeling and the evolution of workshops. They explore the impact of AI on coding practices, the importance of community collaboration, and the future of software as a service.

Chapters: 00:18 Introduction and Industry Insights; 03:25 Workshop Experiences and Learning Outcomes; 06:15 AI's Impact on Software Development; 10:24 The Future of Event Modeling and AI Integration; 15:20 Linux and Open Source Philosophy; 20:27 The Evolution of Tools in Event Modeling; 25:32 Market Trends and AI Hype; 30:24 Community and Collaboration in Event Modeling; 35:28 Navigating Choices in Software Development; 40:08 The Evolution of Workshops and Event Modeling; 44:28 Reflections on Past Experiences and Future Directions; 50:37 The Role of Community and Collaboration; 01:00:34 The Future of AI in Event Modeling; 01:07:46 The Case Against Software as a Service.

## Episode 46 — Power Lines in Sim City 🏙️ European Edition
2026-04-27 · https://podcast.eventmodeling.org/episodes/episode-46/

In this episode, Adam and Martin discuss various aspects of event sourcing and event modeling, including the challenges of internet connectivity, the growing interest in event sourcing, and how to handle large CRUD forms. They delve into the differences between event sourcing and traditional systems, the importance of understanding events as decisions, and the complexities of schema migrations. The conversation also covers event versioning, upcasting, and the misconceptions surrounding event sourcing in software development. In this conversation, Martin and Adam delve into the intricacies of event sourcing, versioning, and the evolution of software development tools. They discuss the challenges of migrations, the impact of AI on event modeling, and the potential for real-time integration of AI in software systems.

Chapters: 00:18 Introduction and Internet Connectivity Issues; 03:12 Growing Interest in Event Sourcing; 06:18 Handling Large CRUD Forms; 10:20 Event Sourcing vs. Traditional Systems; 14:08 Understanding Events and Decisions; 18:15 Challenges of Schema Migrations; 22:18 Event Versioning and Upcasting; 30:15 Navigating Event Types and Versioning Decisions; 32:15 The Complexity of Migrations and Event Sourcing; 35:08 Tools for Schema Migrations and Their Evolution; 36:16 Reflections on Historical Software Development; 39:04 Harnessing AI for Event Modeling and Backtesting; 42:29 The Future of AI in Event Modeling; 49:17 Real-Time Event Modeling and AI Integration.
