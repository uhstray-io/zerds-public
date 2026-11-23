# minicpm5-2b-summary

A LoRA adapter for the Zerds meeting app: task **summary**, on the base model **openbmb/MiniCPM5-2B** (`MiniCPM5-2B-Q4_K_M.gguf`).

## What it does

Writes meeting notes from a transcript.

## Files

| Version | Status | Release | File | SHA-256 | Bytes |
|---|---|---|---|---|---|
| 1.0.0 | stable | hyper-tuned-v1.0.0 | [minicpm5-2b-summary-1.0.0.gguf](https://github.com/uhstray-io/zerds-public/releases/download/hyper-tuned-v1.0.0/minicpm5-2b-summary-1.0.0.gguf) | `9b2d02bf7e769d70427b3680aad52e001f70af1459ca8444d8cdae5c443adfd0` | 50274144 |

## Use

Load it with llama.cpp (converted with `b10200`) on the base file `MiniCPM5-2B-Q4_K_M.gguf`, SHA-256 `ec2d5801640099e97d8d7e8003ad4d81f336e757811f03a26173dddf386602fd`. Another quantisation of the base is not the pairing that was measured.

The adapter expects this prompt template (system prompt SHA-256 `5fd4d87ba7ca5cf4e7fcf17b02a723d0e6317bb84c90dffe47067d4d53f88269,75fa9f760d781d688ab14692c4bc2a14f6578c015c80734e5b3fbbd1c2149f1c`):

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

Gate: blind judges check every statement of the notes against the transcript (rubric bench/JUDGE.md), runs 43, 57, 64, 66 and 69. Passes its bar. Measured 2026-11-22.

| Measure | Value |
|---|---|
| statements_correct_release_configuration_8_meetings | 0.849 |
| statements_correct_raw_input_one_pass_long_meetings | 0.789 |
| statements_correct_raw_input_in_parts_long_meetings | 0.669 |
| wrong_speakers_per_100 | 3 |
| invented_actions | 6 in 8 meetings |

## Limits

- Trained and measured on English meetings of the AMI and ICSI corpora only.
- A small model: check its output before relying on it for names and numbers.
- Measured with the base and prompt above; other pairings are not measured.

## Training

Set `o1` (SHA-256 `babac76fc76b342cf285a79a41ebc53a99ead815990193c51963340d17c4954c`), trainer train_torch.py (torch 2.11.0+cu128, cuda), LoRA rank 16, alpha 32.

## Licence and attribution

Adapter licence: LicenseRef-Uhstray-Hyper-Tuned-Adapter-1.0. Base model licence: Apache-2.0.

The licence text is `LICENSE` and the full notice is `NOTICE`, in `models/hyper-tuned/` of the
`uhstray-io/zerds-public` repository.

> Attribution: Trained in part on text derived from the AMI Meeting Corpus and the ICSI Meeting Corpus, both CC BY 4.0; changes were made. Full notice: models/hyper-tuned/NOTICE.
