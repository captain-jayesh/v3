# How to implement an F# concept exercise

This document describes how to implement a concept exercise for the F# track.

**Please please please read the docs before starting.** Posting PRs without reading these docs will be a lot more frustrating for you during the review cycle, and exhaust Exercism's maintainers' time. So, before diving into the implementation, please read the following documents:

- [The features of v3][docs-features-of-v3].
- [Rationale for v3][docs-rationale-for-v3].
- [What are concept exercise and how they are structured?][docs-concept-exercises]

Please also watch the following video:

- [The Anatomy of a Concept Exercise][anatomy-of-a-concept-exercise].

As this document is generic, the following placeholders are used:

- `<SLUG>`: the slug of the exercise in kebab-case (e.g. `calculator-conundrum`).
- `<NAME>`: the name of the exercise in PascalCase (e.g. `CalculatorConundrum`).
- `<CONCEPT_SLUG>`: the slug of one of the exercise's concepts in kebab-case (e.g. `anonymous-methods`).

Before implementing the exercise, please make sure you have a good understanding of what the exercise should be teaching (and what not). This information can be found in the exercise's GitHub issue. Having done this, please read the [F# concept exercises introduction][concept-exercises].

To implement a concept exercise, the following files must be added:

<pre>
languages
└── fsharp
    ├── concepts
    |   └── &lt;CONCEPT_SLUG&gt;
    |       ├── about.md
    |       └── links.json
    └── exercises
        └── concept
            └── &lt;SLUG&gt;
                ├── .docs
                |   ├── introduction.md
                |   ├── instructions.md
                |   ├── hints.md
                |   └── source.md (required if there are third-party sources)
                ├── .meta
                |   |── config.json
                |   |── design.md
                |   └── Example.fs
                ├── &lt;NAME&gt;.fs
                ├── &lt;NAME&gt;.fsproj
                └── &lt;NAME&gt;Tests.fs
</pre>

## Step 1: Add code files

The code files are track-specific and should be designed to help the student learn the exercise's concepts. The following F# code files must be added (not necessarily in this order):

### Add `<NAME>.fs` file

**Purpose:** Provide a stub implementation.

- The stub implementation's code should compile. The only exception is for exercises that introduce syntax we _want_ a student to define themselves, like how to define a class or property. In this case, insert a descriptive TODO comment instead of providing stub code (see [this example][todo]).
- Stub functions should use the `failwith` function which message contains the function to implement (see [this example][failwith]).

For more information, please read [this in-depth description][stub-file], [watch this video][video-stub-file] and check [this example stub file][example-stub-file].

### Add `<NAME>Tests.fs` file

**Purpose:** The test suite to verify a solution's correctness.

- [xUnit][xunit] is used as the test framework.
- [FsUnit][fsunit] us used as the assertion library.
- Only use `Fact` tests; don't use `Theory` tests.
- All but the first test should be skipped by default (check [this example][skip-fact]).

For more information, please read [this in-depth description][tests-file], [watch this video][video-tests-file] and check [this example tests file][example-tests-file].

### Add `<NAME>.fsproj` file

**Purpose:** The project file required to build the project and run the tests.

For more information, check [this example project file][example-project-file].

### Add `.meta/Example.fs` file

**Purpose:** The idiomatic example implementation that passes all the tests.

For more information, please read [this in-depth description][example-file], [watch this video][video-example-file] and check [this example file][example-example-file].

## Step 2: Add documentation files

How to create the files common to all tracks is described in the [how to implement a concept exercise document][how-to-implement-a-concept-exercise].

## Step 3: Update list of implemented exercises

- Add the exercise to the [list of implemented exercises][implemented-exercises].

## Step 4: format code

To format the exercise's code, follow these steps:

- Open a command prompt in the `language/fsharp` directory.
- Run `./format.ps1 <SLUG>`. This script will format the code using the [`fantomas` tool][fantomas].

## Step 5: Add analyzer (optional)

Some exercises could benefit from having an exercise-specific analyzer. If so, specify what analysis rules should be applied to this exercise and why.

_Skip this step if you're not sure what to do._

## Step 6: Add representation (optional)

Some exercises could benefit from having an custom representation as generated by the [F# representer][representer]. If so, specify what changes to the representation should be applied and why.

_Skip this step if you're not sure what to do._

## Inspiration

When implementing an exericse, it can be very useful to look at already-implemented F# exercises like the [cars-assemble][concept-exercise-cars-assemble] or [log-levels][concept-exercise-log-levels] exercise. You can also check the exercise's [general concepts documents][reference] to see if other languages that have already implemented an exercise for that concept.

## Help

If you have any questions regarding implementing this exercise, please post them as comments in the exercise's GitHub issue.

[concept-exercises]: ../exercises/concept/README.md
[how-to-implement-a-concept-exercise]: ../../../docs/maintainers/generic-how-to-implement-a-concept-exercise.md
[docs-concept-exercises]: ../../../docs/concept-exercises.md
[docs-rationale-for-v3]: ../../../docs/rationale-for-v3.md
[docs-features-of-v3]: ../../../docs/features-of-v3.md
[anatomy-of-a-concept-exercise]: https://www.youtube.com/watch?v=gkbBqd7hPrA
[reference]: ../../../reference
[fantomas]: https://github.com/fsprojects/fantomas
[implemented-exercises]: ../exercises/concept/README.md#implemented-exercises
[concept-exercise-cars-assemble]: ../exercises/concept/cars-assemble
[concept-exercise-log-levels]: ../exercises/concept/log-levels
[allowing-fork-pr-changes]: https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/allowing-changes-to-a-pull-request-branch-created-from-a-fork
[implemented-exercises]: ../exercises/concept/README.md#implemented-exercises
[skip-fact]: ../exercises/concept/log-levels/LogLevelsTests.fs#L11
[xunit]: https://xunit.net/
[fsunit]: https://fsprojects.github.io/FsUnit/index.html
[failwith]: ../exercises/concept/log-levels/LogLevels.fs#L3
[todo]: ../exercises/concept/lucians-luscious-lasagna/LuciansLusciousLasagna.fs
[stub-file]: ../../../docs/concept-exercises.md#stub-implementation-file
[tests-file]: ../../../docs/concept-exercises.md#tests-file
[example-file]: ../../../docs/concept-exercises.md#example-implementation-file
[video-stub-file]: https://www.youtube.com/watch?v=gkbBqd7hPrA&t=1171
[video-tests-file]: https://www.youtube.com/watch?v=gkbBqd7hPrA&t=1255
[video-example-file]: https://www.youtube.com/watch?v=gkbBqd7hPrA&t=781
[example-stub-file]: ../exercises/concept/log-levels/LogLevels.fs
[example-tests-file]: ../exercises/concept/log-levels/LogLevelsTests.fs
[example-example-file]: ../exercises/concept/log-levels/.meta/Example.fs
[example-project-file]: ../exercises/concept/log-levels/LogLevels.fsproj
