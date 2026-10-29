LFIA — Architecture

1. Purpose

LFIA (Local File Interface for AI) is an open-source layer that connects MCP-compatible AI systems to local filesystem operations.

Its purpose is to provide a reusable interface through which compatible AI applications can access permitted local files without requiring a separate file-access implementation for every AI system.

2. Design Goals

- Use the Model Context Protocol (MCP) as the primary integration protocol.
- Keep the local filesystem service independent of any specific AI model or provider.
- Make installation and configuration straightforward.
- Limit filesystem access to explicitly configured locations.
- Separate file reading from file modification.
- Provide predictable error handling and clear operation boundaries.
- Design the core so additional AI integrations and operating systems can be supported later.

3. High-Level Architecture

The planned system consists of three main layers.

A. AI Application

An AI application that supports MCP connects to LFIA and discovers the tools it exposes.

The AI application remains responsible for its own model, reasoning, and user interface.

B. LFIA Local Service

The local service implements the MCP interface and exposes a defined set of filesystem tools.

Planned tools include:

- List permitted directories and files.
- Read file contents.
- Search files and text within permitted locations.
- Create new files.
- Edit existing files.
- Save changes to permitted files.

The exact tool names, schemas, and capabilities will be defined during implementation.

C. Local Filesystem

The service operates on files stored on the user's device, subject to configured permissions and security checks.

It must not automatically expose the entire filesystem.

4. Request Flow

1. An MCP-compatible AI application connects to the LFIA service.
2. The application discovers the available tools.
3. The AI requests a filesystem operation.
4. LFIA validates the request and checks access permissions.
5. LFIA performs the permitted operation.
6. The result or an appropriate error is returned to the AI application.

5. Initial Scope

The first prototype should focus on:

1. Starting a local MCP service.
2. Configuring one or more permitted directories.
3. Listing files in those directories.
4. Reading supported text files.
5. Searching file names and text.
6. Creating or editing files only within permitted locations.
7. Testing the service with at least one compatible AI application.

Binary files, complex document formats, graphical interfaces, and advanced recovery features may be added later.

6. Security Design

Filesystem access is a security-sensitive capability.

The implementation must:

- Enforce configured directory boundaries.
- Validate paths and prevent path traversal.
- Account for symbolic links and other filesystem edge cases.
- Reject unauthorized operations.
- Avoid unrestricted command execution.
- Separate read-only tools from tools that modify files.
- Provide clear errors without leaking unnecessary sensitive information.
- Document that AI applications may transmit file content to external providers.
- Never assume that MCP compatibility alone guarantees security.

The security model must be tested before the project is considered suitable for sensitive files.

7. Transport and Installation

MCP transport and process-launch requirements will be selected according to the compatibility of target AI applications.

The initial target is Windows. Linux support may follow.

The project should prefer the simplest reliable installation method that works with the chosen MCP clients.

8. Implementation Language

The implementation language has not yet been finalized.

The choice should consider MCP library maturity, Windows compatibility, maintainability, testing, and ease of installation.

9. Testing Strategy

Tests should cover:

- Allowed and denied paths.
- Attempts to escape configured directories.
- File listing and reading.
- Search behavior.
- File creation and modification.
- Invalid requests and missing files.
- Filesystem errors and permission failures.
- Integration with an MCP-compatible client.

10. Current Status

This document describes the planned architecture. The service, tools, security controls, and integrations are not yet implemented or verified.

11. Open Questions

- Which MCP transport should the first prototype use?
- Which text file formats should be supported initially?
- How should write permissions be configured?
- Should file modifications require a separate approval mechanism in the client?
- Which MCP-compatible AI application should be used for the first integration test?
- Which implementation language best meets the project's requirements?

These decisions should be resolved incrementally before expanding the implementation.
