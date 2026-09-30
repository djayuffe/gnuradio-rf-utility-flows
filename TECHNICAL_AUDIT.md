# Technical Audit

This audit summarizes code, functions, and feature coverage for `gnuradio-rf-utility-flows`.

## Scope

- Flowgraphs audited: 3 modern files plus archived originals in `flows/`.
- Tools audited: `tools/audit_flows.py` and `tools/validate_grc.py`.
- Reports regenerated locally before publication.

## Code and Function Review

- `tools/audit_flows.py` parses XML with `xml.etree.ElementTree`, hashes each file, lists block counts, connection counts, hardware endpoints, transmit-capable sinks, explicit file paths, duplicate block IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses the installed GNU Radio Companion core API, not text matching, to load, rewrite, and validate each modern `.grc` file.
- Shell examples avoid executing generated RF graphs automatically; generation and validation are separate from runtime operation.

## Feature Coverage

- 433.967 MHz receiver utility flow
- Audio-to-SDR transmit test flow
- WAV/audio/file experiment flow
- Qt GUI conversions for legacy display blocks
- Transmit-capable test graph isolated from receiver repos

## Technical Parameters

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `Uber-rf.grc` | 24 | 8 | samp_rate=1e6; freq=433.967e6; rf_gain=10 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |
| `test.grc` | 12 | 5 | rf_gain=10; freq=93.3e6 | audio_source_0 (audio_source); osmosdr_sink_0 (osmosdr_sink) | osmosdr_sink_0 (osmosdr_sink) |
| `untitled.grc` | 8 | 5 | samp_rate=20000000 | audio_sink_0 (audio_sink) | - |

## Known Operational Gaps

- Runtime hardware behavior is not asserted by validation; actual SDR/audio devices must be configured locally.
- External sample/capture files named in legacy graphs are not bundled unless present in `flows/`.
- Transmit-capable graphs require separate RF lab controls and legal authorization.

## Verification

- `VALIDATION.md` has no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.
