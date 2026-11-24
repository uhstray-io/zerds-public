# Base language models (mirror)

Unmodified copies of the three small language models that Zerds runs on the
device, kept here as a second source for networks that block the upstream
host. Each is Apache-2.0: see [`LICENSE`](LICENSE) and [`NOTICE`](NOTICE).

The files are too large for git, so they are assets of the release
[`base-models-v1`](https://github.com/uhstray-io/zerds-public/releases/tag/base-models-v1).

| File | Model | Bytes | SHA-256 |
|---|---|---|---|
| [`Qwen3-0.6B-Q4_K_M.gguf`](https://github.com/uhstray-io/zerds-public/releases/download/base-models-v1/Qwen3-0.6B-Q4_K_M.gguf) | Qwen3 0.6B | 396705472 | `ac2d97712095a558e31573f62f466a3f9d93990898b0ec79d7c974c1780d524a` |
| [`Qwen3-1.7B-Q4_K_M.gguf`](https://github.com/uhstray-io/zerds-public/releases/download/base-models-v1/Qwen3-1.7B-Q4_K_M.gguf) | Qwen3 1.7B | 1107409472 | `b139949c5bd74937ad8ed8c8cf3d9ffb1e99c866c823204dc42c0d91fa181897` |
| [`MiniCPM5-2B-Q4_K_M.gguf`](https://github.com/uhstray-io/zerds-public/releases/download/base-models-v1/MiniCPM5-2B-Q4_K_M.gguf) | MiniCPM5-2B | 1561318368 | `ec2d5801640099e97d8d7e8003ad4d81f336e757811f03a26173dddf386602fd` |

These are the exact files the [Hyper Tuned adapters](../hyper-tuned/README.md)
are measured with: the hashes are the ones in `models/hyper-tuned/manifest.json`.

Check a download:

```sh
shasum -a 256 Qwen3-0.6B-Q4_K_M.gguf
```
