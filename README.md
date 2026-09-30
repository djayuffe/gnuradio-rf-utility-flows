# GNU Radio RF Utility and Test Flows

Utility SDR flowgraphs for receiver testing, audio/file experiments, and hardware-path checks.

This private repository is split from `modern-gnuradio-sdr-flows` and keeps a focused subset of related GNU Radio Companion flowgraphs. Files in `flows/` are archived originals. Files in `modern/` are the working GNU Radio Companion ports.

## Contents

- `flows/` - original archived flowgraphs and related source files.
- `modern/` - modernized `.grc` files validated with GNU Radio Companion 3.8.5.0 on this Mac.
- `AUDIT.md` - structural audit of the archived originals.
- `VALIDATION.md` - validation result for modernized files.
- `COMPILE.md` - compiler/generation result summary.
- `tools/` - repeatable audit and validation helpers.
- `SHA256SUMS.txt` - integrity hashes for committed files.

## Modern Flowgraphs

- `modern/Uber-rf.grc`
- `modern/untitled.grc`
- `modern/test.grc`

## Archived Originals

- `flows/Uber-rf.grc`
- `flows/untitled.grc`
- `flows/test.grc`

## Notes

- `test.grc` contains an `osmosdr_sink` transmitter path; review RF safety before running.
- `Uber-rf.grc` writes to `/tmp/fifo`; adjust path if needed.
- `untitled.grc` references `/home/ulf/...` paths in the archive.

## Verify

```sh
python3 tools/audit_flows.py flows --report AUDIT.md
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md
shasum -a 256 -c SHA256SUMS.txt
```

To generate Python from the modernized flowgraphs:

```sh
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done
```

`generated/` is intentionally ignored. Commit the `.grc` sources and reports, not generated Python output.

## License

No new license is asserted for the archived flowgraphs in this private repository. Preserve any original ownership/history before redistribution or publication.
