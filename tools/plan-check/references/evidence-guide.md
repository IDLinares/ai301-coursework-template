# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

**Where it lives**

- In eval bundle: the candidate plan's diagnosis section (where the cause is stated) compared with the repro-evidence block (where the observed behavior is described)
- In live mode: the draft plan's diagnosis section compared with the issue thread's evidence section

**What good looks like**

The candidate or draft plan's diagnosis statement shows the bug described in the issue's evidence block and accurately explains why the error state in the issue is occurring. The diagnosis must agree with what the repro evidence shows — the stated cause must be traceable to behavior the repro evidence actually demonstrates.

A diagnosis that *contradicts* evidence names a cause that the repro steps or artifacts rule out. A diagnosis that *ignores* evidence names a cause without referencing the repro output at all, as if the evidence were not there. Both fail this check; they fail differently. If this section is missing entirely, treat it as failing the check.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

**Where it lives**

- In eval bundle: the candidate plan's scope statement, specifically the in-scope list, the not-in-scope line, and any files or areas named
- In live mode: the draft plan's scope section, looking for the same three elements

**What good looks like**

The candidate or draft plan's scope statement explicitly names which files are in scope, includes a not-in-scope line that names adjacent files that could be affected but should not be touched, and does not expand beyond those stated boundaries in later sections.

A bounded change touches only the files it named upfront. A drive-by rewrite introduces additional changes — style fixes, refactors, unrelated behavior — beyond what the diagnosis requires, or expands scope mid-description without justification. If the scope section is missing entirely, or exists but names no files, treat it as failing the check.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

**Where it lives**

- In eval bundle: the candidate plan's changes or approach section
- In live mode: the draft plan's changes or approach section

**What good looks like**

The candidate or draft plan's changes or approach section shows a list of steps in the order they should be executed, with files and areas to change explicitly named within each step. The ordering matters independently of the file list — a plan that names all the right files but gives no sequence fails executability.

A stranger can execute it without asking the author anything: no step requires the reader to infer a file path, method name, or decision that the plan does not state. If a step uses a vague phrase like "update the handler" without naming which file or function, it fails this check. If this section is missing entirely, treat it as failing the check.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

**Where it lives**

- In eval bundle: the candidate plan's test plan section, checked against the repro-evidence block's steps and artifacts
- In live mode: the draft plan's test plan section, checked against the issue thread's repro steps and any linked artifacts

**What good looks like**

The candidate or draft plan's test plan section names a test or repro step that verifies the fix. The test must reproduce the exact failure mode the repro evidence showed — not just a similar scenario — so it fails before the fix and passes after.

A decisive test plan names the specific input, the specific wrong output that currently occurs, and the specific expected output after the fix. A vague test plan just says "add a test" or "verify the fix works" without those specifics. The test type (unit, integration, or manual repro step) should match what the bug requires — "unit test" is not always the right vehicle. If the test plan section is missing entirely, treat it as failing the check.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

**Where it lives**

- In eval bundle: the candidate plan's diagnosis and changes/approach sections for unknowns and risks; the plan's comment or revision history for mid-build deviations
- In live mode: the draft plan's diagnosis and changes/approach sections; any updated or amended sections that appeared after the plan was first drafted

**What good looks like**

The candidate or draft plan's diagnosis and changes/approach sections have no claims stated with certainty about behavior that the repro evidence does not support. Speculative claims are explicitly flagged as assumptions or unknowns — e.g., "we assume X because Y is not shown in the repro output."

False confidence states expected behavior as fact without citing evidence. A stated unknown explicitly names the gap and the assumption used to bridge it. Risks — places where the fix could break adjacent behavior — are named, typically in the approach section near the step that introduces them.

If the plan was updated after execution began, an honest deviation appears as an explicit note in the plan itself (not just in a comment) describing what changed and why. If the plan shows no deviations but the repro evidence suggests the original approach would not have worked, that silence is a honesty failure. If neither the diagnosis nor approach section exists, treat it as failing the check.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

**Where it lives**

- In eval bundle: the candidate plan's comment section compared against the plan's stated changes, the repo-facts block (for templates, contributing asks, AI-use disclosure requirements, and contribution policy), and the issue's thread highlights or maintainer signals
- In live mode: the draft plan's comment compared against the same three sources: the plan's stated changes, the repo's contribution docs, and the live issue thread

**What good looks like**

The comment addresses what the issue thread specifically asks for — including any preference or constraint a maintainer stated — and follows the repo's contribution conventions on format, scope, and framing. It only describes changes stated in the plan, and all described changes are relevant to the issue being addressed.

A thread-aware comment references something specific from the issue thread (a maintainer's preference, an existing workaround, a constraint the reporter named). A boilerplate comment could be copy-pasted onto any issue without changing a word — that is the failure mode. Check the repo-facts block for required templates, contributing asks, and AI-use disclosure requirements; a comment that omits a required disclosure or ignores the repo's stated template fails this check even if its content is otherwise accurate. If the comment section is missing entirely, treat it as failing the check.
