# qwen3-0.6b-high

A LoRA adapter for the Zerds meeting app: task **high**, on the base model **Qwen/Qwen3-0.6B** (`Qwen3-0.6B-Q4_K_M.gguf`).

## What it does

Rewrites a meeting transcript turn by turn to about half its length, keeping its meaning.

## Files

| Version | Status | Release | File | SHA-256 | Bytes |
|---|---|---|---|---|---|
| 0.1.0 | experimental | hyper-tuned-v1.0.0 | [qwen3-0.6b-high-0.1.0.gguf](https://github.com/uhstray-io/zerds-public/releases/download/hyper-tuned-v1.0.0/qwen3-0.6b-high-0.1.0.gguf) | `1e9f917f24b65edbb753a70e7455b504698f42f29dd4c4521e06392a6cc2585d` | 20212512 |

## Use

Load it with llama.cpp (converted with `b10200`) on the base file `Qwen3-0.6B-Q4_K_M.gguf`, SHA-256 `ac2d97712095a558e31573f62f466a3f9d93990898b0ec79d7c974c1780d524a`. Another quantisation of the base is not the pairing that was measured.

The adapter expects this prompt template (system prompt SHA-256 `883d2b765860d63b8af296c6183f0b564de8828541ad9529dcf9f7e18d4d9c7e`):

```
<|im_start|>system
{{SYSTEM}}<|im_end|>
<|im_start|>user
{{USER}}<|im_end|>
<|im_start|>assistant
<think>

</think>


```

## Measured quality (version 0.1.0)

Gate: high gate (bench/high_gate.py): cut 35% overall and 40% on long turns, 97% of names and numbers, judged 95% supported and at most 2% invented, runs 46 and 47. Does not yet pass its bar. Measured 2026-11-21.

| Measure | Value |
|---|---|
| cut_all_meetings | 0.407 |
| names_and_numbers | 0.975 |
| meetings_at_size_bar | 6 of 8 |
| meetings_at_facts_bar | 5 of 8 |
| statements_supported_2_meetings | 0.953 |
| invented | 0 |

## Limits

- Trained and measured on English meetings of the AMI and ICSI corpora only.
- A small model: check its output before relying on it for names and numbers.
- Experimental versions have not passed every part of their gate.

## Training

Set `h4-edits` (SHA-256 `d93377bce997a130fa2be521cc8856edc236280461b06b4a8518fb88fff675a9`), trainer train_torch.py (torch 2.11.0+cu128, cuda), LoRA rank 16, alpha 32.

## Licence and attribution

Adapter licence: LicenseRef-Uhstray-Hyper-Tuned-Adapter-1.0. Base model licence: Apache-2.0.

The licence text is `LICENSE` and the full notice is `NOTICE`, in `models/hyper-tuned/` of the
`uhstray-io/zerds-public` repository.

> Attribution: Trained in part on text derived from the AMI Meeting Corpus and the ICSI Meeting Corpus, both CC BY 4.0; changes were made. Full notice: models/hyper-tuned/NOTICE.
