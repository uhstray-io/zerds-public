# qwen3-1.7b-light

A LoRA adapter for the Zerds meeting app: task **light**, on the base model **Qwen/Qwen3-1.7B** (`Qwen3-1.7B-Q4_K_M.gguf`).

## What it does

Cleans up a meeting transcript turn by turn: fillers and false starts out, the speaker's words kept.

## Files

| Version | Status | Release | File | SHA-256 | Bytes |
|---|---|---|---|---|---|
| 1.0.0 | stable | hyper-tuned-v1.0.0 | [qwen3-1.7b-light-1.0.0.gguf](https://github.com/uhstray-io/zerds-public/releases/download/hyper-tuned-v1.0.0/qwen3-1.7b-light-1.0.0.gguf) | `0712cf03f1716af6da8ba977e0f2a80c660836a867406a5d8c2f49fa7e2348a0` | 17459872 |

## Use

Load it with llama.cpp (converted with `b10200`) on the base file `Qwen3-1.7B-Q4_K_M.gguf`, SHA-256 `b139949c5bd74937ad8ed8c8cf3d9ffb1e99c866c823204dc42c0d91fa181897`. Another quantisation of the base is not the pairing that was measured.

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

Gate: keyword gate, 1,479 examples, bar 98% (finetune/keygate.py), and the 8 bench meetings, run 70. Passes its bar. Measured 2026-11-22.

| Measure | Value |
|---|---|
| keygate_examples_all_keywords | 0.999 |
| keywords_kept | 0.9998 |
| keygate_length_ratio | 0.897 |
| meetings_key_moments | 1 |
| meetings_facts | 0.99-1.00 |
| meetings_length_ratio | 0.85-0.93 |

## Limits

- Trained and measured on English meetings of the AMI and ICSI corpora only.
- A small model: check its output before relying on it for names and numbers.
- Measured with the base and prompt above; other pairings are not measured.

## Training

Set `c1-edits` (SHA-256 `a12f50c7e68c047947300274dfd4e835cd755cb4aa13e42d64e844741fd8d77f`), trainer train_torch.py (torch 2.11.0+cu128, cuda), LoRA rank 8, alpha 16.

## Licence and attribution

Adapter licence: LicenseRef-Uhstray-Hyper-Tuned-Adapter-1.0. Base model licence: Apache-2.0.

The licence text is `LICENSE` and the full notice is `NOTICE`, in `models/hyper-tuned/` of the
`uhstray-io/zerds-public` repository.

> Attribution: Trained in part on text derived from the AMI Meeting Corpus and the ICSI Meeting Corpus, both CC BY 4.0; changes were made. Full notice: models/hyper-tuned/NOTICE.
