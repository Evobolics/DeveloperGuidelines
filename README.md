# Software Development Guidelines Abstract

This document contains a number of software development guides that are intended to aide developers in writing software.  Most of these guides are just guidelines, and should be treated as such; but when they are generally adhered to, they can save a lot of future time and effort.  I am always up for feedback so please feel free to drop me a line.

# General Rules of Thumb

The following are rules that developers need to read and follow in addition to technical guidelines that will follow. 

## Treat Coding as a Business - Not as Research

Unless your organization is focused on research, at the end of the day, the goal is to create and deploy software that a business can use to produce a return on investment (ROI).  Therefore, when prioritizing time, it is more important stories get completed and things work well; creating beautiful code is always secondary.  While it is important to take pride in having well structured code, very few people in the business will ever see the code.  Most likely, only other developers and IT professionals in the organization will ever work with it.  Thus, do spend time structuring code well but do not take so much time that it hurts the teams story velocity - **story velocity and code that works well without error is king**.  Remember, at any point in time, the business can choose to cancel a project or shift directions, regardless if it is a work of art or not, and all of the time perfecting a piece of code will be lost.

## Same Office Attendance Policy

If anyone on a call is in the same building as another attendee, do not call individually from a computer station, but instead find a room for everyone in the building meet together.  Programmers spend way too much time behind computer screens.  Meeting in person greatly improves (even encourages) communication, aides in knowledge transfer, and disrupts interruptions of surrounding team members.  White board sessions often come up on the fly and its helpful to have everyone in the same room.  We are team; act like one!

## Dress Professionally

Just because you can come to work wearing a shreded shirt, and pair of jeans with holes in them, and have your underwear showing, does not mean you should.  Dress for the job you want, not the job you have.

# Naming Guides

Following a consistent set of naming conventions in the development of a framework can be a major contribution to the framework’s usability. It allows the framework to be used by many developers on widely separated projects. Beyond consistency of form, names of framework elements must be easily understood and must convey the function of each element.

The goal of this section is to provide a consistent set of naming conventions that results in names that make immediate sense to developers.

Although adopting these naming conventions as general code development guidelines would result in more consistent naming throughout your code, you are required only to apply them to APIs that are publicly exposed (public or protected types and members, and explicitly implemented interfaces).

|Before diving in, please keep in mind that the most important thing about naming is not to be afraid to just pick something and get moving.  Please do not waste hours trying to think of a perfect name.  It is almost always possible to come back later and change a name during the code review process.  With that said, do put a few seconds to a few minutes of thought into any names picked as they may last a while.  Last, please watch the spelling of names as misspellings have a way of lasting years in a system. |
|--|

## Names of Assemblies and DLLs

An assembly is the unit of deployment and identity for managed code programs. Although assemblies can span one or more files, typically an assembly maps one-to-one with a DLL. Therefore, this section describes only DLL naming conventions, which then can be mapped to assembly naming conventions.

✓ DO choose names for your assembly DLLs that suggest large chunks of functionality, such as `MyCompany.MajorSystem`

**NOTE: Assembly and DLL names don’t have to correspond to namespace names.**  

In traditional .NET the assembly name is the common portion of the namespaces used the library and it makes it simple to come up with a assembly and namespace pattern.  In practice though, linking the two together can cause issues for code portability.  When working with multiple systems, it is important to write code that can be transferred and referenced between systems without having to refactor namespaces.  

✓ CONSIDER naming DLLs according to the following pattern:

<Company>.<Component>.dll

where <Component> contains one or more dot-separated clauses. 

For example: CN.Controls.dll.

## Organize Your Solutions

Organize the projects in your solution using solution folders to aide readability.  Use numbers: 1, 2, 3 or 01, 02, 03 (for solutions with more than ten projects) to put your project in order. Infrastructure projects should be at the top, and examples should be at the bottom.  Each folder should be a natural layer in your solution with each one building on top of the previous one.

## Project Names

Project should named [Company].[Project].[Subsystem].  

Project names can have the words like Core, Base, and Abstractions in them.  Namespaces should not.

After you have created a project, the default namespace should be set to `CompanyName` or an abbreviation. 

## Namespace Names and Folder Structure

### Do not use Nouns

Namespaces should be plural nouns, adjectives, verbs, and adverbs.  Do not use singular nouns in folder names as they will be transformed into namespace names and cause conflicts with classes that use the same singular noun names. 

### Use the Shortest Name Possible

Namespaces have to be written often and their names need to be simple and to the point.  When considering how to name something and there are two possible words for the same concept, use the shortest of the two.  For example, assume a Common / Infrastructure / Core namespace was needed to contain some classes that can be reused.  The later namespace name `Core` should be used over the longer `Common` and `Infrastructure` names if possible. 

### Abbreviate Common Names that are Used Often

Namespace names that are common and used throughout the source code should be abbreviated, especially if they are not going to be made public.  For instance, most of our libraries are not going to be shared with outside parties, and thus it is possible to abbreviate `CompanyName` by just typing `CN`.  Ideally, the team should look for a root namespace name that is eight characters or less.  Now a coder just has to type in two characters to access the root namespace each time instead of typing eleven.  If the library was going to be used externally, then the root namespace of `CompanyName` should be considered for marketing reasons.  

### Pick Names that Minimizes Change

Pick a namespace naming strategy that minimizes the amount of change long term.  The costliest thing in a software development shop is development / testing time.  

### Go from Broad and Fixed to Narrow and Dynamic

Namespaces should start with broad and fixed terms and then proceed to become more narrow and dynamic in nature.  For example the first namespace should often be the companies name, or another common aggregator.  The next level should be names like `Models`, `Services`, `Enums`.  These again are names that do not change often, and provide structure to the code.  More on this on the next section.  

### Use Type Specificity

Traditionally in the past, namespaces start with a company name and then are followed up with a technology and features names.  This is good for separating business concepts, but it does little to explain or encourage a clean design.  Thus, in addition to including the company name in the namespace, the type of the component should be included the namespace path name.  For instance, `CN.Models.Tickets`.  This namespace says the software came from Company Name (CN), and contains models that are Tickets specific.  `Models` is put BEFORE `Tickets` because it is broader in nature than `Tickets` and can be used for more items.  

The following is the common pattern that works well for most namespaces:

`[Type].[Business Name].[Type].[Business Name]...[Type].[Business Name]`

The first [Type] argument of global, Systems or Root is often implied or not needed so most namespaces first start with a business name like `CN` or `CompanyName`.

Common type names that should be considered are:

|**Namespace Type Name**| **Description / Use Case**  |
|--|--|
| Models  |  for business models |
| Entities / DataModels  | for database level models  |
| Services  | for business level services |
| DataServices  |  for database level services  |
| Exts  | should contain extension methods |
| Enums  | should contain enumerations  |
| Constants  | should contain constant declarations. |
| EntryPoints  | for Program and Startup files, if not in the root directory |

### Try to Avoid Overly Nested Namespaces

When coming up with namespaces, try to treat them as heading in a document: less is better.  It most cases, the number of namespaces in a path should not exceed three to four levels, unless the work is overly technical and requires a lot o branching.  Using this approach greatly aides in keeping the using statements at the top clean and to a point.  In addition, when creating micro-services, having these the namespaces short allows for clean compaction of namespaces.  For example, assume three services are needed that all perform Ticketing work.  Their assembly names would be `CN.Ticketing.A`, `CN.Ticketing.B` and `CN.Ticketing.C.`  But, all the libraries could declare and use a single `CN.Services.Ticketing` namespace that is used to house each libraries service, given care is given to not have any class name conflicts.  

### Abstraction Libraries

It is common practice to create abstraction libraries that contain interfaces that are going to be used by integration points, enumerations that are going to be used across projects, or just common code.  These libraries should end with the name Abstractions in the project / assembly name, but the name should not be present in the namespace name whenever possible.  The design of the libraries should be setup where the developer should only have to include the namespace without the word Abstractions in the using statement and the class names should not conflict.   

# Coding Style Guides

## Comments

All classes, methods and properties need short comment on them that explain the purpose of the field.  It may be obvious to the developer who is writing the class what the purpose of the field is, but it will not always be obvious to the developers that come years later that have to support the code base.  Please take a few extra minutes to add comments as it will save developers that come later hours.  In addition, it will greatly increase the longevity of the code and decrease long term costs for the company.

## Remove Unnecessary Using Statements

Please remove all unnecessary using statements from your class files. 

## Organize your Using Statements

Using statements should remain organized and ordered to aide readability and maintainability.  

# Design Pattern Guides

## Model and Service Separation

Traditional OOP allows for models and methods to be coupled together.  For instance, a telephone class could have a property called `CurrentTelephoneNumber` and `Dial()` method.  In theory, this can work well.  But in practice, the method Dial and the Telephone class should have different software life-cycles, and should be separated.  The Dial method should be contained in a service, and only a single instance of it should exist as a singleton.  The Telephone class on the other hand should be setup to be a transient, and multiple copies of it should be created.  In addition, by separating out the two concepts, it is now possible to change the `Dial()` method without causing any ripple affects to the data structure.  

## Code a Class for a Purpose

When writing a class, code it for a singular purpose.  The singular responsibility principal (SRP) states that a class should only have a single reason to change.  Traditional OOP lets this singular purpose include methods and properties in the same class.  OOP structured for rapid change and for dependency injection does not.  When coding classes, keep them setup for DI and set them up for success when working in a rapidly changing environment by keeping service code focused on services and models focused on being models.  This is accomplished by moving most methods to services, and leaving models with just properties.  The two major exception to this rule is when it is necessary to create class inheritance structures for models that need to wire up abstract members or when needing to create models that are enumerable.  

# Source Code Branching Strategy

```
---> Master
  ---> Feature
    ---> User
```

# Agile Development

## Story Estimation Guide

A story points is equal to a combination of time, complexity, and risk.  

`Story Points = Time + Complexity + Risk.`

### Time Estimation

The following table should be used as a guide when estimating a stories points.  

| **Points** | **Description** |
|--|--|
| 01  |  Estimated it can be done in a half day (3 hours) |
| 02 | Estimated it can be done in a day (6 hours) |
| 03 | Estimated it can be done in one to two days (6-12 hours) |
| 05 | Estimated it can be done in two to three days (12 to 18 hours)  |
| 08 | Estimated it can be done in three to five days (18 to 30 hours) |
| 13† | Estimated it can be done in five to eight days.  |
| 20† | Estimated it can be done in under two weeks. |
  
|**† -** Whenever possible a story should not be estimated with this number of points.  When a story has this many points, it is hard for the team and management to see movement on the story and it puts the developer and team at more risk for the story not to be completed.  If the number of points is reach due to complexity or risk, the story should be evaluated to see if it can be broken down further.|
|--|

### Complexity Estimation

| **Risk Level** | **Description** |
|--|--|
| Low | The story is of low complexity and only touches a single method or class.   No additional points should be added to the story.   |
| Medium | The story touches a single system or a single library and multiple changes are being made within the library.   One to two points should be considered to be added to the story's size.   |
| High | The story touches numerous libraries and/or systems.   Three or more points should be added to the stories size.|

### Risk Estimation

| **Risk Level** | **Description** |
|--|--|
| Low | The story is low risk and does not require much coordination between team members.  No additional points should be added to the story.   |
| Medium | The story has some risk to it and some coordination is needed between the team members to accomplish the story.  One to two points should be considered to be added to the story's size.   |
| High | The story has some considerable risk associated with it and a lot of coordination is needed between team members if the story is going to be completed within the sprint.  Three or more points should be added to the stories size.|

# Solution Setup and Design

## Folder Structure

All solutions should contains the following folders:

|**Folder Name**|**Description**  |
|--|--|
| src | Stores all source code for the solution.  |
| doc | Stores all documentation related to the project |
| lib | Stores all referenced assemblies that are not available from a nuget feed.  Libraries available on any nuget feed should not be checked into source control. |
| build | Contain files related to the build.  e.g. *.yaml files|

### The 'src' Folder

The src folder should contain all the source code for the solution. 

All solution files should be in the src directory and not in any project directories.  

# Library Architecture and Design

## Microservices and Micro Libraries

As this guide will get into further, this company is against writing any new [monolithic](https://articles.microservices.com/monolithic-vs-microservices-architecture-5c4848858f59) apis going forward.  Instead, all new API libraries need to be setup to be micro services.  In addition, this company is against creating large libraries as they cause the need for everything including the kitchen sink to be included as libraries.

# API Architecture

## GRPC

# Coding Practices

## Keep Horizontal Scalability in Mind

It is important to keep horizontal scalability in mind when creating systems.  No business logic should ever be placed in stored procedures or any database specific code.  In fact, triggers and stored procedures should be completely avoided.  

## Design your Systems to be Database Agnostic

This company primarily targets SQL Server databases, but this will not always be the case when the systems start moving to the cloud.  When writing new code it is important to keep this fact in mind and design all new systems to be database agnostic - do not write code that specifically targets a single database engine.  Any new code should be written where the data layer is modular; the only change that should be needed to consume a new data service is to replace what classes are swapped out  are injected in the IOC container.  This means that triggers and stored procedures should be avoided.

## Performing Conversions

When converting data types, do not assume the input is of the type expected.  Always use the `Try` version of the convert method and setup your code to handle unexpected input values with default values.
 

## Cost of Change is More Important than Encapsulation

The costiest thing in a development shop is the programmers time; thus it very important to make sure each day each developer spends their time wisely and keep the cost of changing code in mind.  Everytime a developer has to change code there is the potential for bugs to be re-introduced to a program and the software needs to go through 

# Language Specific Guides

## CSharp

### Volatile Keyword

If you are writing new code targeting the .NET 2.0 runtime or greater, [do not use it](https://blogs.msdn.microsoft.com/ericlippert/2011/06/16/atomicity-volatility-and-immutability-are-different-part-three/).  If you really feel that you need to, think again, read the above article, and if you still think you do, discuss it with the team first.  There really is no need for it for the systems being built by developers. 

## VB Dot NET

This Company does have VB Dot Net projects and thus a few words of wisdom are needed for anyone that is working on these projects.  First, [Option Explicit](http://vb.net-informations.com/language/vb.net_option_explicit.htm) should be turned ON; no exceptions.  Second, set [Option Strict](http://vb.net-informations.com/language/vb.net_option_strict.htm) to ON. Last, no project should have a reference to Visual Basic, as the functions have been proven to be over a thousand times slower than using their .NET counterparts.

# DevOps

This section of the guide will go over guiding principals of Development Operations, which is often abbreviated DevOps.

DevOps maximizes the return on investment (ROI) and drastically lowers the total cost of ownership of developing and running a software platform.  

Get rid of redundant work. 

# Repository Setup

There are four flavors of repositories that are common:

1. Monolithic Solution Structure
2. Systems and Combined Libraries
3. Systems and Seperate Libraries
4. Everything Seperate

## Monolithic Solutions

A monolithic solution architecture is the most often solution architecture that is seen.  It is because most companies and organizations start from a single project and or solution and the thing grows.  

### Bifuricated Monolithic Solutions

## Seperated Systems with Combined Libraries

The next common 

## Seperated Systems with Seperate Libraries

Each major system is seperated in its own repository and the This architecture requires a lot of automation to be in place.  

## All Projects are Seperate

The last architecture that is present is one where every project has their own repository.  Period. No Exceptions.  This forces dependencies to be seperate, but 

## General Repository Guidelines

Do not try to combine folder names with periods to save nesting.  It makes it harder for others come along and add to the structure without having to decompress the nested folder structure.

# Continuous Integration

# Continuous Delivery

The goal is to provide valuable continous delivery to the organization.  

Without delivery, all the code that is checked in just stays checked in, is not deployed, and does the organization little.  

Ideally organizations want to gain return on investment for any code written as soon as possible. The goal is to move away from release cycles.  As soon as a piece of code is ready for the user to use it 

## Moving Beyond Virtual Machines

## Setting up Azure App Services

### Set up Deployment Slots

#### Allow for Testing

## Managing Connection Strings

## Managing Application Settings

# Linking your Internal Network to Azure

Often organizations are migrating to azure and need to create a hybrid setup.  This section discusses how to setup the azure network infrastructure that is needed to create a hybrid network.




