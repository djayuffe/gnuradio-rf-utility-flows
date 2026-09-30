# GNU Radio RF Utility and Test Flows

Modern GNU Radio utility and hardware test flowgraphs for RF/audio experiments.

RF/audio utility flowgraphs with receiver and isolated transmit-test examples. The repository is modern-only: runnable GNU Radio Companion files live in `modern/`, use repo-local paths, and validate with GNU Radio Companion 3.8.5.0.

## Features

- Modern GNU Radio Companion XML only; outdated source XML was removed from the public repo.
- Qt GUI blocks replace old WX GUI patterns where applicable.
- Machine-specific paths were replaced with repo-local `samples/` and `captures/` paths.
- `tools/audit_flows.py` and `tools/validate_grc.py` provide repeatable checks.
- `SHA256SUMS.txt` tracks committed-file integrity.

## Flowgraphs

- `modern/Uber-rf.grc`
- `modern/test.grc`
- `modern/untitled.grc`

## Technical Inventory

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `Uber-rf.grc` | 24 | 8 | samp_rate=1e6; freq=433.967e6; rf_gain=10 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |
| `test.grc` | 12 | 5 | rf_gain=10; freq=93.3e6 | audio_source_0 (audio_source); osmosdr_sink_0 (osmosdr_sink) | osmosdr_sink_0 (osmosdr_sink) |
| `untitled.grc` | 8 | 5 | samp_rate=20000000 | audio_sink_0 (audio_sink) | - |

## Standards and Frequencies

- GNU Radio Companion target validated locally: 3.8.5.0.
- Frequency, sample-rate, and mode values are shown in the inventory table above from the actual `.grc` XML.
- Transmit-capable repositories include explicit RF safety text and keep transmit examples isolated.

## Repo-Local File Paths

- `Uber-rf.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `test.grc`: no explicit repo-local file paths
- `untitled.grc`: blocks_wavfile_source_0.file=samples/key.wav; gr_file_sink_0.file=captures/data.wav

## Setup Helpers

- `scripts/generate_placeholder_samples.py`

Run setup helpers only if you need placeholder files for local graph loading or non-radiating tests.

## Usage Examples

```sh
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done
shasum -a 256 -c SHA256SUMS.txt
```

Open a flowgraph interactively:

```sh
gnuradio-companion modern/<flowgraph>.grc
```

Inspect generated Python before running it. Confirm hardware, frequency, gain, sample rate, and paths every time.

## Safety

`test.grc` contains an osmocom transmit path. Use RF isolation and legal authorization before running.

## Audit Status

- Modern flowgraph audit: `AUDIT.md`.
- GNU Radio validation: `VALIDATION.md`.
- Generation summary: `COMPILE.md`.
- Technical review: `TECHNICAL_AUDIT.md`.

## License

No new license is asserted for the original flowgraph design lineage. Review provenance before redistribution in other projects.
