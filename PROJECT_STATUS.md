# FreeDesk AI — Project Status

## 1. Project Overview

FreeDesk AI is an open-source desktop AI assistant for working with files explicitly selected by the user.

The initial target is Windows, with Linux support planned for a later stage.

GitHub repository: https://github.com/M1979OpenLab/freedesk-ai

## 2. Main Goals

- Provide a simple desktop interface for AI-assisted file work.
- Let users explicitly choose which files the application can work with.
- Keep file operations understandable and under user control.
- Build a public, community-friendly open-source project.
- Support AI providers through APIs as a later development stage.

## 3. File Operation Modes

### Mode A: Copy and Edit

1. The user selects a file.
2. The application creates a separate working copy.
3. AI-assisted changes apply only to the working copy.
4. The original file remains unchanged.
5. Changes are never automatically written back to the original.

### Mode B: Edit Original

1. The user explicitly selects the original file.
2. The application clearly warns that the original will be modified.
3. The user approves the operation.
4. The application creates a recoverable backup where feasible.
5. Changes are saved to the selected original file.
6. The application provides clear error handling and recovery guidance.

File selection and application-level restrictions are important safeguards, but they are not by themselves a complete security sandbox. Strong isolation must be evaluated separately.

## 4. Initial Technical Direction

- Preferred language: Python.
- Preferred desktop UI: PySide6.
- Initial platform: Windows.
- Future platform: Linux.
- Build and test incrementally, using cloud-based tools where practical.

These are provisional choices and should be validated before major implementation.

## 5. Security and Privacy Principles

- Work only with files explicitly selected by the user.
- Do not scan or modify the entire computer.
- Do not silently modify original files.
- Clearly distinguish working copies from originals.
- Protect API keys and never commit secrets to the repository.
- Explain what data is sent to external AI providers.
- Use least-privilege access and test file permissions carefully.

## 6. Project Status

Completed:
- Created the public GitHub repository.
- Added an initial README.
- Selected Python as the intended development language.
- Defined the two main file operation modes at the planning level.

Not yet completed:
- Finalize project documentation.
- Define the application architecture.
- Create the initial application skeleton.
- Implement and test file selection and copy handling.
- Implement backup and recovery behavior.
- Add AI provider integration.
- Add automated tests and build workflows.
- Test Windows first and Linux later.

## 7. Next Steps

1. Finalize README and project documentation.
2. Define a minimal architecture and threat model.
3. Build a small desktop prototype.
4. Implement safe file selection and working-copy behavior.
5. Add tests before implementing direct editing of original files.
6. Add AI provider integration after file handling is reliable.

## 8. Handoff Instructions for AI Assistants

When continuing this project:
- Read this file and README.md first.
- Explain steps in beginner-friendly language.
- The project owner has limited programming experience.
- Work incrementally and explain where each file belongs.
- Do not assume that a feature has been implemented just because it is described here.
- Confirm repository contents before proposing edits based on existing code.
- Prioritize file safety, privacy, tests, and recoverability.
- Keep documentation updated as decisions change.

## 9. Important Scope Boundary

FreeDesk AI should work only with user-selected files and resources necessary for the requested operation. It must not be presented as fully isolated or secure until those properties have been implemented and independently tested.
