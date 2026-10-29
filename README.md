# Action Stations pack files

Download host for the [Action Stations](https://github.com/actionstations-ai/actionstations) pack
catalog. Every `.aspack` file listed at [actionstations.ai/packs](https://actionstations.ai/packs/)
is an asset of the [`packs` release](https://github.com/actionstations-ai/packs/releases/tag/packs).
The catalog (`https://actionstations.ai/packs/index.json`) gives each file's size and SHA-256, and
the app checks both before installing.

Browse, read about and download packs on the website, or install them from the app's **Packs**
screen. Files here are never replaced: a changed pack is a new version with a new file name.

This repository holds no source. The packs are built and published from the website repository.

## Share a pack

Anyone can propose a community pack. It costs nothing and needs no Action Stations account.

1. Make the pack with the app's **Export as pack**, or by hand (see
   [Share a pack](https://actionstations.ai/packs/share/)), and run the validator until it passes.
2. Host the `.aspack` at a public https address, such as a release asset in your own public
   repository. Do not attach it to an issue or commit it here.
3. Open the [Submit a pack](https://github.com/actionstations-ai/packs/issues/new?template=pack-submission.yml) issue form. It asks for
   the pack id, version, file address, SHA-256, purpose, domains and license, and four
   confirmations. A free GitHub account is needed.
4. A maintainer downloads the file, checks the hash, runs the validators, renders every template
   and checks the prompts, document licenses and fictional names. They may ask for changes in the
   issue. Accepted packs are added to the catalog as **Community** packs, credited to everyone in
   `contributors`.

Only licenses that let the catalog redistribute a pack are accepted: CC0-1.0, CC-BY-4.0,
CC-BY-SA-4.0, MIT, Apache-2.0, or a `LicenseRef-` license whose text a reviewer approves. Ids that
start with `ai.actionstations.` are reserved for the project.

## Endorsements

Each community pack gets an issue here. A thumbs-up reaction on it counts as an endorsement and
comments are public feedback. Counts are read when the catalog is built and shown with their date;
packs are never ranked by them, and the site and app do not track anyone.
