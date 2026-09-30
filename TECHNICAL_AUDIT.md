# Technical Audit

This audit covers the modern-only public repository `gnuradio-rf-utility-flows`.

## Scope

- Modern flowgraphs audited: 3.
- Outdated public XML removed from the repo.
- Repo-local file paths used for samples/captures.
- GNU Radio Companion validation target: 3.8.5.0.

## Tooling Review

- `tools/audit_flows.py` parses GRC XML, hashes each file, reports block/connection counts, hardware endpoints, transmit-capable sinks, file paths, duplicate IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses GNU Radio Companion's Python API to load, rewrite, and validate each modern `.grc`; it does not rely on ad hoc text matching.
- Setup scripts, where present, create safe placeholder local files only. They do not run SDR hardware.

## Feature and Parameter Coverage

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `Uber-rf.grc` | 24 | 8 | samp_rate=1e6; freq=433.967e6; rf_gain=10 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |
| `test.grc` | 12 | 5 | rf_gain=10; freq=93.3e6 | audio_source_0 (audio_source); osmosdr_sink_0 (osmosdr_sink) | osmosdr_sink_0 (osmosdr_sink) |
| `untitled.grc` | 8 | 5 | samp_rate=20000000 | audio_sink_0 (audio_sink) | - |

## File Path Coverage

- `Uber-rf.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `test.grc`: no explicit repo-local file paths
- `untitled.grc`: blocks_wavfile_source_0.file=samples/key.wav; gr_file_sink_0.file=captures/data.wav

## Remaining Runtime Responsibilities

- GRC validation and `grcc` generation do not prove connected SDR/audio hardware behavior.
- Users must configure local devices, antennas, sample files, and gains.
- Transmit-capable graphs require RF isolation and authorization before any runtime use.

## Verification Checklist

- `VALIDATION.md` contains no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.
- Generated Python and runtime captures remain ignored by git.
