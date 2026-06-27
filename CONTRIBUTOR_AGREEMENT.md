# Contributor License Agreement

VegStyle™ is adopting the **FSFE Fiduciary License Agreement 2.1 (FLA-2.1)** for every contribution to any repository in the `vegstylecio` organization. This page is the practical reference for contributors. The signature flow described below applies to every new Pull Request opened in any repository in the organization.

---

## What you sign

The FLA-2.1 assigns the copyright of your contribution to the VegStyle™ fiduciary. The fiduciary grants you back a perpetual, irrevocable, non-exclusive license to your own contribution. Your moral rights as author are inalienable and remain with you under the law.

The outbound license selected for the FLA is **AGPL-3.0-only**, as defined in our [LICENSING_POLICY](LICENSING_POLICY.md). The fiduciary retains the right to evolve the outbound license in the future, within the set of licenses approved jointly by the FSF and the OSI per the FLA-2.1 mechanism. Signing the FLA does not strip you of the right to use, fork, or relicense your own contribution outside the project.

The fiduciary role rests with the project maintainer.

### Stated transition intent

The project's stated intent is to transfer the fiduciary role to a nonprofit entity (the VegStyle™ CIO) once that entity is formally constituted. Until that constitution actually happens, no claim is made that the CIO exists or that any registration procedure is in progress; the only fiduciary that exists is the project maintainer as a natural person.

When the CIO is constituted and accepts the role, the transfer is executed under the FLA-2.1 mechanism, which allows the fiduciary role and the copyright accumulated under it to pass to a successor fiduciary without requiring contributors to re-sign. Contributors signing the FLA today are therefore signing into a model whose long-term destination is institutional stewardship, even though the present-day fiduciary is a single individual.

## Why an FLA

A fiduciary model concentrates copyright stewardship in a single fiduciary so that future re-licensing decisions can be made on behalf of the entire codebase. Without it, any future relicensing requires contacting every past contributor individually. Most long-running open-source projects discover years later that some early contributors are unreachable, at which point the codebase is permanently locked into its original license.

This is the same model used by KDE e.V. and by other FSFE-fiduciaried projects.

## How the signature flow works

1. You open your first Pull Request on any `vegstylecio` repository.
2. The CLA-assistant bot scans the commit authors on your PR. If any author has not yet signed the FLA, the bot posts a comment with a signature link and sets the `license/cla` status check to `failure`.
3. You follow the link to https://cla-assistant.io, read the FLA-2.1 text, and sign with your GitHub account.
4. Your signature is recorded once (GitHub username, name, email, timestamp, PR id, commit SHA) and remains valid for all subsequent contributions across the entire `vegstylecio` organization.
5. The bot re-scans the PR and the status check turns green.

## What happens if you do not sign

A Pull Request with one or more unsigned commit authors stays **unmergeable** by branch protection. The `license/cla` status check stays red and the merge button is disabled for everyone, including maintainers. The PR remains open until every author signs or until a maintainer closes it.

Co-authored commits require signature from every co-author individually. The bot enforces this per-author, not per-PR.

## Versioning of the FLA

If the FLA itself is updated in the future (for example, from FLA-2.1 to a hypothetical FLA-2.2), prior signatures do not automatically carry over to the new version and the bot will prompt you to re-sign on your next contribution. Outbound license changes within the FLA-2.1 mechanism do not require re-signature, since re-licensing power is part of what you already granted.

## The FLA-2.1 full text

The authoritative FLA-2.1 text is presented by the CLA-assistant bot when you open your first Pull Request. There is no separately published copy of the text outside the signing flow: the bot displays it on the signing page that the comment on your PR will link to, and that page is where you accept the terms by clicking "Sign in with GitHub".

## Questions

If something on this page is unclear, open a Discussion in the org Discussions before opening your PR.
