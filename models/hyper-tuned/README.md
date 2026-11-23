# Hyper Tuned adapters

Small LoRA adapter files that [Zerds](https://github.com/uhstray-io/zerds)
loads onto a small on-device language model, one adapter for each task:
transcript cleanup (light, medium, high), meeting summary and dictation.

**These files are Uhstray's own and are not open source.** They may be used
only as part of an application that Uhstray owns and distributes. Read
[`LICENSE`](LICENSE) before downloading anything; the credit for third-party
material is in [`NOTICE`](NOTICE). The base models are not here: each is
distributed by its own authors under the Apache License 2.0.

## Files

| File | What |
|---|---|
| [`manifest.json`](manifest.json) | every adapter version and every release: file name, size, SHA-256, download URL, the base model file it pairs with, the prompt template, the measured quality |
| [`latest.json`](latest.json) | the current release and the SHA-256 of `manifest.json` |
| [`CHANGELOG.md`](CHANGELOG.md) | what each release changed |
| `<adapter>/README.md` | a card for each adapter |

The adapter files themselves are assets of this repository's GitHub releases,
tag `hyper-tuned-v<version>`. An entry is never removed from the manifest; a
replaced version is marked `deprecated`.

## Release 1.0.0

| Adapter | Task | Base file | Version | Status | Size | SHA-256 |
|---|---|---|---|---|---|---|
| [`qwen3-0.6b-light`](qwen3-0.6b-light/README.md) | light | Qwen3-0.6B-Q4_K_M.gguf | 1.0.0 | stable | 10.1 MB | `c2b4ba997080fcf1b0ed8f3af9297f32b8d7ff7632ae9d248283e458f5f0ebdc` |
| [`qwen3-1.7b-light`](qwen3-1.7b-light/README.md) | light | Qwen3-1.7B-Q4_K_M.gguf | 1.0.0 | stable | 17.5 MB | `0712cf03f1716af6da8ba977e0f2a80c660836a867406a5d8c2f49fa7e2348a0` |
| [`qwen3-0.6b-medium`](qwen3-0.6b-medium/README.md) | medium | Qwen3-0.6B-Q4_K_M.gguf | 1.0.0 | stable | 10.1 MB | `487366add0ed805293d8fe811ff2981455c0368932e069f432842950c05f8b34` |
| [`qwen3-1.7b-medium`](qwen3-1.7b-medium/README.md) | medium | Qwen3-1.7B-Q4_K_M.gguf | 1.0.0 | stable | 17.5 MB | `4d0b1d7857e28c6879eecd93c1dc51f43ba8ad1c21a6d2cbbeabd47f8cb2537c` |
| [`qwen3-0.6b-high`](qwen3-0.6b-high/README.md) | high | Qwen3-0.6B-Q4_K_M.gguf | 0.1.0 | experimental | 20.2 MB | `1e9f917f24b65edbb753a70e7455b504698f42f29dd4c4521e06392a6cc2585d` |
| [`qwen3-1.7b-high`](qwen3-1.7b-high/README.md) | high | Qwen3-1.7B-Q4_K_M.gguf | 0.1.0 | experimental | 34.9 MB | `5c0340e6c56c6b252ca640a2ac2d6b0993ee20771306d35b6071da4bac8965fa` |
| [`minicpm5-2b-summary`](minicpm5-2b-summary/README.md) | summary | MiniCPM5-2B-Q4_K_M.gguf | 1.0.0 | stable | 50.3 MB | `9b2d02bf7e769d70427b3680aad52e001f70af1459ca8444d8cdae5c443adfd0` |
| [`qwen3-0.6b-dictation`](qwen3-0.6b-dictation/README.md) | dictation | Qwen3-0.6B-Q4_K_M.gguf | 1.0.0 | stable | 20.2 MB | `0227045912aff399888a8970cc9308373ad307bc3bd5afa0d7da85e8195ff1f2` |
| [`qwen3-1.7b-dictation`](qwen3-1.7b-dictation/README.md) | dictation | Qwen3-1.7B-Q4_K_M.gguf | 1.0.0 | stable | 34.9 MB | `56a2e6fb555723578131e0e3f07aff8ba878608c7fbeef02986ab8004c942713` |

An adapter is measured with the exact base file and prompt named in its
manifest entry. Zerds refuses any other pairing.
