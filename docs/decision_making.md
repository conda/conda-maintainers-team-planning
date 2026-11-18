[governance]: https://github.com/conda/governance
[rfc7282]: https://www.rfc-editor.org/rfc/rfc7282
[project-roadmap]: https://github.com/orgs/conda/projects/22/views/15
[cep-9]: https://github.com/conda/ceps/blob/main/cep-0009.md
[contributing]: https://github.com/conda/conda/blob/main/CONTRIBUTING.md
[development-process]: development_process.md

# Decision Making for conda Maintainers

> [!NOTE]
> This page is for current and prospective members of the
> **conda-maintainers** team, not for all contributors.

This page describes how the conda-maintainers team makes decisions on the
repositories they maintain, including conda. Conda Organization governance
(Steering Council, project team membership, voting) is covered in the
[conda governance repository][governance].

## Principles

The conda-maintainers make decisions through rough consensus. Every significant
decision has a named owner who drives it and builds consensus among the
maintainers before it stands. The feature owner proposes the decision; the
maintainers decide it. Community members give input along the way.

Everyone can contribute anywhere in a shared codebase, but not every decision
needs consensus from everyone.

## Roles

- **Feature Owner:** Owns an Epic's sequencing and end-to-end experience and
  builds rough consensus for its decisions.
- **PR author:** Proposes and implements the change.
- **PR reviewer:** Reviews the change and merges it once the review passes.
- **Maintainer:** Participates in review and consensus, and may raise a technical
  blocker.
- **Contributor or community member:** Gives input through issues and PR threads
  but does not block a decision.
- **Planning Lead:** Assigns feature owners for Epics that reach Near on the
  Roadmap board.

A maintainer counts as participating in a decision once they have reviewed the
PR or joined the discussion.

## The feature owner role

When an Epic reaches Near on the Roadmap board, a rotating conda-maintainer
volunteers as its feature owner, accountable for that Epic's sequencing and
end-to-end experience. The feature owner does not do all the work themselves.

The feature owner:

- Sequences the Epic's work into shippable slices and keeps the pieces coherent
- Opens and drives the GitHub issue discussion to gather community input before
  work begins
- Proposes the Epic's technical decisions and carries them to rough consensus;
  Tier 2 proposals stand after the 7-day window in Decision tiers

The role rotates across conda-maintainers so that more people get experience
making these decisions.

## Feature owner assignment

Anyone can create an Epic, but only Epics on the [Roadmap board][project-roadmap]
are planned features. The Planning Lead assigns a feature owner when an Epic moves
from Later to Near on the board. Epics that are off the board or stay in Later
do not get a feature owner. Assignment happens asynchronously on the Epic's
GitHub issue.

1. The Planning Lead comments on the Epic and posts a call for volunteers in
   `#conda-maintainers` on Zulip.
2. Any conda-maintainer can volunteer by commenting on the Epic within five
   business days.
3. If several people volunteer, the Planning Lead picks the one who has led the
   fewest Epics recently.
4. The Planning Lead sets the chosen volunteer as the Epic's assignee, and the
   new feature owner confirms by commenting on the Epic.
5. If nobody volunteers, the Epic stays in Near with no feature owner, and the
   Planning Lead raises it at the next conda-maintainers meeting.

## Decision tiers

### Tier 1: PR and story-level decisions

Most changes fall here. A maintainer reviews the PR, approves it, and merges it.
Community members commenting on the PR are providing input.

Request a review from a maintainer, preferably the person you worked with during
development. See [Development Process][development-process] for the review
rules.

### Tier 2: Feature-level architectural decisions

Tier 2 covers changes that alter a contract other projects rely on:
backwards-incompatible changes and [deprecation schedules][cep-9], public APIs
including plugin APIs, support commitments such as supported platforms and
dependency floors, and shared architecture that the ecosystem builds on. Routine
bug fixes, performance work, and platform-specific fixes stay Tier 1 even when
they touch the solver or a public API, because they keep those contracts intact.

The feature owner proposes the decision, or the PR author does when the change
is not part of an Epic. Affected community tool authors and maintainers give
input. The proposal stands after 7 days with no unaddressed technical blocker
from a participating maintainer, and the assigned reviewer merges the PR.

## Input and blockers

In shared-ownership projects, it is easy to treat every reviewer comment as a
potential veto. Any participating maintainer may raise a technical blocker.
Community members and other commenters provide feedback, which should be
considered but does not block the decision.

The feature owner weighs the input and decides what to fold into the proposal
for Epic work. In Tier 1, the reviewer decides whether the PR merges. If the PR
author and reviewer cannot resolve a disagreement between themselves, escalate
it using the process below rather than leaving it open indefinitely.

Review mechanics (when to use Request Changes instead of Comment) are covered in
[Development Process][development-process].

## Escalation process

Conda-maintainers follow the IETF's principle of rough consensus ([RFC
7282][rfc7282]). Rough consensus does not mean everyone is happy, and it is not
a majority vote. It means every technical objection has been heard and either
addressed or found not to be a blocker.

> "Consensus is when everyone is sufficiently satisfied with the chosen
> solution, such that they no longer have specific objections to it." (RFC 7282)

Two things that are not rough consensus:

- A minority objector giving up and saying "do what you want." That is
  capitulation, and an unaddressed technical objection is still an open issue.
- Horse-trading: "I'll drop my objection if you drop yours." This leaves both
  issues unresolved.

If a PR author and reviewer cannot reach agreement after good-faith discussion,
either party may call an escalation meeting with the conda-maintainers team.

> [!IMPORTANT]
> Nothing in this process takes priority over the
> [Conda Code of Conduct](https://github.com/conda/governance/blob/main/CODE_OF_CONDUCT.md).
> Where the two conflict, the Code of Conduct wins. Any code of conduct concern
> must be resolved before the technical decision proceeds.

### Step 1: Reframe objections on the PR

Before calling a meeting, the party with the objection should post a comment
stating:

- The specific technical concern (not a preference or style opinion)
- What outcome would address it

If the solution is not ideal but workable, that is not a blocker and rough
consensus has been reached.

### Step 2: Signal the impasse and start a session

If the objection remains unresolved after Step 1, either party comments on the
PR that the review is at an impasse. The person calling the session opens a
thread in `#conda-maintainers` on Zulip with:

- A link to the PR
- A one-sentence neutral summary of the unresolved technical question

A session can be any of the following:

1. A synchronous meeting via video call or chat
2. An extended asynchronous thread in Zulip

Tag `@conda-maintainers`. For a synchronous discussion, coordinate a session
time that works for the team and takes global time zones into account.

### Step 3: Hold the session

The feature owner presents the proposal if the PR is part of an active feature,
and does not call or facilitate the session. If the feature owner is the PR
author or the reviewer, another conda-maintainer calls and facilitates the
session instead. The session caller should:

- Ask each party to state their technical objection specifically, without
  re-arguing the full history
- For each objection, ask: "Has this concern been addressed, or is it a genuine
  technical blocker?"
- Separate objections that need to be resolved from preferences that can be set
  aside
- Declare rough consensus when all technical blockers have been addressed and
  at least three conda-maintainers, including the session caller, have
  participated in the session or the async thread, even if not everyone prefers
  the chosen solution
- If fewer than three have participated, keep the question on the async
  `#conda-maintainers` thread until a third maintainer joins

If a technical blocker is still open 14 days after the escalation thread's first
post, the contested change pauses and is not merged. The feature owner may split
off uncontested parts or run a spike to answer the open question. Step 4 records
the open objection.

### Step 4: Record the outcome on the PR

Whoever called the session posts a comment on the PR summarizing the decision
and the reasoning, specifically noting how any technical objections were
addressed or why they were judged not to be blockers. If a technical blocker is
still open, that is recorded as well. Otherwise the PR proceeds.

## Further reading

- [conda governance][governance]: project team membership and voting procedures
- [Contributing][contributing]: PR and code review process
- [Development Process][development-process]: issue sorting, labeling, and code
  review and merging
