# Contributing to CapCut MCP Server

Thank you for your interest in contributing to the CapCut Model Context Protocol (MCP) Server! We welcome pull requests, bug reports, and feature requests.

## Development Setup

1. **Prerequisites**:
   - Node.js >= 18.0.0
   - npm >= 9.0.0
   - CapCut Desktop or JianYing Pro installed (for live testing)
   - FFmpeg / FFprobe (optional, for media probing & proxy rendering)

2. **Clone & Install**:
   ```bash
   git clone https://github.com/capcut-mcp/capcut-mcp.git
   cd capcut-mcp
   npm install
   ```

3. **Build the Server**:
   ```bash
   npm run build
   ```

4. **Run Unit Tests**:
   ```bash
   npm test
   ```
   All tests run against synthetic video/audio in an isolated temporary directory.

## Project Structure

- `src/index.ts`: MCP server entrypoint declaring the 24 atomic tools and parameter schemas.
- `src/capcut/draft-builder.ts`: Generates and manipulates CapCut's internal `draft_content.json` Abstract Syntax Tree (AST).
- `src/capcut/draft-manager.ts`: High-level timeline actions (add clips, speed scale, transitions, keyframes, captions).
- `src/capcut/paths.ts`: Dynamic cross-platform path resolver for CapCut Global and JianYing Pro.
- `src/capcut/media.ts`: FFprobe wrapper for duration, resolution, and audio track inspection.
- `src/capcut/preview-renderer.ts`: Headless proxy video preview generator.
- `skills/capcut/`: Agent skill instructions and reference manuals for AI coding assistants.
- `schemas/`: Standalone JSON schemas for all 24 MCP tools.

## Pull Request Guidelines

1. Ensure all TypeScript code compiles with strict mode (`npm run build`).
2. Verify all unit tests pass (`npm test`).
3. If adding a new MCP tool:
   - Implement the tool in `src/index.ts`.
   - Update `src/capcut/draft-builder.ts` or `draft-manager.ts` if modifying timeline AST.
   - Add a unit test in `tests/draft-builder.test.ts`.
   - Add a corresponding JSON schema in `schemas/`.
   - Update `README.md` and `skills/capcut/SKILL.md`.
4. Ensure no sensitive credentials, paths, or personal tokens are committed.
