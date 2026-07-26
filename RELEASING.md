# Releasing & DOI

This repo is set up to mint a permanent [Zenodo](https://zenodo.org) DOI for every tagged
release, so the model has a stable, dated, citable version-of-record. The metadata Zenodo
uses lives in [`.zenodo.json`](.zenodo.json).

## One-time setup (owner)

1. Go to <https://zenodo.org> and log in with GitHub (top-right → "Log in" → GitHub).
2. Authorise Zenodo, then open <https://zenodo.org/account/settings/github/>.
3. Find **VictorOsondu/ai-adoption-model** in the list and flip the switch **On**.
   - If it isn't listed, click "Sync now" and refresh.
   - This must be done **before** the release below, or that release won't be archived.

## Cut a release (mints the DOI)

Once the switch is on:

```bash
# from the repo root, on main, working tree clean
git tag -a v1.0.0 -m "The Six Stages of AI Adoption v1.0.0"
git push origin v1.0.0
gh release create v1.0.0 --title "v1.0.0" --notes "First archived release of the model."
```

Zenodo picks up the release within a minute or two and mints two DOIs:

- a **concept DOI** — always points to the latest version (use this in the badge and most citations)
- a **version DOI** — pins this exact release

## After the first release

1. Copy the **concept DOI** (e.g. `10.5281/zenodo.1234567`) from the Zenodo record.
2. In [`README.md`](README.md), uncomment the DOI badge line and replace `XXXXXXX`.
3. In [`CITATION.cff`](CITATION.cff), uncomment the `doi:` line and fill it in.
4. Commit: `docs: add minted Zenodo DOI`.

Each later release (v1.1.0, etc.) is archived automatically under the same concept DOI —
no further setup needed.
