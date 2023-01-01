# Failures

Systems fail, this document classifies failures and what to do about them. Failures are ordered by seriousness of the situation, but too often emphasized in reverse because of visibility and number of occurrences. The purpose of this document is to help guide and explain system design.

This document is written from a software centered perspective, but software does not exist in a vacuum, without the hardware and people involved, so it generalize to systems software developers build.

Failures can be intentional when there is a conflict of interest. What is a failure for one party may be an intent of an other. Systems could be designed to prefer certain interests over others.

Failures causing immense social harm is outside the scope of this document. We are likely to see a number of such examples in our lifetime where problematic software is involved. No single fault, in any person or thing, should be allowed to cascade to such immensity. Therefor, such a fault is a failure of social norms and regulatory frameworks.

The codes associated with failures holds no meaning outside this document, and maybe re-indexed on update.

## General rules

1. The best prevention is to be so simple that all behavior is obvious.
2. Failures should be automatically mitigated when possible, for example, by presenting a less harmful failure.
3. Do not proceed after a partial failure unless absolutely necessary.

## Data Leakage (-2)

Data leakage is the worst kind of failure because it is un-recoverable. A data leak is leaked forever so the consequences may also be immeasurable. Even anonymized data is not guaranteed to be safe. According to information theory, a dataset can not be truly anonymized, because we can not control what other datasets an attacker may have access too, any additional information could unlock data that an attacker could not previously access.

### (-2) Prevention

Do not ask or keep private data unless absolutely necessary. Data should be scoped to it's intended usage and securely deleted after use.

Minimize attack surfaces.

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

### (-1) Detection

### (-1) Mitigation

### (-1) Intentional failures

- To lie.
- To censor data.
- Fictitious entry as copyright traps.

## Denial of Service (0)

### (0) Prevention

### (0) Detection

Quilt obvious when it happens, but there are too classes:

- Wait until giving up
- Immediate response

### (0) Intentional failures

- 410 Service deprecated or shut down.
- 451 Unavailable for legal reasons.

## Partial Degradation (1)

### (1) Intentional failures

- Remove parts of the service to conserve resources.

## Anti Designs

### The internal network is secure

### Microservices does partial degradation well

It could, but not automatically, nor should it in all cases. A monolith can also handle partial degradation if designed for it.

### Infinite scaling and runaway cost
