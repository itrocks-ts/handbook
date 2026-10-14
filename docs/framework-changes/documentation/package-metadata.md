# Package metadata

Treat the README opening, `package.json.description` and `keywords` as one documentation surface.
Review them together whenever the package's responsibility changes.

## Description

Describe the existing public capability in one phrase, without a trailing full stop.
The first sentence after the README title must reproduce it exactly, adding only the full stop.
Put qualifications in a separate sentence.

Use present tense, a concrete subject and the defining environment only when relevant.
Avoid the package name, version claims, marketing adjectives and secondary feature lists.

## Keywords

Use unique, relevant search terms drawn from the package's capability, operations, platform and technologies.
Include `it.rocks` for framework packages. Prefer 7–15 terms; relevance takes precedence over the count.
Use lowercase except established acronyms; sort alphabetically, ignoring case.
Do not add vague terms, dependency inventories or spelling variants merely to increase the count.

Parse the JSON and check description agreement, keyword uniqueness and ordering after editing.
