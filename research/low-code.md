# Low Code

<https://github.com/topics/low-code>

Personal defination: A data storage and processing solution that is highly customizable without learning programming abstractions.

Low/no-code have a bad reputation, the marking is concentrated on not needing developers. This targets users who don't care about technical details and creates a bad feedback loop. It also implies low code is for less important jobs. But there are some lessons we can learn and apply to building complex business applications.

## What is low code?
The most common low code (or any program used a work) is excel. Half of low code is a SaaS for online spreadsheets, the other half uses UI to pretend it's not.

From this perspective, the most important improvement on excel, other than moving online, is adding column and table metadata. This is familler to anyone who have worked with SQL, defining types and indexes declartively, in contrast to writing code that procedurally uses datastractures directly. By stated purpose, SQL is limited to serving the storage layer (citation needed). A low code solution addes transport and front layer metadata.

## The ideal case
The domain knowleage is sufficiently described by metadata, which the system uses to produce the correct behaviour. 

## trade offs

### metadata complexty vs feature coverage
If metadata is turing complete, then it theoretically have full feature coverage. But a turing complete metadata formate is just an other programing language. This defeate low code promise. It would be better to intergrate with a real programming environment that building it's own.

### strictness vs ease of use
A strict system minimizes bad data entering into the system, and avoids unexpected or untest behaviour. But this requires some forthought and complicates future extension. A system that targets both modes of operation is more complicated and less coherent.

### general vs domain/tech stack specific
Start with specific move to a more general description later on. Nothing is trade off since the general can always cover the specific, allowing futuring compatbilty. General may feel right, but uncessery and hard to get right on first try.

## Banifits of using low code or metadata design as a base platform

