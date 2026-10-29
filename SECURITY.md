LFIA — Security Policy

1. Purpose

LFIA (Local File Interface for AI) is designed to provide MCP-compatible AI applications with controlled access to files on a user's local device.

Because filesystem access can expose private information or modify important files, security is a core requirement of the project.

2. Current Security Status

LFIA is currently in the planning and architecture stage.

The security measures described in this document are requirements for future development. They must not be interpreted as implemented, tested, or guaranteed features until verified in the code.

LFIA must not be considered ready for sensitive or confidential files until its security controls have been implemented and tested.

3. Core Security Principles

The project should follow these principles:

- Least privilege: Access only the directories and operations explicitly authorized by the user.
- Explicit boundaries: Never assume permission to access the entire filesystem.
- Read and write separation: Keep file-reading operations separate from operations that create, edit, or delete files.
- Path validation: Reject paths that escape the configured directories.
- No unrestricted command execution: Filesystem tools must not provide unrestricted access to the operating system shell.
- Data transparency: Explain when file contents may be transmitted to an external AI provider.
- Recoverability: Design file modifications to reduce accidental data loss wherever practical.

4. Local File Access

Future implementations must:

- Restrict access to user-configured directories.
- Validate requested paths before performing operations.
- Account for symbolic links and filesystem edge cases.
- Reject unauthorized paths and operations.
- Handle permission errors safely.
- Avoid exposing unrelated files, credentials, or system data.
- Limit file sizes and resource usage where appropriate.

Path validation must remain effective even when paths contain relative components, symbolic links, or other mechanisms that could bypass directory restrictions.

5. File Modification

Operations that modify files require additional safeguards.

The implementation should:

- Clearly distinguish read-only tools from write-capable tools.
- Validate the destination before writing.
- Avoid silently overwriting existing files when safer alternatives are available.
- Provide clear feedback about successful and failed changes.
- Consider backups, temporary files, or other recovery mechanisms.
- Never claim that a change was saved unless the operation actually succeeded.

Deletion and unrestricted bulk modification should remain outside the initial prototype unless a clear security model is established.

6. AI Providers and Data Privacy

LFIA is intended to operate locally as a filesystem access layer, but this does not mean that all AI processing will necessarily remain local.

When an AI application uses an external provider, file contents or excerpts may be transmitted outside the device.

Documentation and user interfaces should clearly explain:

- Which files the AI can access.
- Which content may be sent to an external provider.
- Which application or service processes that content.
- How users can restrict access.

LFIA must not claim that data is completely private or never leaves the device unless the relevant architecture and data flow support that claim.

7. Credentials and Secrets

- Never commit API keys, passwords, access tokens, or private credentials to the public repository.
- Use appropriate local configuration or environment variables for secrets when needed.
- Keep sensitive configuration files out of version control.
- If a secret is accidentally published, revoke or rotate it as appropriate; deleting it from the latest commit alone may not remove it from repository history.

8. MCP Integration

MCP compatibility does not automatically guarantee security.

The implementation must evaluate how the selected MCP client launches, connects to, and authorizes the LFIA service.

The service should validate incoming requests and must not rely solely on the AI application's instructions to enforce filesystem boundaries.

9. Reporting a Vulnerability

If you discover a potential security vulnerability, please avoid publishing sensitive exploit details or private user data in a public issue.

Until a dedicated private reporting channel is established, do not include secrets, personal files, or sensitive logs in public reports.

A private security contact and disclosure process may be added as the project develops.

10. Security Testing

Before LFIA is considered suitable for sensitive files, testing should include:

- Access to permitted and forbidden directories.
- Attempts to escape configured directories.
- Symbolic-link and path traversal cases.
- Unauthorized file modifications.
- Unexpected, malformed, or oversized requests.
- Permission failures and missing files.
- Accidental exposure of secrets.
- Data flows between LFIA and external AI providers.

Security tests must be repeated when relevant filesystem or integration code changes.

11. Scope and Disclaimer

LFIA is an evolving open-source project. This policy describes intended security requirements, not a guarantee that the software is secure.

Users should not grant access to sensitive files until the relevant protections have been implemented, reviewed, and tested.

12. License

MIT License.
