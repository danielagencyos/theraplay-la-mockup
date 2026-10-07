# THERA-85: Rasika's review-call changes, where they went and how to get them into GitHub

Written 2026-10-07. Covers the Theraplay LA website feedback batch Rasika delivered on 2026-09-22 under THERA-85.

## Summary

- Rasika applied the client's review-call feedback and deployed it to theraplay-la-new.vercel.app on 2026-09-22.
- She never committed or pushed. The deployment was built from a local copy of the August commit `e63b79b` with uncommitted edits (Vercel recorded `gitDirty: 1`).
- GitHub has no trace of her work. The repo `danielagencyos/theraplay-la-mockup` has four commits, all by Daniel, and no branches or pull requests from her.
- Daniel's commit `a9c4b4b` from 2026-10-07 (services review round 2, Sep 29 call) was made on top of the August code without her edits. The two sets of changes have diverged and touch the same files.
- Her source files were recovered from the Vercel deployment on 2026-10-07. They sit ready to commit on a branch. See "Recovery" below.

## Where each thing lives

| Thing | Location | State |
|---|---|---|
| Plane task | THERA-85, assigned to Rasika, high priority, due 2026-09-22 | Still "To Do". Her change list is the only comment (2026-09-22) |
| Preview she shipped | https://theraplay-la-new.vercel.app | Vercel project `theraplay-la-new`, team `agencyosinternal`, deployed from the CLI as team@tryagencyos.ai, not connected to GitHub |
| Deployment holding her source | `dpl_7u6uHVu5kYYZGjoiFKXJu3cX5fMz` (production, 2026-09-22 15:50 UTC) | 59 source files still downloadable through the Vercel API. This is the only copy |
| GitHub repo | `danielagencyos/theraplay-la-mockup`, public, branch `main` at `a9c4b4b` | Does not contain her changes |
| Other Vercel project | `theraplay-la-mockup` (the August mockup URL) | Separate project, also CLI-deployed, not connected to GitHub |
| Local clone | `Theraplay website/site/` | Tracks `main`, at `a9c4b4b` |

## What she changed

Measured as her recovered files against the August commit `e63b79b`, after normalising line endings. Her editor saved 19 files with Windows line endings (CRLF), which made the raw diff look like a rewrite of every file. With that stripped out the real change is small.

**19 source files, 106 lines in, 104 lines out, plus one new image.** 48 of those line pairs only replace a long dash with a comma, full stop, colon or brackets. The substantive changes are below.

### Site-wide

- Removed every long dash (em and en) across all pages and components. Same intent as Daniel's round-two commit, so expect conflicts on these lines.
- Removed "doctor-led" from the home hero subtitle, the home badges and the About page meta description. The badge now reads "Whole-child care".
- Added `PAMS` to Dr. Marielly's credentials in the footer, home bio, About bio and team card.
- Changed "nearly 13 years" to "15+ years" in the home bio, About bio and team card. The stats bar value went from `13+` to `15+`.
- Base layout default meta description: "TheraPlay LA is a leading pediatric therapy clinic..." instead of a dashed phrase.

### Components

- `Hero.astro`: new optional `imagePosition` prop, applied as an inline `object-position` style on the hero image.
- `StatBar.astro`: Google rating `4.5★` to `4.8★`, years `13+` to `15+`.
- `Footer.astro`: PAMS added to the founder line.
- `Header.astro`: logo alt text no longer has a dash.
- `ContactForm.astro`, `CtaBand.astro`: dash cleanup only.

### Home (`src/pages/index.astro`)

- New hero image `public/images/hero-dr-marielly-gym.jpg` (244 KB, new file) positioned at `64% center`, replacing `clinic-swing-therapy.jpg`.
- OT card: "Regulation, attention, fine and gross motor skills, sensory processing, and primitive reflex integration, built through purposeful play." Note that "sensory processing" is kept, not replaced.
- Speech card: "Speech, language, cognitive-communication, feeding and swallowing support from licensed SLPs." The "parent coaching woven into every session" line is gone.
- Testimonials note: "Inspired by the experiences families describe in public reviews." The words "Illustrative testimonials for mockup purposes" are gone.
- "How we help" section: dash cleanup only. No copy rewrite was made here. Rasika flagged this section as still needing a copy pass.

### About (`src/pages/about.astro`)

- Hero subtitle ends "...families trust across Los Angeles and beyond."
- Three disciplines block reordered and reworded: Occupational Therapy (regulation and attention wording), Speech Therapy (new, "Speech, language, cognitive-communication, feeding and swallowing support from licensed SLPs."), Airway-Focused Care. The Myofunctional Therapy card is removed from this block.
- "Parents are partners" belief: "No black-box therapy." removed.
- Bio: "After 15+ years working hands-on with children..." and PAMS in the credentials line.
- Meta description no longer says "doctor-led".
- The "I graduated from USC, number one OT program" line is **not** in her files. Still to do.

### Contact (`src/pages/contact.astro`)

- Hours: "Monday - Friday: 9am - 6pm" (was 8am). "Weekend intensives by arrangement only" (added "only").
- Hero subtitle: "...we'll tell you what we think and what to do next." The word "honestly" is gone.
- Step 1 copy: "Fill out the form or call us. It takes two minutes."

### Our Space (`src/pages/our-space.astro`)

- Dash cleanup, plus "Tours are part of every first visit, and most kids don't want to leave." (was "every discovery visit").

### Services (`src/pages/services/*.astro`)

- Services index: OT card leads with "regulation, attention"; speech card lists "feeding and swallowing" instead of parent coaching; feeding card uses brackets instead of dashes.
- Feeding, intensives, myofunctional, OT and speech pages: dash cleanup only, no content changes.

### Team (`src/pages/team.astro`)

- Dr. Marielly: PAMS in credentials, "15+ years" in bio.
- Sleep specialist bio: dash cleanup.
- Marnie, Megan and Patricia are not added. Rasika noted this was outside the change request.

### Not changed, and still open from her Plane list

- Specialty services count still reads `8` in the stats bar. Waiting on Lenny to confirm.
- "Sensory processing" was kept alongside "Regulation, attention" rather than replaced. Confirm with the client which they meant.
- "How we help" copy from 2:30 in the Fathom recording, and the USC bio line, were not applied.

## Recovery

Done on 2026-10-07 from this machine:

1. Downloaded all 59 files of deployment `dpl_7u6uHVu5kYYZGjoiFKXJu3cX5fMz` through the Vercel API (`/v6/deployments/{id}/files` and `/v7/deployments/{id}/files/{uid}`, team `agencyosinternal`).
2. Created a git worktree of this repo at `e63b79b` on a new branch `rasika/thera-85-review-call-feedback`.
3. Copied her files over it (skipping `.astro/` and `.claude/`), converted CRLF to LF, and restored four PNGs the line-ending pass had touched.
4. Staged everything. Nothing was committed or pushed: the session's permission layer blocked the commit.

The staged branch is in the worktree at:

```
/tmp/claude-1000/-home-daniel-Downloads-Claude-Code-OD-AgencyOS-plane/b42a56ed-0359-484d-bfe5-ea4b45e1dd0b/scratchpad/wt-rasika
```

That path is a session scratch folder and will not survive a cleanup. The raw downloaded files are beside it in `rasika-src/`. If both are gone, repeat step 1; the deployment stays on Vercel until someone deletes the project.

## How to get everything into GitHub

Run from the worktree above. The commit is authored to Rasika since it is her work.

```bash
cd "/tmp/claude-1000/-home-daniel-Downloads-Claude-Code-OD-AgencyOS-plane/b42a56ed-0359-484d-bfe5-ea4b45e1dd0b/scratchpad/wt-rasika"
git status --short | wc -l        # expect 19 staged paths
git commit --author="Rasika Salinda <rasika@faber.house>" \
  -m "THERA-85: apply Theraplay's review-call feedback (recovered from Vercel)" \
  -m "Recovered from CLI deployment dpl_7u6uHVu5kYYZGjoiFKXJu3cX5fMz on Vercel project theraplay-la-new. Never committed; built from a dirty copy of e63b79b. CRLF normalised to LF."
git push -u origin rasika/thera-85-review-call-feedback
gh pr create --base main --head rasika/thera-85-review-call-feedback \
  --title "THERA-85: Theraplay review-call feedback (Rasika, 2026-09-22)" \
  --body "Recovered from the Vercel deployment. See THERA-85-RASIKA-CHANGES-2026-10-07.md on main."
```

Then commit this file on `main` from the normal clone:

```bash
cd "/home/daniel/Downloads/Claude Code OD/Theraplay website/site"
git add THERA-85-RASIKA-CHANGES-2026-10-07.md
git commit -m "Document THERA-85 recovery and Rasika's change list"
git push
```

## Merging her branch with round two

Do not expect a clean merge. Both her branch and `a9c4b4b` edit the same 19 source files, and both remove the same long dashes, often on the same lines with different replacement punctuation. Resolve file by file, keeping:

- Her content changes listed above (hero image, stats, PAMS, 15+, regulation and attention, feeding and swallowing, About disciplines, Contact hours, "beyond").
- Daniel's round-two changes (Lora headings, intensive length removals, reordered signs lists and FAQs, new OT and speech banners, bigger page titles, teletherapy disclaimer removed).
- Whichever dash replacement reads better where they differ.

After the merge, redeploy `theraplay-la-new` from the merged `main` so the preview and the repo agree, and connect the Vercel project to the GitHub repo so this cannot happen again.

## Why this happened

- The Vercel projects are CLI-deployed under the shared team@tryagencyos.ai login and are not linked to GitHub, so a deploy leaves no commit.
- The repo is public and lives under a personal account (`danielagencyos`), not under the team org.
- THERA-85 asked for the design to be updated and shared, but did not say "open a pull request". The definition of done should name the repo and branch.

## Plane follow-ups

- Move THERA-85 out of "To Do". It has been delivered since 2026-09-22 and is waiting on Daniel's review.
- Add a sub-task for the merge with round two and the redeploy.
- Keep the USC line, the "How we help" copy, the specialty count and the team additions as separate open items.
