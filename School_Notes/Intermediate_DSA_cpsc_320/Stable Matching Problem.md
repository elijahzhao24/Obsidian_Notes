
## Basic Variant (equally sized groups)

Supposed there are two equally sized groups:
-  n applicants 
- n employers
Every applicant ranks all employers, and all employers rank all applicants 

The goal is to get a list of matching, which is a collection of applicant-employer pairs where nobody appears more than once

### Definitions 

**Perfect Matching:** matches everyone exactly once

**Blocking pair:**
```
- a is matched with e'
- e is matched with a'

The unmatched pair (a,e) is a blocking pair when:

1. a prefers e over e′ and
2. e prefers a over a′
```

In other words: They are not currently together, but they would both rather be together than stay with their assigned partners.

> Matchings are stable when there are no blocking pairs

## Gale–Shapley algorithm

```
while an unmatched applicants exists:
    applicants proposes to its next employers

    if employers has no matched applicant:
        employers accepts

    else if macthed employers prefers this applicant:
        employers replaces its current applicant

    else:
        employers rejects the applicant
```

Always stable because: A proposer moves down its preference list, while a receiver’s tentative partner only improves.

**Runtime:** Each employer proposes to each applicant at most once. O(n^2)

## Variant: One side has more than the other

example: 
- m families
- n properties
- n≥m

Every family must receive a property, but some properties may remain empty.

**A valid matching has:**
- every family matched
- each property matched to at most one family
- possibly some empty properties

Multiple ways to solve this:

#### Families as the proposers:
```
while an unmatched family exists:
    family proposes to its next property

    if property is empty:
        property accepts

    else if property prefers this family:
        property replaces its current family

    else:
        property rejects the family
```

#### Properties as the proposers:
```
while there is an unmatched property
      that has not proposed to every family:
      
      property proposes to the next family in its preference
      
      ...
```

#### Dummy participants
We have m families , n properties, where n≥m.

```
Add: n−m dummy families

Preferences: Properties keep their same preferences, with all dummy families afterwards

Matching a property to a dummy essentially means the property is empty

Solve SMP

after solving, keep all real family/house pairs
delete pairs with dummy families, and those properties are empty
```

## Variant: one side accepts multiple people

Suppose:
- residents each need one hospital
- hospital h can accept $k_h$​ residents
- Assume # of residents = total spot of hospitals combined

So for example hospital $h_1$ might accept 2 patients ($k_{h1}$ = 2)

Each resident ranks hospitals, and each hospital ranks residents.

How to solve:

#### Gale–Shapley for Mutiple spots:

```
while an unmatched resident exists:
    resident r proposes to next hospital h

    if h has an empty position:
        h accepts r

    else if h prefers r over its worst current resident:
        h rejects its worst resident
        h accepts r

    else:
        h rejects r
```

#### Reduction from hospital capacities to ordinary SMP:

```
Replace every hospital position with a separate copy.

If hospital h has capacity 3, create:
h^1 h^2 h^3

where each hospital copy gets the same resident ranking, and can only accept one resident.

For resident’s preferred list, all copies of a preferred hospital should appear before copies of a less-preferred hospital. 

```