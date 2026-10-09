# Omniseal MCP service

Seal, retrieve, verify, and remove hidden files using PureCipher Omniseal.

## Connect

Remote Streamable HTTP endpoint:

```text
https://api.purecipher.com/mcp?platform=claude
```

No account, OAuth, or API key is required for the current public endpoint.
For Cline setup, see [llms-install.md](llms-install.md). Other MCP clients can
use the same endpoint with their HTTP transport configuration.

## Tools

- `seal_files`: conceal a secret file inside a supported cover.
- `retrieve_secret_file`: recover the hidden file using its private seed.
- `verify_sealed_file`: check seal integrity, without a seed.
- `remove_hidden_file`: create a new clean cover using the private seed.

Original input files are preserved. This repository contains the MCP connection documentation
configuration and instructions. The hosted service executes the Omniseal SDK.

## Inputs and output limits

Each file argument contains `file_name` and exactly one of `download_url`
(a service-reachable HTTPS URL) or `content_base64` (exact file bytes).
Local paths and chat attachments are not automatically uploaded.

Selected file contents and the operation seed are processed by PureCipher's
hosted service. Use an Omniseal seed, never an account password or API credential.
Inputs are limited to 6 MB per file and 10 MB combined for sealing. Responses are
limited to 140,000 serialized characters, typically about 100 KB of output bytes.
Outputs are binary MCP resources, not hosted download links. Client-side binary
rendering and saving have not yet been verified end to end.

The service URL is `https://api.purecipher.com/mcp?platform=claude`. The query
selects the existing compatible file schema; it does not send files to Anthropic.
The service is publicly reachable and requires no authentication.

## Validation

Validated with Gemini CLI 0.63.0: installation and MCP connection succeeded.
All four live MCP operations passed synthetic PNG/PDF tests, including exact
recovery of the secret bytes. Model-mediated execution remains unverified.

## Support

- [Omniseal](https://purecipher.com/solutions/omniseal)
- [Privacy policy](https://purecipher.com/privacy)
- [Terms](https://purecipher.com/terms)
- Email: support@purecipher.com

Copyright 2026 PureCipher. All rights reserved.
