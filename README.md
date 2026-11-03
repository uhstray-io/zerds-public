# zerds-public

Public assets that [Zerds](https://github.com/uhstray-io/zerds) downloads at
runtime. This repository exists **only** because the main Zerds repository is
private: GitHub release assets inherit their repository's visibility, so an app
running on a user's machine — an anonymous client — cannot fetch them.

Nothing proprietary lives here. Everything in this repository is either an
open-source model redistributed under its own license, or a file Zerds needs to
be publicly reachable.

## Contents

| Path | What it is | License |
|---|---|---|
| `models/yamnet/model.onnx` | YAMNet audio-event classifier, converted from the official TensorFlow Hub model to ONNX. Takes a 1-D 16 kHz mono waveform and returns 521 AudioSet class scores per ~0.48 s frame. Zerds uses it to mark laughter, applause, cheering, crying, coughs and sneezes on the timeline. | Apache-2.0 — see [`models/yamnet/LICENSE`](models/yamnet/LICENSE) and [`models/yamnet/NOTICE`](models/yamnet/NOTICE) |
| Release [`nv-diarization-3-v1`](https://github.com/uhstray-io/zerds-public/releases/tag/nv-diarization-3-v1) (optional) | NV Diarization 3, the int8 ONNX speaker-diarization model (graph `model_quantized.onnx` plus weights `model_quantized.onnx_data`, about 120 MB). An optional second source for networks that block the upstream host; Zerds downloads the upstream copy first. Too large for git, so it is a release asset. | OpenMDW-1.1, see [`models/nv-diarization-3/LICENSE`](models/nv-diarization-3/LICENSE) and [`models/nv-diarization-3/NOTICE`](models/nv-diarization-3/NOTICE) |

## Integrity

Every file here is pinned by SHA-256 in the Zerds source. A download whose
digest doesn't match the pinned value is rejected before it reaches the
runtime, so replacing a file in this repository does not silently change what
users run — it makes their download fail until Zerds is updated to match.

Current digests:

```
9a6aef46391df10a4ff804ea196266855a532a200ec13894024da24e16aaf7b1  models/yamnet/model.onnx
fff7d18c7439c9fdc1c6c4dfec924cb42d3344264ca879780dfaf7ee886e6c1e  model_quantized.onnx       (release nv-diarization-3-v1)
002d7483e1c865c35c82220fdb378f185ff213c6d35922b38ae421c8ec72c338  model_quantized.onnx_data  (release nv-diarization-3-v1)
```

Verify locally with:

```sh
shasum -a 256 models/yamnet/model.onnx
```

## Adding files

Two constraints worth knowing before adding anything large:

- **GitHub rejects files over 100 MB** (and warns above 50 MB).
- **Git keeps every version forever.** Replacing a binary does not free the old
  one; the repository only grows, and every clone pays for it.

So this tree suits assets in the tens of megabytes. For anything larger — the
Whisper models are hundreds of MB, GGUF language models are gigabytes — use a
GitHub **release** on this repository instead: release assets are public here
too, are served from a CDN, have no practical size limit, and stay out of git
history.

## How the YAMNet model was produced

Not hand-converted. `.github/workflows/build-yamnet-onnx.yml` in the Zerds
repository converts the official Apache-2.0 TF-Hub model with `tf2onnx` and
validates the result in the same run — graph shape, frame counts against
YAMNet's 0.96 s window / 0.48 s hop, and numeric parity against the original
TensorFlow model. It refuses to publish anything that fails. The build that
produced this file reported a maximum score difference of 1.2e-06 against
TensorFlow and 100% top-class agreement across four waveform lengths.
