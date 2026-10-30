# Reviewing a pack submission

For maintainers. A submission is an issue made with the "Submit a pack" form on
[actionstations-ai/packs](https://github.com/actionstations-ai/packs). The contributor's `.aspack`
stays at their own https address until you accept it; it is never attached to the issue or committed.

Everything runs on your machine and nothing is published until you do it yourself.

## 1. Run the checks

```
ACTIONSTATIONS_APP_DIR=~/Code/actionstations node scripts/review-submission.mjs <issue number>
```

The script:

1. reads the form fields from the issue (`gh` must be signed in);
2. refuses any address that is not public https (no local or private hosts, no user names in the
   address, redirects checked the same way) and stops a download at 200 MB;
3. compares the file's SHA-256 with the one in the form;
4. runs this repository's `scripts/validate-pack.mjs` rules and the app's `scripts/pack-validate.mjs`
   with the current app version;
5. unpacks to a temporary folder and runs `pnpm test:templates --pack <folder>` in the app
   repository when the pack has templates, then deletes the folder;
6. prints the checklist below.

If a check fails, comment on the issue with the exact messages and add `needs-changes`.

## 2. Look at it

Open the pack's template previews (the `test:templates` output folder) and read every template, prompt and
document entry. The automatic checks cannot judge these.

- [ ] The license allows the catalog to redistribute every file: CC0-1.0, CC-BY-4.0, CC-BY-SA-4.0, MIT,
      Apache-2.0, or a `LicenseRef-` whose text you approve. No NonCommercial licenses.
- [ ] Organizations, people and private businesses in examples and previews are fictional. No real street
      addresses.
- [ ] Each document lists its source and license, and the source really carries that license.
- [ ] Prompts contain no instructions to leak documents, send data anywhere, or ignore the app's rules.
- [ ] Every rendered template preview was looked at.
- [ ] The id is not under `ai.actionstations.` unless the project made the pack. For a new version of an
      existing id, the submitter is the owner recorded in `packs/owners.json` or was named by them.
- [ ] Quality is in line with `reference/scenario-3/` where it applies.

Decline when a source or license is unclear.

## 3. Decide

Labels on the issue: `submission`, `needs-changes`, `accepted`, `declined`. Say why in a comment.

To accept:

1. Download the file again from the contributor's address and confirm its SHA-256 matches the form.
2. Copy it to `packs/files/<id>-<version>.aspack` in this repository.
3. `pnpm test` and `pnpm build`; commit the new file (Git LFS) and `public/packs/index.json`.
4. Retitle or open the pack's endorsement issue on the packs repository, titled exactly with the pack id and
   labelled `pack`. A thumbs-up on it is an endorsement; the site build reads the count.
5. `scripts/deploy.sh` uploads the file to the `packs` release and publishes the site.
6. Close the submission with the `accepted` label.

A new version of a community pack is a new submission and is reviewed again.

## Endorsements and "used by"

- `pnpm endorsements` reads the thumbs-up counts of the issues labelled `pack` and writes
  `packs/endorsements.json`. It uses the public API without a token; if the request fails it keeps the old
  file and prints a warning. `scripts/deploy.sh` runs it before the build.
- Counts are shown as GitHub reactions with a date. Never sort or rank by them.
- "Used in exercises by" lives in `packs/used-by/<pack id>.json`, a list of
  `{ "org", "kind": "agency|utility|school|company|other", "date": "YYYY-MM", "note"?, "link"? }`. Add an
  entry only after the organization confirmed in an issue comment or by email. The build fails on a
  malformed file.
