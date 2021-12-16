# GIT NAMING CONVENTIONS AND BEST PRACTICES 

### Branch Naming

Branches created should be named using the following format:

```
{story type}-{2-3 word summary}
```

`story-type` - Indicates the context of the branch and should be one of:

- ft == Feature
- bg == Bug
- ch == Chore
- rf == Refactor

`story-summary` - Short 2-3 words summary about what the branch contains

**Example**

```
ft-blog-rest-endpoints
```

### PR Naming

The PR title should be named using the following format:

```
# Story Short description
```

**Example**

```
Build out REST Endpoints for Blog (CRUD)
```

### PR Description Template (Markdown)

The description of the PR should contain the  headings of PULL_REQUEST.md


### Commits

Atomic commits should be made with the format:

```
<type>(<scope>): <subject>``<BLANK LINE> <body> <BLANK LINE> <footer>

```

Any line cannot be longer than 100 characters, meaning be concise.

```<type>``` should be:

 * feature
 * bug
 * chore
 * release
 * refactor
 * documentation
 * style
 * test

```<scope>``` should be something specific to the commit change. For example:

costume
 * flight
 * fighting-style
 * fan-base
 * logo and so on.

```<subject>``` text should:

 * use present tense: "save" not "saved" or "saving"
 * not capitalize first letter i.e no "Carry to safety"
 * not end with a dot (.)

**Message body (optional)** If a body is to be written, it should:

 * written in present tense.
 * include the reason for change and difference in the previous behaviour


chore(coveralls):add coveralls yml  

# Rules

* No more than two commits per branch or in a PR .


