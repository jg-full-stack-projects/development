# Contributing to the repository

To start contributing we ask of you to read through the commit conventions before starting development, use the resources provided below to read up on the material on top of this document:

- [Commit Message Guidelines](https://www.conventionalcommits.org/en/v1.0.0-beta.2/#summary)

## Commit Message Guidelines

We have very precise rules over how our git commit messages can be formatted. This leads to **more readable messages** that are easy to follow when looking through the **project history**. But also, we use the git commit messages to **generate the change log**.

### Format

Each commit message consists of a **header**, a **description**. The header has a special format that includes a type, a scope and a subject:

```
<type>[(optional scope)]: <description>
```

### Branching

Commits **will not** be made directly to master, instead use appropiate branches for example:

```
feature/xyz

fix/xyz
```

After work is complete submit a **merge request** to put the code up for review before merging through to master. It's a best practice to keep merge requests small, feature/bug specific.

### Examples

```
docs(changelog): update changelog to beta.5
```

```
fix(release): need to depend on latest rxjs and zone.js
```
