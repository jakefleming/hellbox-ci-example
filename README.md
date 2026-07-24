# Hellbox CI example

Proof your fonts on every commit. This repo renders a font proof PDF with
[Hellbox](https://hellbox.com) on a GitHub Actions runner, fails the build if
character coverage or layout regresses, and attaches the proof as a build
artifact.

## How it works

- `proofs/family.fontproof` is a proof document authored in Hellbox (here via
  the CLI: `hellbox --proof fonts/... --save-doc`). It proofs
  [Space Grotesk](https://github.com/floriankarsten/space-grotesk) (SIL OFL),
  all four named instances, using the comprehensive "Idiot Proof" template: character sets, spacing and kerning tests, diacritics, waterfalls, and more, across every section type Hellbox ships (~200 pages).
- `proofs/fonts/` holds the font binaries. Hellbox resolves fonts relative to
  the document, so the committed proof renders on any machine (Hellbox 1.20.2+).
- `.github/workflows/proof.yml` installs Hellbox, runs `--render-check`
  (machine-readable coverage + overflow audit), gates the build on it, then
  exports the PDF artifact.

Grab the rendered proof from any run's artifacts, or just open [proofs/family.pdf](proofs/family.pdf): the workflow commits the freshly rendered PDF back to the repo on every main push, so the proof you see is always current.

## Use it for your fonts

1. Fork this repo (or copy the workflow).
2. Author a `.fontproof` in Hellbox for your typeface and commit it with your
   font binaries beside it (or have your CI font build place them there).
3. Push. Coverage regressions and layout overflows now fail the build.

Full guide: [hellbox.com/docs/ci](https://hellbox.com/docs/ci)

## License

Space Grotesk is included under the SIL Open Font License (see `OFL.txt`).
The workflow and configuration are MIT.
