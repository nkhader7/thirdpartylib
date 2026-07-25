# thirdpartylib

Small utility to assess whether third-party OSS vulnerabilities are likely exploitable.

## Run

```bash
python3 oss_exploitability.py --input input.json --output report.json --graph graph.dot
```

## Input format

```json
{
  "application": "payments-api",
  "dependencies": [
    {
      "name": "example-lib",
      "version": "1.2.3",
      "reachable": true,
      "runtime_exposed": true,
      "sandboxed": false,
      "entry_points": ["POST /payments"],
      "vulnerabilities": [
        {
          "id": "CVE-2025-0001",
          "severity": "high",
          "cvss": 8.3,
          "exploit_available": true,
          "fixed_version": "1.2.4"
        }
      ]
    }
  ],
  "calls": [
    ["handler:payments", "dep:example-lib:1.2.3"]
  ]
}
```

## Outputs

- JSON report with exploitability score, exploitable decision, missing details, and fix version.
- Graphviz DOT graph linking application -> dependency -> CVE and optional call edges.
