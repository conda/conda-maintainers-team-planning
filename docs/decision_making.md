[governance]: https://github.com/conda/governance
[how-we-use-github]: https://github.com/conda/conda/blob/main/HOW_WE_USE_GITHUB.md#code-review-and-merging
[rapid]: https://cio-wiki.org/wiki/RAPID_Approach
[rfc7282]: https://www.rfc-editor.org/rfc/rfc7282
[project-roadmap]: https://github.com/orgs/conda/projects/22/views/15
[cep-9]: https://github.com/conda/ceps/blob/main/cep-0009.md
[contributing]: https://github.com/conda/conda/blob/main/CONTRIBUTING.md

# Decision Making for conda Maintainers

> [!NOTE]
> This page is for current and prospective members of the
> **conda-maintainers** team, not for all contributors.

This page describes how the conda-maintainers team makes decisions on the
repositories they maintain, including conda. Conda Organization governance
(Steering Council, project team membership, voting) is covered in the
[conda governance repository][governance].

## Principles

The conda-maintainers use a lightweight version of the [RAPID framework][rapid].
Every significant decision gets a named owner, a small set of people who must
agree before it proceeds, and a set of people whose input is sought but who
cannot block it.

Everyone can contribute anywhere in a shared codebase. That does not mean every
decision needs consensus from everyone.

## Roles

- **Recommend (R):** Investigates the problem, proposes the solution, and
  drives the plan. For features, this is the feature owner. For smaller changes,
  this is the PR author.
- **Agree (A):** Must approve before the decision is final. For PRs, this is
  the reviewer the PR author identified ahead of time, ideally someone they
  worked with during development. Keep this group small. Other commenters on a
  PR are giving Input, not Agree.
- **Perform (P):** Executes the decision. Often the whole team or a subset of
  contributors. Because ownership is shared, most engineers are in this role on
  most features.
- **Input (I):** Consulted but not a blocker. Community contributors, users,
  and other maintainers provide Input through GitHub issues and PR threads.
- **Decide (D):** Single accountable decision-maker for this decision type. For
  in-scope technical decisions on a feature, this is the feature owner. For
  major architectural decisions with ecosystem impact, this is the Technical
  Lead.

## The Technical Lead role

The Technical Lead is a named role held by one conda-maintainer. The
team README lists who currently holds it. The Technical Lead holds Agree for
Tier 2 feature-level architectural decisions, chairs escalation sessions, and
decides blockers that stay open past the Step 3 time box.
When the Technical Lead is unavailable, they designate an acting Technical Lead
in the PR or the Zulip thread before the session starts.

## The feature owner role

Each Epic that reaches Near on the Roadmap board is assigned a feature owner: a
rotating conda-maintainer who is accountable for that Epic's requirements, plan,
and execution. The feature owner does not do all the work themselves.

The feature owner:

- Holds R and D for the duration of the Epic
- Opens and drives the GitHub issue discussion to gather community Input before
  work begins
- Makes in-scope technical decisions during execution without requiring
  consensus on every choice

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
   fewest Epics recently. If nobody volunteers, the Planning Lead assigns a
   conda-maintainer directly, using the same rule.
4. The Planning Lead sets the feature owner as the Epic's assignee. The feature
   owner confirms by commenting on the Epic.

## Decision tiers

### Tier 1: PR and story-level decisions

Most changes fall here. The PR author is R, the reviewer they identified ahead
of time is A, and the approving reviewer merges. Community members commenting on
the PR are providing Input.

Request a review from the person you identified ahead of time to work with. If
you paired with them during development, continuous review counts as this
requirement. See [How We Use GitHub: Code Review and Merging][how-we-use-github].

### Tier 2: Feature-level architectural decisions

Changes that affect solver behavior, plugin APIs, [deprecation schedules][cep-9],
cross-platform behavior, or other areas with ecosystem-wide impact. The feature
owner is R, affected community tool authors and maintainers are I, the
Technical Lead is A on PRs, and the feature owner is D for implementation
decisions.

## Input vs. agree

In shared-ownership projects, it is easy to treat every reviewer comment as a
potential veto. Only the assigned reviewer holds Agree and can block a merge.
Other commenters are providing Input. Their feedback should be considered, but
it does not block the decision.

The feature owner synthesizes Input and decides what to act on. If the PR author
and reviewer cannot resolve a disagreement between themselves, escalate it
using the process below rather than leaving it open indefinitely.

Review mechanics (when to use Request Changes instead of Comment) are covered in
[How We Use GitHub: Code Review and Merging][how-we-use-github].

## Escalation process

Conda-maintainers follow the IETF's principle of rough consensus ([RFC
7282][rfc7282]). Rough consensus does not mean everyone is happy, and it is not
a majority vote. It means every technical objection has been heard and either
addressed or found not to be a blocker.

> "Consensus is when everyone is sufficiently satisfied with the chosen
> solution, such that they no longer have specific objections to it." (RFC 7282)

Two things that are **not** rough consensus:

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

This separates genuine blockers from unappealing but acceptable tradeoffs. If
the objection is that the solution is not ideal but workable, that is not a
blocker and rough consensus has been reached.

### Step 2: Signal the impasse and start a session

If the objection remains unresolved after Step 1, either party comments on the
PR that the review is at an impasse. The person calling the session opens a
thread in `#conda-maintainers` on Zulip with:

- A link to the PR
- A one-sentence neutral summary of the unresolved technical question

A session can be any of the following:

1. A synchronous meeting via video call or chat
2. An extended asynchronous thread in Zulip
3. 1:1 discussions with the session chair, which gather input and count toward
   participation, though consensus is still declared per Step 3

Tag `@conda-maintainers`. For a synchronous discussion, coordinate a session
time that works for the team and takes global time zones into account.

### Step 3: Hold the session

The session chair is the Technical Lead, or the acting Technical Lead they
designated. The feature owner attends if the PR is part of an active feature.
The chair should:

- Ask each party to state their technical objection specifically, without
  re-arguing the full history
- For each objection, ask: "Has this concern been addressed, or is it a genuine
  technical blocker?"
- Separate objections that need to be resolved from preferences that can be set
  aside
- Declare rough consensus when all technical blockers have been addressed, even
  if not everyone prefers the chosen solution
- Declare rough consensus only when at least three conda-maintainers, including
  the chair, have participated, whether in the session, the async thread, or a
  1:1 with the chair
- If fewer than three have participated, keep the question on the async
  `#conda-maintainers` thread. The chair may declare consensus no earlier than
  7 days after the thread's first post

Once that participation floor is met, the chair does not need unanimity. A
strong majority with no unaddressed technical blockers is enough.

If a technical blocker is still open 14 days after the escalation thread's first
post, the Technical Lead decides the question and overrides the open objection.
Step 4 records the decision and the objection.

### Step 4: Record the outcome on the PR

Whoever called the session posts a comment on the PR summarizing the decision
and the reasoning, specifically noting how any technical objections were
addressed or why they were judged not to be blockers. If the Technical Lead
overrode an open objection, then that is included as well. The PR then proceeds
accordingly.

## Further reading

- [conda governance][governance]: project team membership and voting procedures
- [RAPID Approach][rapid]: background on the Recommend, Agree, Perform, Input,
  and Decide roles
- [Contributing][contributing]: PR and code review process
- [How We Use GitHub: Code Review and Merging][how-we-use-github]: GitHub
  workflow and review requirements
