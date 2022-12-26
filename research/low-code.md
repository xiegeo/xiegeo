# Low Code

<https://github.com/topics/low-code>

Personal defination: A data storage and processing solution that is highly customizable without learning programming abstractions.

Low/no-code have a bad reputation, the marking is concentrated on not needing developers. This appears to target users who don't care about technical details and creates a bad feedback loop. It also implies low code is for less important jobs. But there are some lessons we can learn and apply to building complex business applications.

## What is the core of low code?
The most common low code (or any program used a work) is excel. Half of low code is a SaaS for online spreadsheets, the other half uses UI to pretend it's not.

From this perspective, the most important improvement on excel, other than moving online, is adding column and table metadata. This is familler to anyone who have worked with SQL, defining types and indexes declartively, in contrast to writing code that procedurally uses datastractures directly. By stated purpose, SQL is limited to serving the storage layer (citation needed). A low code solution addes transport and front layer metadata.

Low code and metadata driven can be considered interchangeable.

## The ideal case
The domain knowleage is sufficiently described by metadata, which the system uses to produce the correct behaviour. 

## trade offs

### metadata complexty vs feature coverage
To have full feature coverage, there for able to build any system, it must be turing complete. But a turing complete metadata formate is just an other programing language. This defeats the low code promise. It would be better to intergrate with a real programming environment that building it's own.

### strictness vs ease of use
A strict system minimizes bad data entering into the system, and avoids unexpected or untest behaviour. But this requires some forthought and complicates future extension. A system that targets both modes of operation is more complicated and less coherent.

### general vs domain/tech stack specific
Start with specific and move to a more general meta formate later on. Nothing is trade off since the general can always cover the specific, allowing futuring compatbilty. General may feel right, but uncessery and hard to get right on first try.

## Banifits of using low code or metadata driven design as a base platform

Many (all?) programing languanges have a reflect feature to look at it's own code as a datasturcture. This is a necessary component of any compiler or run time, and commonly used by data serialization libraries. As such, all code can be considered metadata. But this is not a metadata first approach and deriving intent from code is either difficult or lacking important domain context. Some languages allow code to be marked up with addtion metadata to improve intergation with tooling, but common metadata definations is usually lacking in scope, so such tooling useally define there own without interopartion build in. This makes end to end use difficult.

A metadata design would reverse the situation. Domain driven design and tooling intergration become first parties. But code will target metadata processing first instead of accomplishing tasks directly, increasing complexty of simple tasks by an order of magnitude, and complex tasks must be subdivided into simpler ones. This cost can be amortized, but only when implemnting a highly complex domain, or cross supporting many domains.

Additional benefits of metadata driven design: 
 - A single scource of truth that can be easly processed by people and machine.
 - Clean sepration of interface (domain knowledge) and implementation.
 - Easy mock interfaces and data. Test cover typical and extreme cases.
 - Replace stupidly repetitive glue code between different services.
 - Update domain mode without code change.

## Conclusion

