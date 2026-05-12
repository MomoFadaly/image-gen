# Image Generation — 10 AI Models via Smart Router

## What It Does
Generates images using 10 AI models with automatic model selection based on use case. Supports text-in-image, photorealism, design assets, background removal, reference-guided generation, batch editing, and prompt validation.

## Engine API (programmatic)
```javascript
const imageGen = require('./engine');

// Smart router — tries models in priority order
const res = await imageGen.generateBest({ prompt, imageType: 'hero', outputDir: './out', namePrefix: 'hero' });
// Returns: { ok: true, data: { images: [...], model_used, cost_usd }, meta: { skill, command, duration_ms } }

// Direct provider calls
await imageGen.generateImagen({ prompt, outputDir, namePrefix });
await imageGen.generateOpenAI({ prompt, outputDir, namePrefix, quality: 'high' });
await imageGen.generateFal({ prompt, outputDir, namePrefix, model: 'fal-ai/flux-2-pro' });

// Reference-guided
await imageGen.generateWithRef({ prompt, referenceImages: ['./ref.png'], outputDir });

// Editing
await imageGen.editImage({ imagePath: './in.png', instruction: 'Make it watercolor' });
await imageGen.removeBackground({ imagePath: './in.png' });

// Validation
imageGen.validatePrompt({ prompt, imageType: 'hero' }); // score 0-10
```

## CLI (backward compatible)
```bash
node <home>/projects/tools/pantheon/cli/provision.js imagen-best --prompt "<p>" --type hero --output <dir> --name <prefix>
node provision.js imagen-openai --prompt "<p>" --output <dir>
node provision.js imagen-fal --prompt "<p>" --model <fal-model-id> --output <dir>
node provision.js imagen-ref --prompt "<p>" --ref <image> [--strength 0.7] --output <dir>
node provision.js imagen-edit --image <path> --instruction "<edit>"
node provision.js remove-bg --image <path> [--output <path>]
node provision.js validate-prompt --prompt "<p>" [--type hero]
```

## Smart Router — Image Types
| Type | Priority Models |
|------|----------------|
| `hero` | GPT Image 1 → Flux 2 Pro → Seedream 4.5 → Flux Ultra → Imagen 4 |
| `card` | Seedream 4.5 → Flux Ultra → Flux 2 Pro → GPT Image 1 → Imagen 4 |
| `product` | GPT Image 1 → Seedream 4.5 → Flux Ultra → Imagen 4 |
| `asset` | Recraft V3 → Recraft V4 → Ideogram 3.0 → GPT Image 1 |
| `text` | Ideogram 3.0 → Recraft V3 → GPT Image 1 |
| `draft` | Flux 2 Turbo → Imagen 4 |
| `texture` | Imagen 4 → Flux 2 Turbo |

## Models & Costs
| Model | Cost | Best For |
|-------|------|----------|
| GPT Image 1 | $0.08 | Text overlay, photorealism |
| Flux 2 Pro | $0.03 | General high-quality |
| Flux 2 Turbo | $0.008 | Fast drafts |
| Flux Pro Ultra | $0.05 | Maximum quality |
| Ideogram 3 | $0.06 | Text in images |
| Recraft V3/V4 | $0.06 | Design assets |
| Imagen 4 | $0.04 | Google's latest |
| Seedream 4.5 | $0.04 | Artistic styles |
| Flux 2 Flex | $0.03 | Reference-guided |
| BiRefNet v2 | $0.005 | Background removal |

## Critical Rules
1. **NEVER use `editImage` for background removal** — Gemini renders checkerboard, not alpha. ALWAYS use `removeBackground`.
2. Every function returns `{ ok, data, error, meta }` — the universal result contract.
3. At least ONE API key (GEMINI, OPENAI, or FAL) must be set for healthCheck to pass.

## Env Vars
- `GEMINI_API_KEY` — Google Gemini/Imagen (optional)
- `OPENAI_API_KEY` — OpenAI GPT Image (optional)
- `FAL_KEY` — fal.ai Flux/Recraft/Ideogram/BiRefNet (optional)
