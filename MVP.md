LFIA — Minimum Viable Product (MVP)

1. Goal

The first version of LFIA will provide a simple, controlled way for MCP-compatible AI applications to access files on the user's local device.

LFIA is a local file-access interface, not an AI agent. It does not analyze files, make decisions, or determine what changes are logically correct. The connected AI performs those tasks.

2. Initial Scope

The first version should support:

- Running a local MCP-compatible file service.
- Configuring one or more authorized folders.
- Listing files and folders within the authorized scope.
- Reading source code and text documents.
- Searching file names and text contents.
- Creating new files within the authorized scope.
- Editing and saving existing files within the authorized scope.
- Working with multiple related files in the same project.
- Returning clear results and errors to the connected AI.

The implementation should prioritize simplicity, reliability, and practical use.

3. Access Boundaries

LFIA must expose only folders explicitly selected or authorized by the user.

It must:

- Reject access outside authorized folders.
- Validate paths for every file operation.
- Prevent path traversal and unsafe symbolic-link access.
- Avoid unrestricted operating-system command execution.
- Never grant automatic access to the entire filesystem.

File deletion is outside the initial MVP scope.

4. File Support

The first version focuses on source code and text-based documents.

The design should allow additional file formats, such as PDF and Word, to be supported later.

The connected AI may request small sections, complete files, or information from multiple files. Large projects should be handled incrementally when necessary, rather than assuming all content can fit into one AI context.

5. Privacy Modes

The planned design includes two mutually exclusive modes.

Mode 1: Protect Original Files

The goal is to prevent original files from being copied or moved elsewhere as part of the workflow while still allowing their contents to be read by the AI.

This mode does not prevent file contents from being transmitted to an external AI provider.

Mode 2: Strict Local Privacy

The goal is to prevent protected file contents from leaving the user's device.

This mode requires a local AI or a verified architecture that blocks external transmission. Incompatible AI connections or operations must be rejected.

Enabling one mode must automatically disable the other.

Both modes must be implemented and tested before they are described as working security features. A setting alone is not sufficient to guarantee privacy.

6. Project Memory

The MVP will not include a complex built-in memory system.

Projects may use a Markdown file such as "PROJECT_MEMORY.md" to record:

- Project goals and important decisions.
- Reasons for important decisions.
- Files changed and summaries of changes.
- Current status and known issues.
- Completed work and next steps.

The connected AI is responsible for reading and updating this file. LFIA only provides the necessary file access and does not act as an intelligent memory manager.

Local Git may be used for version history. GitHub and other cloud services are optional. Strict Local Privacy mode must not permit protected project content or memory to be synchronized to the cloud.

7. Compatibility

The MVP should be tested with at least one real MCP-compatible AI application.

Compatibility with other applications should be added and verified incrementally. MCP support alone does not guarantee that every AI application can connect to LFIA.

8. Testing Requirements

Before the MVP is considered usable, tests must cover:

- Access to authorized folders.
- Rejection of unauthorized paths.
- Attempts to escape folder boundaries.
- File listing, reading, and searching.
- File creation and editing.
- Multiple files within a project.
- Missing files, invalid requests, and filesystem errors.
- Privacy-mode enforcement and incompatible connections.

9. Out of Scope

The initial MVP will not include:

- An autonomous AI agent.
- Independent reasoning or decision-making.
- A complex built-in memory engine.
- Unrestricted shell or command execution.
- Automatic access to the entire filesystem.
- File deletion.
- A mandatory cloud service or GitHub account.
- Advanced graphical interfaces.
- Guaranteed support for every AI application or document format.

10. Implementation Approach

The project should be developed incrementally:

1. Establish a working local MCP service.
2. Configure authorized folders and enforce access boundaries.
3. Implement and test basic file operations.
4. Connect one compatible AI application.
5. Add project-memory workflow guidance.
6. Implement and test the privacy modes before claiming they are enforced.
7. Expand compatibility and file-format support only when the core is reliable.

The implementation language, transport details, and installation method remain open until they can be selected based on compatibility, security, and ease of use.

11. Current Status

This document defines the planned MVP. The listed capabilities are requirements, not claims that the software has already been implemented.

The immediate priority is a small, reliable, secure local file-access service that follows the project's core principle:

LFIA provides controlled access to files. The AI does the thinking.
