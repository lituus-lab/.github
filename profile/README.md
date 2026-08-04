# lituus-lab

## What is lituus-lab?

**lituus-lab** is my personal software laboratory: a collection of libraries
and applications developed around a common philosophy rather than a single
domain. Topics include mathematics, geometry, personal information
management (PIM), music, media, graphics, and other areas that I find
interesting to explore.

Each project is developed independently in its own repository. This
`.github` repository serves as an entry point to the ecosystem and
documents the ideas that connect the projects together.

Although these libraries cover very different subjects, they all share the
same goals: consistency, readability, portability, and pedagogy.

---

## Origins

Most of these projects did not start from scratch.

Long before *lituus-lab* existed, I had already experimented with many of
these topics through C libraries, Python prototypes, Rust experiments, and
later Nim. One of the earliest influences was Kyle Loudon's
*Mastering Algorithms in C*, which inspired me to write
[Dyabl](https://github.com/lbartoletti/dyabl) as a programming exercise.
Many years later, that same curiosity evolved into a larger ecosystem.

The "Uni" prefix originally stood for **Unified** and **Universal**.
Rather than producing isolated libraries with different APIs and coding
styles, the objective is to build a coherent collection that shares common
principles, conventions, documentation, and design decisions across every
project.

---

## Philosophy

The purpose of these libraries is **not** to invent new algorithms.

Most of the algorithms implemented here are well-established and have been
described for years—sometimes decades—in textbooks, academic papers,
language specifications, technical reports, or existing open-source
projects.

The originality of *lituus-lab* lies elsewhere:

* implementing algorithms in pure Nim whenever practical;
* providing several implementations of the same family of algorithms,
  rather than selecting only a single approach;
* exposing consistent and predictable APIs across projects;
* writing code intended to be understandable and educational;
* documenting not only *how* something works, but also *why* it is
  implemented that way.

Whenever a problem admits multiple classical solutions, the goal is often
to implement **most, if not all, of them**. This allows users—and myself—to
study their trade-offs, compare their behaviour, benchmark them, and choose
the implementation that best fits a particular use case.

The libraries therefore aim to become collections of reference
implementations rather than minimal wrappers around one "best" algorithm.

Existing libraries frequently serve as behavioural references ("oracles")
for validation, while textbooks and published algorithms provide the
theoretical foundations. Implementations are written independently rather
than mechanically translated from another code base.

---

## A Pure Nim Ecosystem

One of the long-term objectives is to build a coherent ecosystem written in
**pure Nim**.

Whenever possible, projects avoid external runtime dependencies in favour
of implementations developed within the ecosystem itself. This has several
advantages:

* easier portability;
* simpler builds;
* predictable behaviour across platforms;
* better understanding of the underlying algorithms;
* complete control over implementation choices.

External libraries are used when they genuinely provide capabilities that
would be unreasonable to reimplement, but unnecessary dependencies are
avoided whenever practical.

Over time, libraries naturally build upon one another, allowing the
ecosystem to remain largely self-contained.

---

## Organization

Projects are grouped by topic but are designed to complement each other.

Libraries share common conventions regarding:

* naming;
* project layout;
* documentation;
* testing;
* benchmarking;
* bindings;
* continuous integration.

The intention is that moving from one library to another should feel
familiar, regardless of the problem domain.

---

## Technical Choices

### Nim, with C and Python bindings

Every library is primarily developed in
[Nim](https://nim-lang.org/).

Whenever appropriate, projects expose:

* a native Nim API;
* a stable C API;
* Python bindings generated through Cython.

Continuous integration builds and publishes binaries and Python wheels for
Windows, macOS, and Linux.

After experimenting with several languages over the years, Nim eventually
proved to be the best fit for this kind of work. It combines a readable,
high-level syntax with performance close to C while remaining remarkably
easy to compile and deploy.

Its ability to generate efficient C code also makes it particularly well
suited for producing stable C APIs that can be reused from virtually any
language.

---

## Development Process

The earliest versions of these projects were entirely handwritten.

Over the years they evolved through numerous rewrites, experiments,
prototypes, and abandoned ideas. Many implementations existed long before
their current repositories were created.

The arrival of Large Language Models (LLMs) and coding agents introduced a
new development tool—not a replacement for software engineering.

Today, these tools are used throughout the development process in many
different ways:

* discussing architecture;
* exploring alternative implementations;
* generating repetitive boilerplate;
* proposing refactorings;
* improving documentation;
* reviewing existing code;
* comparing algorithms;
* accelerating experimentation.

Their level of involvement naturally varies from one project to another.

AI-generated code is **never considered authoritative**. It is treated as a
proposal that must earn its place through review, testing, benchmarking,
comparison with trusted references, and, when necessary, complete rewriting.

Likewise, documentation produced with AI is systematically reviewed before
publication.

The objective is not simply to write software faster. Instead, AI allows
more time to be invested where it matters most:

* architecture;
* correctness;
* documentation;
* portability;
* testing;
* educational value.

Every released library remains the responsibility of its maintainer.

---

## Quality and Validation

Because these libraries primarily implement known algorithms, correctness
matters more than novelty.

Depending on the project, implementations are validated through a
combination of:

* unit tests;
* regression tests;
* property-based tests;
* benchmarks;
* comparisons against trusted reference implementations;
* comparisons against published results or specifications.

Reference libraries are frequently used as behavioural or numerical
oracles, but they are not treated as implementation sources.

Quality is therefore measured by correctness, consistency, portability, and
maintainability rather than by the speed at which code can be generated.

---

## About the Git History

One consequence of modern development workflows deserves to be explained.

Some repositories may show a relatively short, linear Git history, with
large commits appearing over a short period of time.

This should not be interpreted as the projects having been conceived and
implemented from scratch within a few days.

Most repositories represent the latest iteration of work that often spans
many years of experimentation, handwritten prototypes, previous libraries,
partial rewrites, discarded approaches, and accumulated experience.

LLMs and coding agents have been used to perform large-scale
rewrites or consolidations of this earlier work, producing repositories
whose visible history is much shorter than the history of the ideas they
contain.

The Git history reflects when the current implementation was committed—not
when the underlying work began.
