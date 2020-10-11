# Scaling the Developer Toolkit Team: Writing Code that Writes Code
Maintaining multiple active projects is difficult at baseline, especially when those projects have their own dependencies. For many projects driven by external APIs, new features often become available upstream and then need to be built into the downstream projects.  With a large enough feature set, this can quickly become a cumbersome process. To keep up with feature demand and still maintain a minimal amount of tech debt, a team could add additional engineers. But this presents another problem - you’re either reallocating engineer time from another team or you’re taking on the cost of adding more engineers.<br >

Another potential way to tackle the team scalability problem is through automation.<br >

In this presentation, we’ll be discussing how the Developer Toolkit team has been working on a code generation tool that leverages GraphQL’s introspection feature in New Relic’s NerdGraph API. Introspection provides the ability to query which resources are available in the API schema, gleaning insight into the available queries, types, fields, query arguments, and directives it supports. Introspection provides enough metadata about the API models for us to automatically generate new feature code in multiple projects.<br >

Code generation with automation facilitates scaling developer productivity, reliability, maintainability, as well as portability, helping our small (yet powerful) team deliver better software for a more perfect internet.

## Prerequisites
1. A New Relic account
> If you dont have an account -  [Free Tier Sign Up Link](https://newrelic.com/signup)
2. Basic CLI knowledge
3. Basic Golang experience is a plus

