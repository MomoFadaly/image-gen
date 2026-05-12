# image-gen

> Image generation across 10 AI models via a smart router — text overlay, photorealism, design assets, reference-guided generation, batch editing.

**Free. Apache 2.0. Bring-your-own-Claude.**

## What this is

A Claude skill bundle — a sanitized, attributed, downloadable subject-matter expert that runs inside Claude Code, Claude Desktop, or any Claude-API workflow. Drop it in, invoke it, get answers grounded in real practitioner content rather than generic LLM consensus.

Use to generate an image from a prompt, route to the right model by image type (hero, card, product, asset, text), edit images, or remove backgrounds.

## Install

```bash
# Claude Code plugin install (one-line)
claude plugin install image-gen --from https://fadaly.net/downloads/skills/image-gen.zip
```

Or clone this repo into your local Claude skills directory (typically `~/.claude/skills/` on macOS / Linux):

```bash
git clone https://github.com/MomoFadaly/image-gen.git
```

Or download the zip from [fadaly.net/skills/image-gen](https://fadaly.net/skills/image-gen) (the per-skill landing page on fadaly.net) and extract into `~/.claude/skills/`.

## What's in the bundle

| File | Size |
|---|---|
| `SKILL.md` | 3KB |
| `thumb.png` | 1.12MB |

Total: 1.12MB

## Sources

This SME's canon was built from these practitioners. Every claim in the canon is attributed.

- Google Gemini / Imagen · OpenAI GPT Image · fal.ai (Flux · Recraft · Ideogram · BiRefNet)

Primary sources (official documentation, peer-reviewed research) take priority over practitioner consensus, which takes priority over single-source claims. Confidence tiers are tagged inline.

## How it works

Claude reads `SKILL.md` as the system instructions for the skill. Supporting files (`canon.md`, `mental-models.md`, etc.) are loaded as reference material when the skill needs to answer off the cuff or cite a specific source.

When you ask a question this SME covers, Claude pulls the relevant canon entry, names its source, tags its confidence level, and pushes back if your question contradicts canon.

## Confidence levels

- **Verified** — primary source + practitioner corroboration. Treat as fact.
- **Confirmed** — practitioner consensus across credible voices, no primary contradiction. Defended best-practice.
- **Plausible** — single-source or thin evidence. Working hypothesis until validated.
- **Disputed** — credible voices disagree. The SME names the camps and gives you the lens to decide.
- **Stale** — once true, contradicted by current docs/data. Flagged for refresh.

## License

Apache License 2.0. See [LICENSE](LICENSE).

You are free to use, modify, redistribute, and build on this skill. Attribution to the original practitioners (named in `sources.md` or `SKILL.md`) is morally required even if not legally; their work made the canon possible.

## More like this

This is one of a series of Claude skills published openly. See the [full catalog at fadaly.net/work](https://fadaly.net/work).
