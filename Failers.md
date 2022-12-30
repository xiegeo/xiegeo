# Failers

Systems fail, this document classifies failers and what to do about them. Failers are ordered by seriousness of the situation, but too often emphasized in reverse because of visibility and number of occurrences. The purpose of this document is to help guide and explain system design.

This document is written from a software centered perspective, but software does not exist in a vacuum, without the hardware and people involved, so it generizes to systems software developers build.

Failers can be intentional when there is a conflict of interest. What is a failer for one party may be an intent of an other. Systems could be designed to prefer certain interests over others.

Failers causing immense social harm is outside the scope of this document. We are likly to see a number of such examples in our lifetime where problematic software is involued. No single failt, in any person or thing, should be allowed to cascade to such immensity. Therefor, such a failt is a failer of social norms and regulatory frameworks.

The codes assoiated with failers holds no meaning outside this document, and maybe re-indexed on update. 

## General rules

1. The best prevention is to be so simple that all behavior is obvious. 
2. Failers should be automatically mitigated when possible, for example, by presenting a less harmful failer.
3. Do not proceed after a partial failer unless absolutely necessary.

## Data Leakage (-2)
Data leakage is the worst kind of failer because it is un-recoverable. A data leak is leaked forever so the consequences may also be immeasurable. Even anonymized data is not guaranteed to be safe. According to information theory, a dataset can not be truely anonymized, because we can not control what other datasets an attacker may have access too, any addtional information could unlock data that an attacker could not prevously access.

### Prevention
Do not ask or keep private data unless absolutly necessary. Data should be scoped to it's intended usage and securly deleted after use.

Minimize attack surfaces. Minimize network access and service complexty. Prefer physical over software only solutions.

Privacy conscious users will gave fake information when possible. Don't fight againt it, follow rule #2. A data corruption is better than a data leakage, and an obvious data corruption is better than a hidden one.

### Detection


### Mitigation
Give immediant discloser, so those effected can take evasive action. Organizations are typically reluctant because of the difficulty of evaluating the scope of data leakage and negative publicity.

### Intentional failers

- By legal order.
- By whistleblower.
- Secondary use.

## Data Corruption (-1)
A data corruption error could lead to suboptimal or delayed decision making.

### Intentional failers

## Denial of Service (0)

### Wait until giving up (0A)

### Immediate response (0B)

### Intentional failers

- 410 Service deprecated or shut down.
- 451 Unavailable for legal reasons.

## Partial Degradation (1) 

### Intentional failers

- Remove parts of the service to conserve resources.

## Anti Designs

### The internal network is secure

### Microservices does partial degradation well
It could, but not automatically, nor should it in all cases. A monolith can also handle partial degradation if designed for it.
