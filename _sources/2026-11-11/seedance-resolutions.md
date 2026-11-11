# Seedance — what each model actually outputs, and where 4k lives

Captured 2026-11-11 from BytePlus's own documentation. Every quote below is
verbatim from the page named beside it.

## The short version

| Model ID | 480p | 720p | 1080p | 4k | Source |
|---|---|---|---|---|---|
| `dreamina-seedance-2-5-260628` | yes | yes | yes (10-bit) | **no** | tutorial, create-task reference, pricing |
| `dreamina-seedance-2-0-260128` | yes | yes | yes | **yes** (10-bit) | tutorial, create-task reference |
| `dreamina-seedance-2-0-fast-260128` | yes | yes | no | no | create-task reference |
| `dreamina-seedance-2-0-mini-260615` | yes | yes | no | no | create-task reference |
| `dreamina-seedance-2-5-premium-260915` | — | — | yes | **yes** | BytePlus solutions repo only; see last section |

## 1. Seedance 2.5 tutorial — Resolution

Source: <https://docs.byteplus.com/en/docs/ModelArk/2607688>

> **resolution**: Specifies the resolution of the output video.
>
> - Default value: `720p`
> - Optional values:
>   - `480p` (8-bit color depth)
>   - `720p` (8-bit color depth)
>   - `1080p` (10-bit color depth)

The capability table on the same page lists 4k under **Seedance 2.0**, not 2.5:

> Output resolution — Seedance 2.5: 480p, 720p, 1080p (10-bit) — Seedance 2.0:
> 480p, 720p, 1080p, 4k (10-bit)

## 2. Create video generation task — supported values

Source: <https://docs.byteplus.com/en/docs/ModelArk/1520757>

> - **Dreamina Seedance 2.5:** Default `720p`; supports `480p`, `720p`, and `1080p`.
> - **Dreamina Seedance 2.0:** Default `720p`; supports `480p`, `720p`, `1080p`, and `4k`.

The pixel table in the same reference gives 4k at 16:9 as **3840×2160**, and
marks every other ratio at 4k as a dash for all models except Seedance 2.0.

> 4k — `16:9` — Seedance 2.5: — | Seedance 2.0 series: 3840×2160

## 3. Model list

Source: <https://docs.byteplus.com/en/docs/ModelArk/model-list>

> `dreamina-seedance-2-5-260628` — `.mp4` / `.mov` — 480p (8-bit), 720p (8-bit), 1080p (10-bit)
> `dreamina-seedance-2-0-260128` — `.mp4` — 480p (8-bit), 720p (8-bit), 1080p (8-bit), 4K (10-bit)

## 4. Pricing

Source: <https://docs.byteplus.com/en/docs/ModelArk/1544106>

> `dreamina-seedance-2-5-260628` — 480p and 720p $10.70 — 1080p $11.7 — 4K **Not supported**
> `dreamina-seedance-2-0-260128` — 4K $4.0

## 5. Draft mode ends at 1080p on 2.5

Source: same tutorial, Draft mode section.

> When generating a final video from a Draft video, Dreamina Seedance 2.5
> currently supports only 1080p output. Setting another resolution causes an error.

> `resolution` is required and only supports `1080p`.

## 6. The whitelist-only Premium route

Not on any public BytePlus documentation page. The claim comes from BytePlus's
own solutions-team repository, <https://github.com/byteplus-sa/modelark-mcp>,
`docs/models.md`:

> Seedance 2.5 Premium (`seedance_2_5_premium`) is a separate, whitelist-only
> family with the same 2.5 limits plus `4k`.
>
> `seedance_2_5_premium` — `("480p", "720p", "1080p", "4k")`

Default model ID in that document: `dreamina-seedance-2-5-premium-260915`.
Treat this as an account entitlement, not a public capability: an account
outside the program gets the request rejected by the provider. There is no
published price and no signup path.

## What this means for the catalogue

`engine-bytedance` lists `4k` on both Seedance entries:

- **Seedance 2.0** — documented, works on any activated account.
- **Seedance 2.5** — accepted only by the Premium program. The endpoint file
  says so in the parameter note, so nobody reads the option as a promise.

Draft finishing honours `4k` when the profile asks for it and otherwise sends
`1080p`, which is what BytePlus requires for every non-Premium account.
