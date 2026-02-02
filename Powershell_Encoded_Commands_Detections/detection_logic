## Detection approach

Encoded PowerShell execution alone is not malicious.

Detection becomes useful when encoding is combined with context.

Key observations from testing:

- Parameter variations defeat simple keyword searches
- Dash characters break token based indexing
- Regex matching is required for reliable coverage
- ScriptBlock logging provides the strongest signal

Encoded commands should be treated as a hunting signal, not an alert by default.

The most reliable detections combined:
- Encoded execution
- Execution hiding
- Dynamic code execution
- Download activity
