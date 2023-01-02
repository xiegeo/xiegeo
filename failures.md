# Failures

Systems fail, this document classifies failures and what to do about them. Failures are ordered by seriousness of the situation, but too often emphasized in reverse because of visibility and number of occurrences. The purpose of this document is to help guide and explain system design.

This document is written from a software centered perspective, but software does not exist in a vacuum, without the hardware and people involved, so it generalize to systems software developers build.

Failures can be intentional when there is a conflict of interest. What is a failure for one party may be an intent of an other. Systems could be designed to prefer certain interests over others.

Failures causing immense social harm is outside the scope of this document. We are likely to see a number of such examples in our lifetime where problematic software is involved. No single fault, in any person or thing, should be allowed to cascade to such immensity. Therefor, such a fault is a failure of social norms and regulatory frameworks.

Each class of failures encapsulate entire fields of study. As such this topic can include unending detail. But humans have limited brain capacity, so drawing parallels without going into detail:

- Data Leakage (-2) include privacy research, intelligence gathering, spy war.
- Data Corruption (-1) include data science (bias detection), coding theory.
- Denial of Service (0) and Partial Degradation (1) include reliability engineering, error handling.

The numbers defined in this document holds no meaning outside this document, and maybe re-indexed on update.

## General rules

1. The best prevention is to be so simple that all behavior is obvious.
2. Failures should be automatically mitigated when possible, for example, by presenting a less harmful failure.
3. Do not proceed after a partial failure unless absolutely necessary.
4. Treat untested code as having undefined behaviour. Undefined behaviour can fail in the worst way imaginable. Therefor, untested code should be replaced by panics instead of released into production.

## Data Leakage (-2)

Data leakage is the worst kind of failure because it is un-recoverable. A data leak is leaked forever so the consequences may also be immeasurable. Even anonymized data is not guaranteed to be safe. According to information theory, a dataset can not be truly anonymized, because we can not control what other datasets an attacker may have access too, any additional information could unlock data that an attacker could not previously access.

### (-2) Prevention

Do not ask or keep private data unless absolutely necessary. Data should be scoped to its intended usage and securely deleted after use.
Just like you would never use code without an undisputed and clearly presented licence, you should never use data without a licence.
The default licence is aways always all rights reserved.

Do not special case data to be more private, special case should only apply to make data less private.
The first consideration of system design is to protect the most private data.

Minimize attack surfaces.

- The less data is used, the less that can be leaked.
- Minimize network access and service complexity. Prefer physical over software only solutions.
- Data should be encrypted, and only services that must read plain text has access to the key.

Privacy conscious users will gave fake information when possible. Don't fight against it, follow rule #2. A data corruption is better than a data leakage, and an obvious data corruption is better than a hidden one.

### (-2) Detection

### (-2) Mitigation

Give immediate discloser, so those effected can take evasive action. Organizations are typically reluctant because of the difficulty of evaluating the scope of data leakage and negative publicity.

### (-2) Intentional failures

- Secondary use.
- By legal order.
- By whistleblower.

## Data Corruption (-1)

A data corruption error could lead to suboptimal or delayed decision making.

Sources of data corruption include input, transformation, and interpretation. The root cause include not only bugs and user errors, but also design (confusing user interface) and happenstance (aging hardware, cosmic ray bit flip).

### (-1) Prevention

Two schools of thought:

1. Systems should prevent bad data from entering to protect it self.
2. Systems should present all data as is so users do not get a false sense of the correctness of data.

Here bad data means data that is in conflict with our data model.

If data source is trustworthy only #1 is needed. Also, if there are other downstream data consumers, #1 is necessary for a well behaving system.

When source is questionable. #2 is preferred. In fact, feed back to data entry should be keeps to a minimum.
This is to avoid biasing the data to fit pre-existing biasing of the system. (see also: [blinded experiment](https://en.wikipedia.org/wiki/Blinded_experiment#In_forensics).) Feed back can improve user experience, filtering can improve data quality, but both might also make the source a better liar.

With a holding place for dirty data, #1 and #2 can be combined to fit both needs.

The result of data transformations should not be used to overwrite the original.

Data should be stored and presented unambiguously in UI and API. Examples of ambiguous data include: time recorded in a local time zone without explicitly recording the time zone; a measurement presented without unit (unit could be part of the field name); and an event recorded without the time and place metadata.

### (-1) Detection

Erroneous data that fits the model is impossible to detect. Usually, such cases are detected by an investigator with additional domain knowledge.

On the other hand, data that does not fit the model could mean two things. The data is wrong, or the model is wrong. The later is a serous situation that should not be ignored.

Make error reporting easy. Correcting data is not urgent to those who can easily identify the mistake, but not correcting is detrimental to those who can not identify it.

### (-1) Mitigation

Data modifications should be reversible, versioned, or logged. This improves usability even without data corruption concerns.

Care must be taken to avoid an conflict with `Data Leakage (-2)`. Protection against data loss is fundamentally trading against leakage.
This is important enough for an example to illustrate:

    A shared online document has auto versioning capabilties, a user paste in a section, but the intended content was not inside the clipboard.
    Instead, unrelated information is pasted. The user quickly deletes the section, but a version with the clipboard data is already saved on the server.

This mean a system must allow all history and backups to be investigated by authors, and allow history to be irreversibly modified or deleted.

### (-1) Intentional failures

- To lie.
- To censor data.
- Fictitious entry as copyright traps.

## Denial of Service (0)

### (0) Prevention

Provide a buffer of availed resource on top of typical usage patterns.

Don't over do it. Define upper limits for resource consumption and deny service when reached. Unless you like paying for things without knowing when or why.
Secure limited liability with your service provider.

Provide software and hardware backups.

Taken to the extreme, this means sourcing redundant software and hardware from different venders.

In typical setups, redundant software mean multiple versions can interoperate, and redundant hardware means the same setup exist in different physical locations.
The assumption is, easily detectable software bugs are unlikely to survive multiple version updates, manufacturing defects are mostly random, and utility outages are local. Quality is better served testing one setup in deeps, that maintaining a diverse ecosystem.

Resource buffers must be considered with redundancy in mind, if peak usage is 60% with 2 locations, then there is no failover since a single location can not serve 120%.

### (0) Detection

Quilt obvious when it happens, but there are too classes:

- Wait until giving up.
- Immediate response.

### (0) Mitigation


### (0) Intentional failures

- 410 Service deprecated or shut down.
- 451 Unavailable for legal reasons.

## Partial Degradation (1)

Really a subtype of `Denial of Service (0)` where only parts of the system denies service.

### (1) Intentional failures

- Remove parts of the service to conserve resources.

## Anti Designs

### The internal network is secure

You might read this in the docs:

>[Because the network connection is private and encrypted, you can generally just talk back and forth without extra authentication until you know you need it; in other words, you can keep things simple.](https://fly.io/docs/app-guides/multiple-processes/#maybe-you-want-multiple-apps-though)

Only to be followed by in their blog:

> [... your app server is behind a security perimeter, and can usually reach things an ordinary Internet user can’t. Because HTTP is a relatively flexible protocol, and URLs are so expressive, attackers can often use SSRF[Server-side request forgery] to reach surprising places;](https://fly.io/blog/practical-smokescreen-sanitizing-your-outbound-web-requests/)

Defend in depth, don't let your network perimeter be the thin shell protecting all your yolk.

A private network offers improved security and provide a buffer for monitoring attacks against high value targets. A private network can not offer security guaranties if any service on the network could be mislead to miss behave. The attack surface is to big. A private network is useless if not monitored for network anomalies.

Using an analogy. Your home is a private and secure place, but you wouldn't trust someone just because they are inside your home.

### Microservices does partial degradation well

> My manager said this is why we are doing microservices. We ended up with a complex web of interdepend services.

It could, but not automatically, nor should it in all cases. A monolith can also handle partial degradation if designed for it.

Choosing the right tech stack can make reaching certain gaols easier. But no tech stack is either sufficient or necessary.

### Infinite scaling and runaway cost

This is a follow up to bad mitigation against DoS. Monitor resource usage before monitor uptime. Especially for expensive API calls.
