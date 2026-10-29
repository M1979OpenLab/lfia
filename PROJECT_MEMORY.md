LFIA — Project Memory

1. Project Goal

LFIA (Local File Interface for AI) is an open-source local file-access layer for AI systems compatible with the Model Context Protocol (MCP).

Official Persian definition:

«لایه‌ای متن‌باز برای اتصال هوش‌های مصنوعی سازگار به فایل‌های محلی سیستم‌عامل بر پایه MCP»

2. Core Principle

LFIA provides controlled access to local files. The connected AI does the thinking.

LFIA is not an AI agent. It does not reason, analyze, or make decisions. It validates file-access requests, enforces permissions, and performs permitted file operations.

3. Key Decisions

- Access is limited to folders explicitly authorized by the user.
- The project prioritizes simplicity, speed, security, and practical use.
- Initial file support focuses on source code and text documents.
- The architecture should allow additional document formats later.
- The connected AI may work across multiple related project files.
- Large projects may need to be read in smaller parts.
- A Markdown file serves as the project's memory; no complex built-in memory engine is planned.
- GitHub is optional, not a required component of LFIA.

4. Privacy Modes

Two mutually exclusive modes are planned.

Mode 1: Protect Original Files

Protect original files from being copied or moved elsewhere as part of the workflow. This does not prevent file contents from being sent to a cloud AI provider.

Mode 2: Strict Local Privacy

Protected content must remain on the device. This requires a local AI or another verified architecture that prevents external transmission. Incompatible connections must be rejected.

These modes are planned requirements and must not be described as implemented until verified by tests.

5. Project Documents

- "README.md" — project introduction and overview.
- "PROJECT_STATUS.md" — current development status.
- "ARCHITECTURE.md" — system design and responsibilities.
- "MVP.md" — requirements for the first usable version.
- "SECURITY.md" — security principles and vulnerability reporting.
- "PROJECT_MEMORY.md" — decisions, progress, issues, and next steps.

6. Current Status

The project is in the planning and documentation stage. A working service and its security controls have not yet been verified.

Documentation has been created or updated for the project overview, architecture, MVP scope, and security principles.

7. Next Steps

1. Review the project documents for consistency.
2. Choose the simplest suitable implementation language and MCP approach.
3. Build a minimal local MCP service.
4. Restrict access to explicitly authorized folders.
5. Test basic file listing, reading, searching, creation, and editing.
6. Test the service with one compatible AI application.
7. Implement and verify the privacy modes before claiming they provide protection.

8. Rules for Updating This File

After important project work, the connected AI should update this file with concise summaries of decisions, changed files, current status, known issues, and next steps.

Do not duplicate entire source files or conversations. Record only information needed to continue the project accurately.

This file is a normal Markdown document, not an intelligent memory engine. LFIA itself does not guarantee that an AI application will update it.
