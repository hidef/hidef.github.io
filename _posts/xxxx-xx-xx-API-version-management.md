# Take Back Control of your APIs


## The Lay of the Land


Aging monoliths
Desktop Software
Web applicationsr
Back End Services
Highly distributed microservices

How would you describe your systems?
SOA
Microservices
Distributed Monolith

How many services do you have in your platform?
1-10
10-100
100+

Code might live for years.
Consumers in maintenance mode.
Many consumers -> Many Legacy Consumers -> supporting multiple contracts

Not Version Control Mechanisms:

- URL: `https://nowhere.com/api/v2/cats`
- Custom Request Header: `My-Version: 3`
- Accept Header: Accept: `application/vnd.nowherecats.v2+json`

But Version Management Strategies
Code might live for years.
Consumers in maintenance mode.

## 1 Organic Growth
Add fields when you need them, forget about them when you don’t.
Why do we do this?
Fast
Easy
Zero Design
Null Implementation
Not worth the effort of making a breaking change for just one more field

## 1 Organic Growth
Thousand line long files
Redundant fields
Mystery legacy fields
Single element arrays
Confusing/Reused variable names
Duplicate fields with different types
Misplaced fields
Dumping ground for new fields - like ever growing SQL tables.
Redundant: fields you don’t (meaningfully) populate but don’t know if you can remove.
Mystery Legacy fields: populated with a value that doesn’t seem to correspond to its name.
Single Element Arrays: Was an array once, but only ever has a single value now.
Stupid Variable Names: Bugs as features or reused fields
Duplicate fields with different types: string[] ProductIds & Product[] Products
Misplaced fields: In the wrong place (should have been grouped differently)

Standard tech debt stuff





## 1 Organic Growth
De Facto
Necessary Evil
Dumping ground for new fields - like ever growing SQL tables.
Redundant: fields you don’t (meaningfully) populate but don’t know if you can remove.
Mystery Legacy fields: populated with a value that doesn’t seem to correspond to its name.
Single Element Arrays: Was an array once, but only ever has a single value now.
Stupid Variable Names: Bugs as features or reused fields
Duplicate fields with different types: string[] ProductIds & Product[] Products
Misplaced fields: In the wrong place (should have been grouped differently)

Standard tech debt stuff





## 2 The Clean Start
New endpoint
New API

## 2 The Clean Start
New distinct requirements
New consumer doesn’t need compatibility
Different projection of the same data
Different datasource
Different technical requirements
Want to use new technologies
New requirements are big enough to require significant work
Different Datasource: new DB or event stream has similar but different data
Might want a cache, or to decouple from datasource	

## 2 The Clean Start
Old world/New world 
Unkillable legacy code
Duplicate logic
Inconsistent logic
Old world left to rot
Failure to migrate legacy consumers means that old world i still strongly needed
Duplicate Logic: copying = more to maintain, rewriting = more to maintain + regression bugs
Inconsistent logic: new code might have a better source of data and “bug fixes” become divergence

## 2 The Clean Start
Fun
Satisfying
Risks doubling your problems
Old world left to rot
Failure to migrate legacy consumers means that old world i still strongly needed
Duplicate Logic: copying = more to maintain, rewriting = more to maintain + regression bugs
Inconsistent logic: new code might have a better source of data and “bug fixes” become divergence

## 3 Compatibility Layer
Transform your output:
Hide new values
Provide fallback

## 3 Compatibility Layer
Decorate on a field by field basis

## 3 Compatibility Layer
Contract models contains all version configuration
Cannot deprecate fields in contract definitions
Contract code becomes confusing 

Thousand line long files
Single element arrays
Stupid variable names
Duplicate fields with different types
Misplaced fields

Not: mystery legacy fields
Not: Redundant fields (well, maybe less so)

Fields added in later versions may not apply in earlier versions of the same state(e.g. DeliveryOnItsWay has DepartedAt, but prior to OIW it was “Accepted” and “DepartedAt” means nothing, but may still have a value)



## 3 Compatibility Layer
Actually supports multiple versions
Doesn’t help clean up legacy code
Tied to the current tech
Thousand line long files
Single element arrays
Stupid variable names
Duplicate fields with different types
Misplaced fields

Not: mystery legacy fields
Not: Redundant fields (well, maybe less so)

Fields added in later versions may not apply in earlier versions of the same state(e.g. DeliveryOnItsWay has DepartedAt, but prior to OIW it was “Accepted” and “DepartedAt” means nothing, but may still have a value)



## 4 The Mapping Chain
“Compatibility Layer Plus”
Copy and evolve
Add a bidirectional mapping to/from the previous version.
Requests for older versions will just need to be mapped back repeatedly until the data is mapped to the requested contract version.


Demo Time
Caveats:
No Input mapping
Could be nicer registration of config & tooling

## 4 The Mapping Chain
Breaking changes are cheap (tidying up is easy)
Legacy fields only exists in old contract definitions
Legacy logic only exists in the mapper that removed it (i.e. provided a default value when the original logic was removed)
Legacy tests can still work against legacy contracts
Keeps your contracts clean of version information

## 4 The Mapping Chain
Hundreds of mappers
Hundreds of contract versions
Tied to the current tech
Challenges around versioning different resources
Apparent duplication = change blindness?


## In Closing

Adopting a proactive approach => Agility
Either preserve legacy code, or kill it, but don’t let it fester
Paying off tech debt is Subscription vs One Time Payment Model
Don’t think that you can version your data without versioning structure

Have a plan for how you are going to EOL legacy code/contracts.

## Notes

Proof of Mapping Chain Concept: https://github.com/uatec/mappingchaindemo 
