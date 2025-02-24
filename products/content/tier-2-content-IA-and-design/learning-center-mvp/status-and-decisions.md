# Status and decisions for MVP Learning Center

## mm/dd/yy

## 9/23/20 

See summary of findings from search.gov call wrt learning center search: https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/content/tier-2-content-IA-and-design/learning-center-mvp/search-feature-inside-LC/README.md#summary-of-call-with-searchgov-on-918

Tl;dr - today, we can show the content type labels on FE generated article list pages; but search.gov does not have this ability for dynamic search results. In order to keep consistency between the 2 types of pages, in MVP 1.0 we are suppressing content type labels on the static article list landing pages.

LC Search - MVP 1.0
- In scope
  - Search.gov-driven keyword search 
  - Results will include document title and description
- Not in scope
  - LC content type in search results
  
Articles List - MVP 1.0
- In scope
  - Lists organized by: X LC Category, All articles tagged Y content tag
- Not in scope
  - LC content type embedded in the list items

MVP 1.1 - Article list and search results pages:
- PW FE will begin investigating custom options to include content type labels on the search results, so we can have consistent experience when we add content type labels in 1.1 static article list landing pages. 

## 9/22/20 

From CMS weekly call. 

Decisions re:

-  __CTA buttons in the CMS for LC:__ We don't need any special CMS modifications in order to link ppl from a CTA button to sign in. Nick confirmed that we can link to this URL https://www.va.gov/?next=%2Fprofile%2F - this link opens the sign in modal and takes the user to their profile dashboard.

-  __Landing pages for 'all articles in X category' or 'tagged: Y' use cases:__ These will be rendered by FE logic pulling from CMS meta data for categories and tags. These will not be dynamic pages rendered by search.gov engine. 

- __Nick and Kelson on PW to confirm by Sept 30 that we can use GraphQL__ data to create the ^ static landing pages. (See description of [requirements for the 'all articles in X cateogory' and 'tagged: Y' landing pages](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/content/tier-2-content-IA-and-design/learning-center-mvp/view-all-articles-in-X-category-landing-pg-requirements.md).) 




## 09/18/20

Liz Lantz, Ryan Thurwell, and Jennifer Strickland synced on how to move forward with responsive tables for the learning center.

**What we ARE doing for MVP 1.1**

- Proposing a solution that creates a responsive and accessible table UX, hopefully without CMS modifications.
- Planning to submit for an async design review w/ collaboration cycle team, since this includes a variation of a design system component

**What we are NOT doing right now**

- Submitting these concepts for review to be adopted globally, or into the design system
- Providing solutions for comparison table use cases.  We have mock-ups for these but want to learn from this MVP responsive version and understand how tables are used before we take those concepts further
- Implementing sticky headers or sticky functionality.  We started to explore this and identified some complexities that need to be solved for, and wouldn't be in scope for an MVP solution.

**Mock-ups**

[Screen 1](https://preview.uxpin.com/e7717d3fa019146277f28d799d247b820140d1b5#/pages/132642759/documentation/no-panels?mode=i) - shows what we **hope** can be implemented completely by the FE (no CMS updates required), for MVP 1.1

- includes a show/hide functionality that collapses columns 2-12, for tables that have 3 or more columns.  
- Includes a variation on the additional info component
- This may not be MVP 1.0 if it requires CMS work.
- There is documentation about a required `<caption>` element - this is the one piece I suspect needs CMS changes to implement.

[Screen 2](https://preview.uxpin.com/e7717d3fa019146277f28d799d247b820140d1b5#/pages/132642760/documentation/no-panels?mode=i) - shows what this would look like if a cell was expanded, and contains some additional documentation.

[Screen 3](https://preview.uxpin.com/e7717d3fa019146277f28d799d247b820140d1b5#/pages/132642765/documentation/no-panels?mode=i) - shows 2 things:

- What a 2 column table would look like (doesn't get show/hide) AND
- The pattern our responsive table can follow if the show/hide functionality turns out to be out of scope for MVP 1.1

> [CodePen example of screen 3](https://codepen.io/jenstrickland/pen/NWNOjMO)

**Next Steps**

1. We need our FE devs to evaluate the designs and determine if anything might require CMS changes. We can revise the concept so that CMS changes aren't required. 
2. Submit designs for an async collaboration cycle review.

## 09/01/20
Liz Lantz and Ryan Thurwell made decisions about which pages need mobile templates:
Template/Page | Release Version | Mobile Design
--- | --- | ---
About - text only | 1.0 |  not needed - just text
About - text w/ on this page, loooong content | 1.0 | needed, to explore use case of very long content (also, define `very long`). See #13038
About - tables | 1.0 | needed, see #11499. Check w/ eBenefits team's responsive table for View Payments
Checklist | 1.1 | needed, new pattern. See #13037
FAQ Single (question and answer) | 1.0 | not needed - just text 
FAQ Multiple | 1.0 | not needed, since uses existing ds component
Home | 1.0 | in progress, see #11490
Media list - images | 1.1 | needed, see #12759
Media list - video | 1.1 | needed, see #11497
Results - Keyword search | 1.0 | needed, see #12863
Results - `Articles tagged`  | 1.0 | not needed, since design will match keyword search
Step-by-step w/out screenshots | 1.0 | not needed, since uses existing ds component
Step-by-step w/ Screenshots | 1.0 | needed, to explore possible need for progressive enhancement. See #13036

## 08/06/20

### Engineering discussion - Nick Sullivan, Kelson Adams, Jen Lee, Mickin Sahni
#### MVP - Oct/Nov 2020

- Avoid Veterans Day Launch
- Through staging and perhaps hidden in prod (if possible given potential limitations)
- 1 audience type - Veterans
- 2 topics/categories: VA Profile and General resources/help
- Designs will look different
  - no find articles by audience
  - not every find articles by topic
- Includes search results
- Templates that will be included: 
  - About
  - Multiple FAQs
  - Single Question/Answer
  - Step-by-step

- In addition to the ^ templates, we will launch with these pages which are not technically templates:
  - LC homepage
  - LC search results page
  - LC 'view all X articles' page / LC articles tagged X page
- Will also include COPE reusable FAQs infra, which will be CMS infrastructure that lets us treat a question/answer unit as reusable content that can be published in multiple Drupal nodes (or pages). It allows us to create and edit that question/answer in one place, the FAQs library; while different authors can display that question/answer text on multiple Drupal pages without manually recreating that content on each of those pages.
- Tags to be included: Veterans VA Profile General resources/help Exact nomenclature is TBD

#### MVP 1.1 December 2020

- Additional tags
- Additional topics
- Was this helpful component?
- CRM integration
- Additional templates: LC HomePage Iteration, LC Search Results, About, Videos, Images
- Tags: Other audiences and topics

#### MVP 1.2 January-March

- CRM integration
- Onboarding authors, governance hardening

#### Questions

- Are we reinventing the wheel (loaded, i know) by revisiting account vs. profile when it comes to tagging?
- Are we seeing trends in search usage?
- Is there an opp to deviate between these iterations?
- What will view all articles look like?
- likely as search results
- How do we reconcile the two searches (LC and main VA.gov)?
- What is the order of search functionality we release?

#### Notes:
- wish we could hit drupal on the fly to search

## 07/27/20

### Outcome of accessibility review and design decisions

1/ __Video template:__ To ensure a better experience for mobile users and users on slow Internet connections, we will provide a 4-phased progressive FE experience. [See ticket #11497](https://github.com/department-of-veterans-affairs/va.gov-team/issues/11497)

Impacts: Design + FE engineering

2/ Audience links in the __Find articles by audience__ boxes:

__On desktop – no change for MVP:__

•	Default show 5 per box

•	Expand to show up to 10

o	  Future state when there are 10+ audience links in each box, we’ll use the same “View all…” ux as the topic links. User clicks View all > go to landing page showing all audiences as a list. 

__On mobile:__

•	Each audience box becomes an accordion

•	On expand, all audience links are viewable
o	    Future state mobile: when there are 10+ audience links in each box: we’ll create a different UX, as we don’t want an accordion to expand and require another click from inside an accordion to see all.

Impacts: Design + FE engineering 

3/ __Find articles by topic__ section
- We will not hide category articles in accordions. (Poor UX to hide 5 articles, expand 5, and in expanded view make them click again to see all the rest.)

- We will surface up to 5 each topic category, with a ‘view all’ link as currently.

- First mvp 1.0 (Oct/Nov) will likely only have 2 categories; next mvp (Nov/Dec) will have more categories, as more IRIS FAQs are migrated

_Design change - for post-mvp state:_

•	We will expose the first 6 category topics – TBD alphabetically or curated

•	We will include a ‘show more topics’ affordance to enable users to expose additional topic categories on the page

Impacts: Design + FE engineering + Content


4/ __Tags__

•	Tags will have a character max limit of 70 with spaces (matches our Learning center H1 and H2 limits)

•	Tags will be stacked if multiple tags fit over a line or in mobile

•	In mobile, the tag dimension will expand vertically to accommodate text wrapping

- In mobile, we may combine topic and audience tags under a single label "Tags" - for better stackability in mobile; we will adapt the same design on desktop. 

Impacts: Design + CMS + FE engineering

_Reminder re current tag requirements: There is a max 3 audience tags limit per article. We haven’t set a specific number yet for topic tags, but there will also be a max limit to ensure content authors are not tagging an article with everything and diluting search/filter relevance._

~5/ Print button on Checklist~  We are not providing a 'print' feature in LC mvp.


6/ __Back to top__ feature

•	We will provide a Back to top link that is triggered on page height. It will be sticky. [See ticket 11498](https://github.com/department-of-veterans-affairs/va.gov-team/issues/11498)

Impacts: Design + FE engineering




## 07/20/20
Summary of roadmap sessions with CMS team (Kevin, Steve, Clarence, Oksana, Jeff Barnes); Jen Lee (PW); and Dave Conlon (VAMC Upgrade+Facilities)

__Decisions - Q3 CMS product prioritization__

Facilities:

1. Delivery points (aka addresses and hours)	- Facilities	- Target: Aug/Sept

Learning Center:

2. Multiple FAQs template	- 	Public Websites	 - Target: 9/22 (Sept)

3. About template - 	Public Websites	- Target:  9/22 (Sept)

4. Process list update to include screenshots	- 	Public Websites	- Target: 9/22 (Sept)

5. Learning Center Home	- Public Websites	- Target: Sept

6. Audience, topic, LC taxonomy	-	Public Websites	- Target: Sept

7. Make FAQs in the CMS reusable: COPE in Drupal	- Public Websites	- Target: Sept

__MVP launch of learning center__
- MVP content: VA account and profile articles

- MVP templates: About, FAQs, Step-by-step's

- Target launch eta: Oct/Nov

__Status:__

- CMS team will work on #s 2-4 during sprint 11; and prepare for #7, in sprint 12. 

__Other:__
- PW team will have a FE technical discovery to get ready for working with the CMS team on the above Q3 LC deliverables. 
- PW user research on prototype is in flight to begin Aug 3.


## 07/07/2020

Summary of meeting between Jen Lee, Beth Potts, Danielle Thierry, and Liz Lantz to sync on research plan for MVP usability testing.

Discussed card sort, GH issues [#10432](https://github.com/department-of-veterans-affairs/va.gov-team/issues/10432#issuecomment-654412613) (responses captured in issue), [#10777](https://github.com/department-of-veterans-affairs/va.gov-team/issues/10777), [#10775](https://github.com/department-of-veterans-affairs/va.gov-team/issues/10775), [#10778](https://github.com/department-of-veterans-affairs/va.gov-team/issues/10778), and reviewed conversation guide.  Re-ordered tasks based on conversation.

**Decisions**

- Determined we want to do **one unmoderated hybrid card sort** with two participant groups to test audience labels
  - Group 1: Veterans, family members, caregivers. Looking into whether or not we can recruit through Perigean for unmoderated card sort
  - Group 2: Content authors. Jen will coordinate recruiting efforts w/ VHA, VBA, NCA contacts and SMEs
  - Danielle to possibly refine audience labels and get back to Liz with any changes
  - Jen will start list of articles but wants it to be a team effort
- We will prioritize the prototype usability study over the card sort

## 06/30/2020

Summary of meeting between Jen Lee, Beth Potts, Danielle Thierry, and Liz Lantz to sync on research plan for MVP usability testing.

Discussed [possible articles from this list](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/content/tier-2-content-IA-and-design/learning-center-mvp/wip-copy/README.md), research goals and tasks in conversation guide draft.  Determined overarching goal of this study: can users find what they need, and do they understand where they are in the site?

**Question:  Are we intentionally making learning center look different? Why?**

- Yes, it is intentional. We want to make a clear distinction between tier 1 and tier 2 content for users, and also for businesses. 
- The other reason we designed it this way, is that it doesn't have navigation, and because we've experienced pages which businesses have tried to make look like our benefit hub pages but they create them in a way that doesn't align with our patterns and how we create pages.  They compromise the nav structure.  With tier 2 and tier 3 content, that we're not going to be creating or managing, we don't want to manage the IA on those. And if they have same IA, navigation, and menu links as our hub pages, it will be bad.

**Question: Can we explore rate information in this study? Specifically, looking for insights on where people expect to see rate information. Is it with their benefit management and getting info or is that something people can find in the learning center? Is it something they look at when applying or is it something they reference later?**

- This topic would be better addressed in a study dedicated to content and/or applying for benefits since our study is really about being able to find the information, and if it is confusing going back and forth in the hub.  We can understand if users get confused without adding rate-specific content to our study.
- We can gain insights to user behavior with this information with analytics. E.g. looking at navigation summaries, how many sessions include both this info + application pages, or how frequently logged-in users (inferring they already have benefits) are looking at this info.
- Could be possible to explore this question in conjunction with another team who is evaluating the application process.

**Question: Do we still think a card sort is necessary? If so, what questions are we trying to answer with this?**

- Definitely still want to do a card sort
- Danielle is working on re-thinking some labels
- Let's re-group to discuss (meeting ran out of time)

**Decisions**

Whittling down the list above to a few core screens for the prototype:

- Learning center home page (1)
- Search results pages (2)
  - One w/ VA account specific results
  - One with tag results, that also has similarly titled articles where the template tag could help users determine 
- Hub pages  (2)
  - One for participants to start on when we want to see if they get confused going to the learning center from the hub
  - One for participants to land on from the learning center after clicking a CTA, to see if they get confused going to the hub from the learning center
- Learning center article page (1)
  - Participant will land on here from first hub page
  - Ideally would have CTA that would direct them to the second hub page



## 06/22/2020

Summary of decisions from 6/17 LC+CMS meeting w/ Kevin Walsh, Steve Wirt, Oksana Cyrwus, Stephanie Orkand, and Jen Lee. 

We are not prototyping page templates in Drupal, but the CMS team can start some related drupal epics. These are the templates the team discussed can be started in parallel with non-CMS workstreams (prototyping and user research). 

**Learning center templates we can build in the CMS in parallel**

These templates were selected to start with because they are 1/content template types that we know will have the most use by content autors and will fit the majority of content use cases, or 2/ they have component elements that can/will be used in other products (e.g., video component will be used in campaign landing pages). 

   * [Reusable single Q&A](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/content/tier-2-content-IA-and-design/learning-center-mvp/template-requirements.md#single-faq) (COPE epic)
   * Reusuable multiple FAQs (COPE epic)
   * [About template](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/content/tier-2-content-IA-and-design/learning-center-mvp/template-requirements.md#about)
   * [Video component](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/content/tier-2-content-IA-and-design/learning-center-mvp/template-requirements.md#media-imagevideo)
   * [Step-by-step template](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/content/tier-2-content-IA-and-design/learning-center-mvp/template-requirements.md#step-by-step) (Iterations on 'subway map' process list to enable screengrabs) 


**Question: Are tags something we can start in parallel, since this will used across all learning center templates?**

- We need to flesh out the MVP taxonomy and other requirements. This needs to be a follow up call as a topic. 


## 06/11/2020

### CMS-focused follow-up meeting

**Agenda**

* Should we prototype in Drupal, or something else?
* What questions would we like to gather, to inform the questions we'd like answered by user testing?  (or, where to log these questions so we don't lose them)
* Next steps

**Action Items from this meeting**

1. Continue building questions for user research and review the need for prototyping
2. If prototype is warranted for testing, will pursue a clickable prototype. Public Websites discussion needed.
3. Jen to review the suggestion for bringing in more content for testing purposes
4. Stephanie to set up a followup with the CMS team on components. In this follow-up, we will need to review the components. As we review, we will need to discuss which components (if any) would need to go throgh user research first before being built.

**Initial list of questions or areas of interest, for user research**

1. The findability, navigation of content using this search-focused, tag-based navigation. Is the information easy to find using this new method?
2. The taxonomy, IA of categories. Is the chunking of the categories and labels the best way to begin this? For Veteran and other audiences, in terms of taxonomy and nomenclature, is this effective?
3. The labels of the types of templates, and if they affect what the user chooses to read (ex: FAQs, Checklist, Media List). We think it is useful for users. Do we test without the labels to gauge if including is an improvement or not?
4. Based on the thoughts regarding Tier 1 and Tier 2 content: is there a way we can find out with users how comfortable they are with the distinction between Tier 1 and Tier 2 content - or do they even care, as long as they can find what they need? Does it matter if something is in benefit hubs or learning center? How frequently do they go bak and forth?

### Notes from meeting

Before we begin a prototype, what questions do we want to get answered by user research? This may impact if we even need a prototype. 

In approaching a prototype, the CMS team recommends focusing on a clickable prototype & not building a prototype in Drupal. The investment in using Drupal for this purpose would be high. Their feedback is captured below under "Learning Center user research / prototyping notes from CMS

The CMS team recommends we include more than one content type (currently planning for Account information) for prototyping to help prove out a better content model. The CMS team provided thoughts and feedback regarding the distinction and access of Tier 1 and Tier 2 content, also captured in their notes below. 

We believe that users care less about where the content lives or how it's structured as long as it's easy to find what they are looking for. Are users thinking in precise terms the way IA, taxonomists are thinking?

The CMS team recommends not building a prototype in Drupal but there items they could start on shortly that would further this initiative. They could start on related Epics around:

* Reusable Q&AS, FAQs
* Video (note: this is shared with the Campaign Landing Page, and would be built to serve both)
* Checklist component
* Step-by-step component - it's a modification of the subway map for when we want to include screenshots. This would allow content authors who provide step 1, step 2, etc. for things like 'how to do x in a tool', they would be to provide screenshots as visual reference for users
* Iteration on the Table component

### Learning Center user research / prototyping notes from CMS

**Should we prototype in Drupal, or something else?**

1. Generally speaking, no. At this stage, we recommend clickable prototypes instead of investing in an approach using Drupal & FE that consumes the content API, because
   * The amount of resources required. 
   * The amount of risk / unknowns for many of the templates. 

**What questions would we like to gather, to inform the questions we’d like answered by user testing?**

1. Do these designs create too much distance between Tier 1 and 2 content?  
   * We see risk in this design that Tier 1 and Tier 2 are silo’d through two primary IA means: search and tags/taxonomy. 
   * The only bridges to Tier 1 that we can see are CTA buttons and Related information. Search and Topic/Tags listing do not seem to surface Tier 1. 
   * The CMS can support the IA needs of users to get to Tier 1 content while maintaining the Tier 1 / Tier 2 governance distinction.. 
2. Not a question exactly, but relevant to the “real content” question for user testing. The Account info epic 9938 looks like an excellent use case. BUT:
   * We recommend multiple use cases for each template. 
   * We’re concerned that a single use case for MVP (Account info) may not yield the level of content diversity required to make content model decisions. 
   * User research about account info may point us down a content model path specific to that use case, and content models are expensive to refactor.

**Additionally**

1. Just because we are not prototyping page templates in Drupal, doesn’t mean we can’t start some related drupal epics, at the component level, eg:
   * Reusable Q&As, FAQs
   * Video component
   * Checklist component
   * Iterations on Process list (eg screengrabs) 
   * Iterations on Table components


## 06/04/2020

Team Kick-off held, to align on problem to solve, high-level requirements and wireframes. 

**Why The Learning Center**

We have brought over Tier 1 content over for benefits. There is a lot of information that is not in the Tier 1 category but is very helpful content.

The Learning Center aims to house additional help information, knowledge articles about a service or a problem. It is benefit adjacent. The product is not campaign or marketing information, and it is not program office/administration content. The Learning Center is search-focused and tagged, rather than driven by IA and navigation. This will be in Drupal as templates.

**MVP and Requirements**

The content below does not replace or substitute the product outline. 
We plan to use VA.gov account information for this "MVP."
Some new functionality that was discussed:

* New/updated Search box with the ability to search within the learning center or va.gov (this is in the learning center, at the top of the pages)
* Tag system - 'Topics' and 'Audience'
* "On this Page" component
* "Back to top" (some of the pages will get really long)
* "Need More Help" section - can be phone numbers, links, links to chat. It will be customizable but something like a chatbot could be 'fixed' on there, if it's available.
* "Was this page helpful?" - TBD on where the data from users would go
* Ability to pull Youtube video, content in for Videos. 

**Identified Areas for User Testing**

The new tag system - by breaking up tags between "Topics" and "Audience", does this help users? The "Topics", for example, would be clickable and would take the user to articles tagged with that topic.

When viewing a list of articles tagged with a topic, we are curious if the types of templates affects what the user chooses to read (FAQs, Checklist, Media List). Would knowing this kind of content be helpful to the user?
Should we plan to conduct testing with the two identified user groups - Veterans, and groups who support Veterans?

**Next Steps**

A goal of the meeting was to determined what first steps we should take to move this initiative forward. 

1. User testing is desired, but we would like to have a prototype (clickable) available to test with
2. Defining questions that we wish to answer through user testing (research planning - meeting(s) to take place soon)
3. Follow-up on CMS next steps, and prototyping: should we prototype in Drupal, or something else? Stephanie to schedule a discussion for this topic
