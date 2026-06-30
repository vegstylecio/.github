# VegStyle Licensing Policy
Version 1.0 (effective 2026-06-23)  

This document defines the outbound license under which software contributions to VegStyle repositories may be released by the fiduciary. It is referenced by the FSFE Fiduciary License Agreement 2.1 (FLA-2.1) adopted by the project.

## Current outbound license
For software (source code, build configuration, executable binaries):  
- **AGPL-3.0-only** (GNU Affero General Public License version 3.0, without the "or later" clause)  
The applicable license for each file is indicated by the file's copyright header or by a top-level `LICENSE` / `NOTICE` file.

## Constraints on policy evolution
This policy may evolve over time, but only within the following constraints:
1. Any added or substituted outbound license must be classified as both Free Software by the Free Software Foundation AND approved as Open Source by the Open Source Initiative.
2. Any added or substituted outbound license must be copyleft. Strong copyleft is preferred; weak copyleft is acceptable only on a case-by-case basis for specific components where strong copyleft is technically incompatible. Permissive licenses (MIT, BSD, Apache, ISC, and equivalent) are excluded by this policy.
3. The fiduciary (the project maintainer as a natural person at the time of writing, with stated intent to transition to a successor fiduciary as defined by the FLA-2.1 transfer mechanism) is responsible for keeping this policy aligned with the FLA-2.1 framework.

## Why permissive licenses are excluded
Permissive licenses qualify under the FLA-2.1 "FSF approved + OSI approved" constraint and would therefore be technically eligible. They are nonetheless excluded by this policy because derivative works under permissive licenses can be incorporated into proprietary products, which is incompatible with VegStyle's mission to build a commons that cannot be privately enclosed.

## How to change this policy
Updates to this document are made via Pull Request to the `vegstylecio/.github` repository. Material changes (adding or removing licenses from the current outbound list, modifying constraints) are announced via the project's public communication channels and become effective on commit to the main branch.  
Updates to this policy do not require contributors to re-sign the FLA, as long as the change stays within the constraints listed above. This is the explicit purpose of selecting Option 3 (external licensing policy) under FLA-2.1.

---

*Version history:*
- *v1.0 (2026-06-23): initial policy. Outbound: AGPL-3.0-only.*
