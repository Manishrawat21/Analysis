# PowerShell Encoded Command Detection

This repository documents practical detection research into Base64-encoded PowerShell command execution. It distills hands-on testing performed in a controlled Splunk lab and presents reproducible rules and guidance suitable for defenders and security engineers.

Table of contents

- [Scope](#scope)
- [What's included](#whats-included)
- [Detection summary](#detection-summary)
- [False positives and limitations](#false-positives-and-limitations)
- [Sigma rule and usage](#sigma-rule-and-usage)
- [Testing methodology](#testing-methodology)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements & References](#acknowledgements--references)


## Scope

This repository focuses on how PowerShell encoded commands appear in real-world logs, why naive string matching often fails when parameters vary, and which detection approaches proved reliable in our Splunk lab. It is defensive research only — not malware, tooling for attackers, or copied documentation.

## What's included

- Examples of how encoded PowerShell execution is logged across common Windows hosts and agents
- Detection logic that we validated in Splunk (search queries and SPL samples)
- Notes on observed false positives and edge cases
- A portable Sigma rule derived from lab results
- Reproducible test cases used during validation

## Detection summary

Key findings:

- Encoded PowerShell invocations vary in parameter ordering and quoting; simple substring matches (e.g., "-EncodedCommand") can be bypassed or produce noisy results.
- Detection that normalizes parameters and checks for Base64-structured arguments plus execution contexts (e.g., parent process, user account, telemetry source) is more reliable.
- Combining string checks with entropy-based heuristics and context filters greatly reduced false positives in our lab.

For full detection details and the working Splunk SPL, see the `detections/` folder (or the `Sigma` rule in `sigma/`).

## False positives and limitations

- Some legitimate administrative tooling encodes PowerShell commands for transport; these generate similar artifacts and must be accounted for in a production deployment.
- Filebeat/Winlogbeat/other agent logging differences mean not all events contain the same fields; adapt queries to your telemetry.
- This work does not guarantee detection of obfuscated or multi-stage loaders that do not use clear encoded arguments.

## Sigma rule and usage

A portable Sigma rule is included to help operators deploy the logic across different SIEMs. The rule is a translation of our validated Splunk logic, and should be tuned to your environment (whitelist benign tooling, adjust thresholds, and refine context filters).

See `sigma/encoded_powershell.yml` for the rule and mapping notes.

## Testing methodology

- Lab environment: Windows hosts with default PowerShell and common logging agents; Splunk for indexing and rule validation.
- Tests exercised variations in quoting, parameter order, and common wrappers used by deployment tools.
- Results were measured by true/false positive counts using the supplied test cases in `tests/`.

## Contributing

Contributions are welcome. Please open a pull request or file an issue describing the change. When proposing detection changes, include the test case and observed logs so we can reproduce.

## License

This repository is released under the MIT License. See `LICENSE` for details.

## Acknowledgements & References

This work is based on hands-on testing and is documented in a longer write-up available on my Medium blog. Links and additional references are included in the `references.md` file.
