# `wasi-sql`

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

`wasi-messaging` is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/main/Proposals.md#phase-1---feature-proposal-cg).

### Champions

- [Dan Chiarlone](https://github.com/danbugs)
- [David Justice](https://github.com/devigned)
- [Jiaxiao Zhou](https://github.com/Mossaka)

### Phase 4 Advancement Criteria

`wasi-sql` should have at least two implementations (i.e., from service providers, and or cloud providers), and, at the very minimum, pass the testsuite for Windows, Linux, and MacOS.

## Table of Contents

- [Introduction](#introduction)
- [Goals [or Motivating Use Cases, or Scenarios]](#goals-or-motivating-use-cases-or-scenarios)
- [Non-goals](#non-goals)
- [API walk-through](#api-walk-through)
  - [Use case 1](#use-case-1)
  - [Use case 2](#use-case-2)
- [Detailed design discussion](#detailed-design-discussion)
  - [[Tricky design choice 1]](#tricky-design-choice-1)
  - [[Tricky design choice 2]](#tricky-design-choice-2)
- [Considered alternatives](#considered-alternatives)
  - [[Alternative 1]](#alternative-1)
  - [[Alternative 2]](#alternative-2)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

### Introduction

[The "executive summary" or "abstract". Explain in a few sentences what the goals of the project are, and a brief overview of how the solution works. This should be no more than 1-2 paragraphs.]

### Goals [or Motivating Use Cases, or Scenarios]

[What is the end-user need which this project aims to address?]

### Non-goals

[If there are "adjacent" goals which may appear to be in scope but aren't, enumerate them here. This section may be fleshed out as your design progresses and you encounter necessary technical and other trade-offs.]

### API walk-through

[Walk through of how someone would use this API.]

#### [Use case 1]

[Provide example code snippets and diagrams explaining how the API would be used to solve the given problem]

#### [Use case 2]

[etc.]

### Detailed design discussion

[This section should mostly refer to the .wit.md file that specifies the API. This section is for any discussion of the choices made in the API which don't make sense to document in the spec file itself.]

#### [Tricky design choice #1]

[Talk through the tradeoffs in coming to the specific design point you want to make.]

```
// Illustrated with example code.
```

[This may be an open question, in which case you should link to any active discussion threads.]

#### [Tricky design choice 2]

[etc.]

### Considered alternatives

[This section is not required if you already covered considered alternatives in the design discussion above.]

#### [Alternative 1]

[Describe an alternative which was considered, and why you decided against it.]

#### [Alternative 2]

[etc.]

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

[This should include a list of implementers who have expressed interest in implementing the proposal]

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- [Person 1]
- [Person 2]
- [etc.]
