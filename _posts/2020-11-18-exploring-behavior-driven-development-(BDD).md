---
layout: post
title:  "Exploring Behavior Driven Development (BDD)"
date:   2020-11-18 16:04:54 +0100
categories: bdd
---

# What is BDD

**Behavior Driven Development (BDD)** is an Agile software development process that encourages collaboration among developers, QA and non-technical or business participants in a software project. It encourages teams to use conversation and concrete examples to formalize a shared understanding of how the application should behave.

The main concept behind BDD is the cooperation between all the stakeholders of a project, in order to share the definition of a set of functionalities and how they should behave through a set of concrete examples.

From this point of view, BDD as a practice involving both technical and business users is strictly related to the Agile methodology principles.



# Mind the Gap: Business Vs. Developers Perspective

Let’s consider the existing scenario before BDD emerged as a practice. As developers know, the process of translating software requirements into a set of well defined feature specifications is tedious, frustrating and error prone. A software requirements document was the typical interaction between business users and developers when the waterfall methodology was in place. This is typically a static kind of interaction: business users wrote the requirements, and then developers extracted from it a set of functionalities to implement.

Software requirements documents can contain a lot of unnecessary details, a lot of contradictory descriptions of the same functionalities and also a lot of insufficient definitions of some other functionalities. So developers typically need to ask business users to integrate the document several times, but every version of the document is not a 1 to 1 mapping to the set of functionalities to implement.

The first thing to note is that the process of extraction of well defined functionalities from this kind of document is error prone; therefore, there is no guarantee that we cover all the functionalities nor that we define them correctly.

The extraction process can produce a considerably and not acceptable gap between the business users’ point of view and the developers one.

This gap is mainly due to the fact that who creates software requirements documents and who uses them to create features are two distinct teams. If we consider that QA is another team, then we easily understand that this process is quite problematic.

BDD as a practice to encourage the collaboration between people having different cultures and mindsets, and together explore and define features behavior, is a way to fill this gap.



# BDD as a Way to Describe Features

The central point of BDD is the sharing of tools and competences between technical and non-technical stakeholders, in order to share concepts and meet a common understanding of a set of functionalities.

**The first tool we can use is the language**: the concrete examples that describe the desired behavior of the system are written in a language that is very close to the natural language, so in the domain of business users.

BDD is made upon a three-step iterative process, where the steps are: **Discovery**, **Formulation** and **Automation**:

![](/assets/2020-11-18-exploring-behavior-driven-development-(BDD)/bdd-process.png)

#### 1 Discovery

BDD helps teams have the right conversations at the right time, so that you can minimise the amount of time spent in meetings and maximise the amount of valuable code you produce.

In this phase team members, both technical and non technical users talk about the requirements related to one or more functionalities (user stories), in order to obtain a shared understanding of the expected behavior through a set of concrete examples that describes how the system should work in different scenarios.

This phase is based on structured conversations called discovery workshops, where team members focus around real world examples that describe the features from the user’s perspective.



#### 2 Formulation

In this phase every example is expressed in a way that can be documented and then checked. The way is to express those examples using a medium that can be read both by humans and by automated processes.

A widely adopted language is **gherkin**: this is similar to a natural language and allows to describe the **features** through one or more **scenarios**.

Every scenario is a concrete example that explains how the feature should behave in a particular circumstance.

A typical scenario can be expressed in gherkin describing three things: 1) what are the preconditions to meet before beginning to use a feature, 2) what are the actions to be taken in order to use the feature, 3) and then what are the assertions to check if the feature is correctly implemented.

Here’s the structure of a typical BDD scenario:

**Given** a precondition

**And** another one precondition

**And** …



**When** I do something

**And** something else

**And** …



**Then** I expect something

**And** something else

**And** …


Here’s an example of definition in gherkin of the feature related to money withdraw using an ATM:

![](/assets/2020-11-18-exploring-behavior-driven-development-(BDD)/bdd-feature-gherkin.png)



#### 3 Automation

In this phase we take one scenario at a time and we make a test that satisfies the preconditions (expressed in the **given** clause), make the actions (expressed in the **when** clause) and then verify the assertions (expressed in the **then** clause).

The test is an automated way to verify if a functionality behaves as described in the corresponding scenario.

As we do in TDD, the test is made before the implementation: it is thus a failing test at the beginning, and then we implement the feature in order to make it pass.

Since this kind of test is defined by a team having business people in it, it has a recognized business value; therefore, it can be used as part of the **acceptance tests**.

BDD is supported by several open source and commercial tools; a couple of them are:

**Cucumber** https://cucumber.io/

**JBehave**     https://jbehave.org/


In the following example you can see how the tests related to the first scenario of the ATM feature can be implemented:

![](/assets/2020-11-18-exploring-behavior-driven-development-(BDD)/bdd-cucumber.png)


As you can see from the following example, the automation process produces a set of reports that are very useful for the team members to verify, during all the phases of the development, if the features are implemented, if they behave as expected or, for some reason, they need to be investigated further (in case a refactoring or some other change broke some of them).

Another key point is that **BDD can be viewed as a sort of documentation**: indeed, it explains what the features are, how they should behave, and how you can verify them.



![](/assets/2020-11-18-exploring-behavior-driven-development-(BDD)/bdd-report.png)

# BDD with TDD

BDD does not replace TDD. The automation phase produces a set of automated tests, but compared to those created by TDD, they are at a higher abstraction layer: they are actually used to verify a scenario related to a feature or to a user story.

A BDD test will guide the implementation of a feature as a whole and how to meet the expectations described in the related scenario. The implementation phase of a single feature involves many low level components and, embracing TDD practices, that implementation will start with a failing unit test of a small component; then, the component will be implemented, resulting in a green test. The cycle is then repeated for other components, as described in the following image:

![](/assets/2020-11-18-exploring-behavior-driven-development-(BDD)/bdd-with-tdd.png)

Since every feature is made of many small components, then every BDD test corresponds to many TDD tests.

Both BDD and TDD are iterative processes: they start from a failing test, then the implementation will have the side effect to fix the test and, when a refactoring causes a test to fail, the iteration will start again.



# TDD Vs. BDD

BDD tests are part of a shared understanding of a set of features between all the stakeholders of a project; they have a recognized business value and can be used as **acceptance tests** in order to verify if the system is behaving as expected.

They can be used to decide if it is safe to install in production (go / no go); typically, they can tell if something is broken, but not exactly what.

TDD tests are part of the development process, they are useful for developers to gain confidence about the quality of the software and also to do refactoring without the fear of breaking something, but they have not an immediately understandable business value.

TDD tests can tell exactly what small piece of the software is broken but, when one of these tests fails, it is usually safe to install in production.



# Conclusions

Although tests are a fundamental part of it, defining BDD as a test practice is highly reductive.

BDD is intimately related to the concept of Agile: with its procedures and tools, it facilitates the collaboration between people with different backgrounds and roles, in order to define a common point of view on the features to be implemented.

BDD allows you to verify the correct behavior of your software at any time during the development process, and helps provide a structured documentation on how your software should work.

BDD and TDD are not in competition with each other: each practice completes the other and is a fundamental aspect of the development process.



# References

https://cucumber.io/

https://jbehave.org/

https://cucumber.io/docs/bdd/

https://blog.gurock.com/bdd-testing-strategy/

https://gojko.net/2020/03/17/sbe-10-years.html

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
