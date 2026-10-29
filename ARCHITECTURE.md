# FreeDesk AI — Architecture

## 1. Purpose

This document describes the planned technical structure of FreeDesk AI. The architecture is a proposal and must be validated during implementation.

## 2. Technology Direction

- Language: Python
- Desktop UI: PySide6
- First target platform: Windows
- Future platform: Linux
- AI providers: provider-independent integration, with OpenRouter as one possible option

## 3. Main Components

### 3.1 User Interface

Provides the desktop windows, file selection controls, operation-mode selection, confirmation prompts, and status messages.

### 3.2 File Selection

Allows the user to explicitly choose a file through a standard file picker. The application must not scan the whole computer or access unrelated files.

### 3.3 Workspace and Copy Manager

Creates and manages separate working copies for Copy and Edit mode. It records which source file a working copy came from and avoids silently overwriting the original.

### 3.4 Original File Editor

Handles Edit Original mode only after clear user confirmation. Before implementation, this component must have a documented backup, error-handling, and recovery strategy.

### 3.5 Backup and Recovery

Creates backups where feasible, detects failures, and helps users recover from unsuccessful operations. Backup behavior must be tested before direct editing is considered ready.

### 3.6 AI Provider Adapter

Provides a consistent interface for communicating with supported AI providers. API keys must not be committed to source control, and users must be informed before file content is sent to an external provider.

### 3.7 Tests and Logging

Tests file operations, permission boundaries, copy integrity, failure cases, and recovery behavior. Logs must avoid exposing file contents, secrets, or unnecessary personal information.

## 4. File Operation Flows

### Copy and Edit

1. The user selects a file.
2. The application validates the selection and creates a separate working copy.
3. The user requests an AI-assisted operation.
4. The application sends only the necessary content to the chosen provider, with user awareness and consent.
5. The result is applied to the working copy.
6. The original file remains unchanged.

### Edit Original

1. The user selects the original file.
2. The application explains that the original will be modified.
3. The user explicitly confirms.
4. The application creates and verifies a backup where feasible.
5. The application applies the approved change.
6. The application reports success or failure and provides recovery guidance.

## 5. Security Principles

- Follow least-privilege access.
- Operate only on user-selected files and resources necessary for the requested task.
- Do not silently modify originals.
- Keep API credentials out of source control.
- Make external data transfers clear to the user.
- Treat file selection and application checks as safeguards, not as a complete security sandbox.
- Evaluate stronger isolation separately where needed.

## 6. Proposed Development Order

1. Confirm requirements and security assumptions.
2. Create the minimal PySide6 application.
3. Implement file selection.
4. Implement Copy and Edit mode.
5. Add tests for original-file integrity and failure handling.
6. Design and test backup and recovery.
7. Implement Edit Original mode behind explicit confirmation.
8. Add the AI provider adapter.
9. Build and test on Windows.
10. Evaluate Linux support.

## 7. Open Questions

- Which file formats should be supported first?
- Should AI operations work on entire files or selected text initially?
- How should the application manage temporary copies and their deletion?
- What backup retention policy should be used?
- Which AI providers should be supported first?

## 8. Current Status

This architecture is a planning document. Components and workflows described here are not yet implemented or verified. Update this file as technical decisions are tested and confirmed.
