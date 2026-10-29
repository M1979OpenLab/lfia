LFIA — Architecture

1. Purpose

LFIA (Local File Interface for AI) is an open-source local file-access layer for AI systems compatible with the Model Context Protocol (MCP).

LFIA acts as a local file server. It exposes only the files and folders explicitly authorized by the user.

LFIA is not an AI agent. It does not reason, analyze, or make decisions. The connected AI is responsible for understanding files and deciding what changes are needed. LFIA provides the permitted file operations and enforces access boundaries.

2. Main Components

A. AI Application

The AI application connects to LFIA through MCP.

It is responsible for:

- Understanding and analyzing file contents.
- Working across related files in a project.
- Deciding which files to read or modify.
- Requesting permitted file operations.
- Maintaining the optional project memory file.

B. LFIA Local Service

LFIA runs locally and provides controlled access to authorized files.

Its planned operations include:

- Listing files and folders.
- Reading file contents.
- Searching file names and text.
- Creating new files.
- Editing and saving existing files.

LFIA validates each request and prevents access outside the configured locations. It does not decide whether an AI's proposed changes are logically correct.

C. Local Files and Projects

The user selects which folders or projects LFIA may expose.

The initial version focuses on source code and text documents. Support for additional formats, such as PDF and Word, may be added later.

The AI may work with one line, multiple pages, or related files across a project. Large projects may need to be read in smaller parts.

3. Request Flow

1. The user configures the permitted folders.
2. A compatible AI application connects to LFIA through MCP.
3. The AI requests access to specific files or operations.
4. LFIA checks the requested paths and permissions.
5. LFIA performs the allowed operation and returns the result.
6. The AI analyzes the result and decides what to do next.

4. Privacy Modes

LFIA is planned to support two mutually exclusive privacy modes.

Mode 1: Protect Original Files

This mode aims to protect original files from being copied or moved elsewhere as part of the workflow.

The AI may still receive file contents for analysis. If the connected AI uses a cloud provider, those contents may be transmitted outside the device.

This mode does not guarantee that file contents remain private.

Mode 2: Strict Local Privacy

This mode aims to keep file contents on the user's device.

It requires a local AI or another verified architecture that prevents external transmission of protected content.

If the connected AI application or provider cannot meet this requirement, LFIA must block or reject the incompatible connection or operation.

Enabling either mode automatically disables the other.

5. Project Memory

LFIA will not include a complex built-in memory engine.

Instead, a project may use a normal Markdown file, such as "PROJECT_MEMORY.md", as its logbook.

The connected AI can read and update this file to record:

- Project goals and important decisions.
- Reasons behind those decisions.
- Files changed and a short summary of the changes.
- Current status and known issues.
- Completed work and next steps.

The memory file should summarize important information rather than duplicate entire files or conversations.

LFIA only provides file access. The AI is responsible for maintaining the memory file. LFIA cannot guarantee that every AI application will update it.

Local Git or optional hosting and synchronization services may be used for versioning. GitHub is not required. In Strict Local Privacy mode, protected memory and project contents must not be synchronized to cloud services.

6. Security Boundaries

LFIA must:

- Restrict access to user-authorized folders.
- Reject attempts to access files outside those folders.
- Validate paths and handle symbolic links safely.
- Perform only supported and permitted file operations.
- Avoid unrestricted operating-system command execution.
- Protect secrets and avoid exposing unrelated system files.
- Clearly document when file contents may be sent to external AI providers.

MCP compatibility alone does not guarantee security.

7. Compatibility

LFIA is intended for AI applications that support MCP and can connect to a compatible local service.

Compatibility must be tested with actual client applications. LFIA should remain independent of any particular AI model or provider.

8. Current Status

This document describes the planned architecture. The service, file operations, privacy enforcement, and integrations have not yet been implemented or verified.

Implementation choices should be made incrementally, prioritizing simplicity, security, and practical use.
