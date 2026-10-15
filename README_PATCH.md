# MTA GitHub Pages deployment correction

Apply these two files to the **desalvo/mta-audio-editor-packages** repository (NOT to the main source repository).

- `scripts/assemble_pages.py`: validate the complete signed tarball but exclude RPM binaries from the deployed site; retain signed DNF indexes and APT data.
- `.github/workflows/pages.yml`: reject leaked RPMs, print APT/RPM sizes, and replace the obsolete R2 diagnostic.

Important: the signed Actions artifact is intentionally left intact so that the existing source-repository RPM retention workflow can recover older releases. The RPMs themselves remain published as GitHub Release assets.

Commit these changes in `mta-audio-editor-packages`, then rerun Deploy MTA package repositories to GitHub Pages. If the assembled site still exceeds the limit, the new logs will show the size of the APT subtree, which requires a separate migration decision.
