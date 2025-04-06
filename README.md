# Spec: Technical Debt Tracing v0.0.1

A set of rules for keeping track of code-level technical debt in Uqido code-base repositories.

## Dependencies

- https://github.com/Uqido/spec-specification-repository/tree/0.0.1

## Adoption Impact

Software production processes—like any economic production process—generate both credit and debt as byproducts of value creation.
**Both of these byproducts can be either desirable or undesirable**.  
Debt, in particular, is beneficial when it is sustainable and contributes to value creation.
It becomes problematic when it cannot be repaid or leads to inefficiencies in production.  
Therefore, how a team manages debt is a crucial factor in its ability to create value efficiently.

Since technical debt primarily concerns the *future* impact of today’s decisions, the first priority for any team managing it is to keep track of it.  
While most technical debt is tracked in team work management tools—alongside the relevant stories and tasks—there is still a need to track debt at
the **code-level**, directly tied to specific sections of code or individual software components.

Developer teams often signal such debt using unstructured, loosely defined comments like TODOs or FIXMEs. This makes it difficult to understand the nature—and therefore the desirability—of these technical decisions, leading to ambiguity and misinterpretation, especially for new team members or external collaborators.

This specification standardizes the syntax and semantics of code comments to:
- Make all team members aware of the intended *future impact* highlighted by the author
- Help both human and AI reviewers easily identify and prioritize these comments
- Enable both human and AI systems to compute code-level debt metrics

## Normative Content

Technical debt comments **shall** follow one of the following forms:

```
# IMPROVE: comment 
# PENDING: comment
```

in the syntax above, the `#` **will** be replaced with your language one-line or multi-line comment character sequence of choice.

Both IMPROVE and PENDING comments signal that a variant of some piece of code exists with more desirable technical characteristics.
They differ in the reasons why the final code had been chosen:
- IMPROVE: the improved version has been deferred due to effort constraints, yet the provided solution still satisfy the acceptance criteria, now and in the foreseeable future.

  *examples*:
  - this piece of code is pessimized, it's quadratic, it could be logN ... yet in this stage of the project the quadratic version suffices (or it's even faster in absolute terms), so we choose the quadratic, commenting that an improved log version exists but is not necessary.
- PENDING: the pending version has been deferred due to lack of information, the risk and cost of overengineering is too high.

  *examples*:
  - an API controller requires in-depth validation of the parameters, but the API is unstable and under-specified, the meaning and structure of the parameters will probably change soon.

Neither of these comments **should** be used to comment code that will fail acceptance criteria—no FIXMEs, WIPs or the like—such choices should be managed at team level instead.
