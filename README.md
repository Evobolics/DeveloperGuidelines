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

# Continuous Integration

# Continuous Delivery

## Moving Beyond Virtual Machines

## Setting up Azure App Services

## Managing Connection Strings

## Managing Application Settings

# Linking your Internal Network to Azure

Often organizations are migrating to azure and need to create a hybrid setup.  This section discusses how to setup the azure network infrastructure that is needed to create a hybrid network.




