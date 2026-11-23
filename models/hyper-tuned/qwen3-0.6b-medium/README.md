# qwen3-0.6b-medium

A LoRA adapter for the Zerds meeting app: task **medium**, on the base model **Qwen/Qwen3-0.6B** (`Qwen3-0.6B-Q4_K_M.gguf`).

## What it does

Cleans up a meeting transcript turn by turn and shortens it, keeping every name, number and decision.

## Files

| Version | Status | Release | File | SHA-256 | Bytes |
|---|---|---|---|---|---|
| 1.0.0 | stable | hyper-tuned-v1.0.0 | [qwen3-0.6b-medium-1.0.0.gguf](https://github.com/uhstray-io/zerds-public/releases/download/hyper-tuned-v1.0.0/qwen3-0.6b-medium-1.0.0.gguf) | `487366add0ed805293d8fe811ff2981455c0368932e069f432842950c05f8b34` | 10119936 |

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

## Measured quality (version 1.0.0)

Gate: keyword gate, 1,479 examples, bar 98% (finetune/keygate.py), and the 8 bench meetings, run 73. Passes its bar. Measured 2026-11-23.

| Measure | Value |
|---|---|
| keygate_examples_all_keywords | 0.993 |
| keywords_kept | 0.9978 |
| keygate_length_ratio | 0.816 |
| meetings_key_moments | 0.97-0.99 |
| meetings_facts | 0.97-1.00 |
| meetings_length_ratio | 0.78-0.83 |

## Limits

- Trained and measured on English meetings of the AMI and ICSI corpora only.
- A small model: check its output before relying on it for names and numbers.
- Measured with the base and prompt above; other pairings are not measured.

## Training

Set `m5-edits` (SHA-256 `a0de0029923ae6c88625ca0dc3c1860051e659f0519d23831644fa510e548c70`), trainer train_torch.py (torch 2.11.0+cu128, cuda), LoRA rank 8, alpha 16.

## Licence and attribution

Adapter licence: LicenseRef-Uhstray-Hyper-Tuned-Adapter-1.0. Base model licence: Apache-2.0.

The licence text is `LICENSE` and the full notice is `NOTICE`, in `models/hyper-tuned/` of the
`uhstray-io/zerds-public` repository.

> Attribution: Trained in part on text derived from the AMI Meeting Corpus and the ICSI Meeting Corpus, both CC BY 4.0; changes were made. Full notice: models/hyper-tuned/NOTICE.
