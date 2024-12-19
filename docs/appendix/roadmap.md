# Roadmap

It doesn't exist a roadmap yet, but the first step is to create a MVP (Minimum Viable Product) with the basic features, so:

- PoC (Proof of Concept) of the language: implement the basic features as a clang plugin
- v0.1: Implement the basic features in the compiler
- v0.2: Implement the standard library
- Until v1.0: Iterate over the language, add new features, remove others, etc.
- v0.9: Feature freeze, only bug fixes
- v1.0: Release, the language is stable

After the v1.0 the development will be separated in two types of releases: 'major' and 'minor'.

- Major releases can introduce breaking changes
- Minor changes only can be bugfixes or patches

With this approach the language don't need to have an 'LTS' version, major versions will be.
In the far future the develop of an v2.0 may start, but it will feel like a new language, not a new version.