# GNU Radio RF Utility and Test Flows

Modern GNU Radio utility and hardware test flowgraphs for RF/audio experiments.

This public repository is split from the audited `modern-gnuradio-sdr-flows` workspace. It keeps a focused GNU Radio Companion flow family with archived originals in `flows/` and validated modern ports in `modern/`.

## Features

- 433.967 MHz receiver utility flow
- Audio-to-SDR transmit test flow
- WAV/audio/file experiment flow
- Qt GUI conversions for legacy display blocks
- Transmit-capable test graph isolated from receiver repos

## Standards and Signal Context

- General SDR utility/test graphs
- GNU Radio Companion XML validated with GNU Radio 3.8.5.0

## Flowgraph Inventory

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `Uber-rf.grc` | 24 | 8 | samp_rate=1e6; freq=433.967e6; rf_gain=10 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |
| `test.grc` | 12 | 5 | rf_gain=10; freq=93.3e6 | audio_source_0 (audio_source); osmosdr_sink_0 (osmosdr_sink) | osmosdr_sink_0 (osmosdr_sink) |
| `untitled.grc` | 8 | 5 | samp_rate=20000000 | audio_sink_0 (audio_sink) | - |

## File and Capture Paths

- `Uber-rf.grc`: gr_file_sink_0.file=/tmp/fifo
- `test.grc`: no explicit file paths found
- `untitled.grc`: blocks_wavfile_source_0.file=/home/ulf/key.wav; gr_file_sink_0.file=/home/ulf/hack/data.wav

Update these paths before running graphs on a different machine. Generated files, captures, recordings, and raw samples are intentionally ignored by git.

## Usage Examples

```sh
# Validate modernized flowgraphs
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md

# Generate Python without running RF hardware
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done

# Verify committed file integrity
shasum -a 256 -c SHA256SUMS.txt
```

To open a graph interactively:

```sh
gnuradio-companion modern/<flowgraph>.grc
```

To run generated Python, inspect the generated script first and confirm hardware, frequency, gain, sample rate, and file paths. Do not run transmit-capable graphs directly from generated code without RF isolation and legal authorization.

## Safety

`test.grc` contains an `osmosdr_sink` transmit path. Use a dummy load or shielded setup, verify frequency/gain, and obey local law before running.

## Audit Status

- Archived originals parse as XML. See `AUDIT.md`.
- Modernized flowgraphs validate OK. See `VALIDATION.md`.
- Python generation was verified with GNU Radio Companion Compiler 3.8.5.0. See `COMPILE.md`.
- Checksums are tracked in `SHA256SUMS.txt`.

## Repository Layout

- `flows/` - archived original flowgraphs and related data files.
- `modern/` - modernized GNU Radio Companion flowgraphs for normal use.
- `tools/` - repeatable audit and validation helpers.
- `README.md` - usage and technical overview.
- `DESCRIPTION.md` - short project description.
- `AUDIT.md`, `VALIDATION.md`, `COMPILE.md` - generated audit/verification reports.

## License

No new license is asserted for the archived flowgraphs. Preserve original ownership/history before redistribution or publication.
