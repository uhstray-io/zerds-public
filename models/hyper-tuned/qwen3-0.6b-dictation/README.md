# qwen3-0.6b-dictation

A LoRA adapter for the Zerds meeting app: task **dictation**, on the base model **Qwen/Qwen3-0.6B** (`Qwen3-0.6B-Q4_K_M.gguf`).

## What it does

Tidies dictated text, and rewrites it on a spoken command.

## Files

| Version | Status | Release | File | SHA-256 | Bytes |
|---|---|---|---|---|---|
| 1.0.0 | stable | hyper-tuned-v1.0.0 | [qwen3-0.6b-dictation-1.0.0.gguf](https://github.com/uhstray-io/zerds-public/releases/download/hyper-tuned-v1.0.0/qwen3-0.6b-dictation-1.0.0.gguf) | `0227045912aff399888a8970cc9308373ad307bc3bd5afa0d7da85e8195ff1f2` | 20212480 |

## Use

Load it with llama.cpp (converted with `b10200`) on the base file `Qwen3-0.6B-Q4_K_M.gguf`, SHA-256 `ac2d97712095a558e31573f62f466a3f9d93990898b0ec79d7c974c1780d524a`. Another quantisation of the base is not the pairing that was measured.

The adapter expects this prompt template (system prompt SHA-256 `b611dc39e6eddf33f3eddeda20767bf95b9e898fce274e18ee5888c111e53260,be92ceeb6f7144599cc5f7920a105133443a028fb1bccc6629bcb97a77c5faa3`):

```
<|im_start|>system
{{SYSTEM}}<|im_end|>
<|im_start|>user
{{USER}}<|im_end|>
<|im_start|>assistant
<think>

</think>


```

## Measured quality (version 1.0.0)

Gate: tidy gate, 32 phrases (zerds-bench tidy --rules --phrases bench/tidy_phrases.json), run 5. Passes its bar. Measured 2026-11-16.

| Measure | Value |
|---|---|
| phrases_exact | 26 of 32 |

## Limits

- Trained and measured on English meetings of the AMI and ICSI corpora only.
- A small model: check its output before relying on it for names and numbers.
- Measured with the base and prompt above; other pairings are not measured.

## Training

Set `d1` (SHA-256 `48586609b2a441736d8c2df51407dc81adf379d13298f4581951cac3d5b0d703`), trainer train_torch.py (torch 2.11.0+cu128, cuda), LoRA rank 16, alpha 32.

## Licence and attribution

Adapter licence: LicenseRef-Uhstray-Hyper-Tuned-Adapter-1.0. Base model licence: Apache-2.0.

The licence text is `LICENSE` and the full notice is `NOTICE`, in `models/hyper-tuned/` of the
`uhstray-io/zerds-public` repository.

> Attribution: Trained in part on text derived from the AMI Meeting Corpus and the ICSI Meeting Corpus, both CC BY 4.0; changes were made. Full notice: models/hyper-tuned/NOTICE.
