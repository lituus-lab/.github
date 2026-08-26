<!-- SPDX-License-Identifier: Apache-2.0 -->
<!-- Copyright 2026 lituus-lab -->
# Shared workflows

Workflows held once here instead of copied into every repository.

**Nothing here acts on a repository that does not call it.** A workflow
reachable through `uses:` is inert until something uses it. The only contents
of this repository that reach the whole organisation on their own are the
profile README and the default community health files — workflows are not
among them. A project whose CI has a different shape keeps its own, and is
unaffected by what lives here.

## `uni-nim-library.yml`

The CI every `Uni*` engine runs: Nim, the C ABI and Python each across the
runner matrix, then jobs that rebuild against the published artifacts on a
machine with no Nim, so what ships is what was tested. Plus lint, docs,
coverage, SPDX, DCO, and a canary that must fail.

Thirteen of the sixteen published libraries had the same eleven jobs,
differing by forty to sixty lines of `diff` — and reading them, the difference
was almost entirely the library's name. That is why this is one file with a
handful of inputs rather than a framework.

### Calling it

```yaml
jobs:
  ci:
    uses: lituus-lab/.github/.github/workflows/uni-nim-library.yml@<commit-sha>
    permissions:
      contents: read
      pages: write
      id-token: write
    with:
      library: UniChecksum
      module: unichecksum
      python-smoke-test: py/tests/test_checksums.py
```

Pin by commit SHA. A moving ref here would be the same unpinned dependency the
family forbids everywhere else, and Dependabot updates these `uses:` like any
other action.

### Inputs

| Input | Required | What it names |
|---|---|---|
| `library` | yes | PascalCase: `UniChecksum`. Gives `include/<library>.h`, `lib<library>.*`, and the artifact names. |
| `module` | yes | The same name in lower case: `unichecksum`. Names the Python import, `tests/c/test_<module>.c`, and the wheel artifacts. The PyPI distribution is `lituus-<module>`; the import name is not namespaced. |
| `python-smoke-test` | yes | The test copied outside the checkout, to prove the installed wheel stands alone. |
| `nim-version` | no | Default `2.2.10`. |
| `os` | no | JSON array. Default all three runners. |
| `python-versions` | no | JSON array. Default 3.10 to 3.14. Without `Py_LIMITED_API` each CPython minor has its own C ABI, so each needs its own run. |
| `publish-pages` | no | Default false. Across the family every one of these deployments reports success while every site answers 404 and no Pages build is ever recorded; a job that is red forever teaches everyone to ignore red. |

### What a caller must have

The workflow runs the repository's own tooling, so these have to be there. A
repository started from UniTemplate has them all; one that predates this
should be checked before it calls.

| Path | Used by |
|---|---|
| `tools/gate.nim` | every task call |
| `tools/hooks/spdx_check.sh`, `tools/hooks/dco_check.sh` | the SPDX and DCO jobs |
| `tools/vgraph.nim`, `tools/lint.nim` | `checkVGraph`, `lint` |
| `tests/c/test_<module>.c` and its `Makefile` | the artifact consumer |
| `py/notebooks/quickstart.ipynb` | the wheel consumer |
| `include/<library>.h` | the artifact consumer |

Plus the nimble tasks it calls by name: `testCi`, `testCiRelease`, `example`,
`ctest`, `cexample`, `clib`, `pyLib`, `lint`, `checkVGraph`, `docsDeps`,
`docs`, `coverage`, and `canary` — which must fail.

### What the caller keeps

The **final check**. A job that has `uses:` cannot also have `steps:`, so a
repository with work of its own puts it in a separate job — and only the
caller knows what its own jobs are. `all-green` therefore lives there, over
the call and anything beside it, and is the single check branch protection
requires: a name that never has to change again.

The **task gate**. `nimble` exits 0 even when an `exec` inside a task failed,
so this workflow calls every task through the repository's own
`tools/gate.nim`, which reads the task's success marker instead. A repository
without that tool cannot use this workflow — which is the point: it is what
makes a red run possible at all.
