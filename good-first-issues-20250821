# OpenHands Good First Issues - August 21, 2025

This document contains an analysis of 100+ recent issues from the OpenHands repository to identify good first issues suitable for new contributors. These issues are well-defined, have clear solutions, and are appropriately scoped for first-time contributors.

## Top 10 Good First Issues

### 1. **Issue #10499**: [Bug]: Welcome page should show OPENHANDS_API_KEY_HELP for OpenHands Provider
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10499  
**Labels**: bug, OH UI/UX, frontend, Needs Design  
**Why it's a good first issue**: Simple frontend text display fix - just needs to conditionally show existing translation key `SETTINGS$OPENHANDS_API_KEY_HELP` when OpenHands provider is selected in the LLM configuration welcome page.

### 2. **Issue #10501**: UI shows red "x" for Tavily MCP results even when isError=false  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10501  
**Labels**: None  
**Why it's a good first issue**: Well-documented bug with specific code location (`get-observation-result.ts`) and suggested fix already provided - just needs to parse JSON and check isError flag instead of substring matching for "error:".

### 3. **Issue #10523**: Tweak labels prompt  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10523  
**Labels**: enhancement  
**Why it's a good first issue**: Simple text movement task - move existing instruction from microagents to tool description in `create_pr`/`create_mr` tool to prevent GPT-5 from inventing labels.

### 4. **Issue #10536**: [Evaluation] evaluation shouldn't save session data to ~/.openhands/sessions  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10536  
**Labels**: enhancement, evaluation, openhands  
**Why it's a good first issue**: Clear path configuration change - update `file_store_path` in `run_infer.py` files to use `.eval_sessions` instead of `~/.openhands/sessions` and add to gitignore.

### 5. **Issue #10555**: [Bug]: Settings page shows duplicate element IDs for React Aria controls  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10555  
**Labels**: bug, frontend  
**Why it's a good first issue**: Frontend accessibility fix with clear reproduction steps and detailed analysis - needs to ensure unique ID generation for React Aria controls on settings page.

### 6. **Issue #10428**: Add styling tips in system_prompt for models like GPT-5  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10428  
**Labels**: enhancement, openhands, OH UI/UX, agent  
**Why it's a good first issue**: Simple documentation/prompt enhancement - add formatting guidelines to `system_prompt.j2` with specific suggestions provided (bold text, single-layer sections, single-layer bullets).

### 7. **Issue #10411**: [Bug]: CLI file edit action/observation didn't show "create"  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10411  
**Labels**: bug, openhands, CLI  
**Why it's a good first issue**: Frontend/CLI display bug with clear issue - file edit actions show wrong message when creating files, needs to fix visualization of file edit actions in CLI.

### 8. **Issue #10355**: OpenHands error windows_bash.py:92 - DotNetMissingError not defined  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10355  
**Labels**: bug, windows  
**Why it's a good first issue**: Simple Python import/exception handling fix - clear NameError for undefined `DotNetMissingError` in `windows_bash.py` line 92.

### 9. **Issue #10212**: [Enhancement]: Update @vscode/vsce package in VS Code extension  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10212  
**Labels**: enhancement, dependencies  
**Why it's a good first issue**: Simple dependency update with clear instructions - update `@vscode/vsce` from 3.5.0 to 3.6.0 in VS Code extension package.json.

### 10. **Issue #10211**: [Security]: VS Code extension has npm vulnerabilities  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10211  
**Labels**: None  
**Why it's a good first issue**: Security fix with clear solution - run `npm audit fix` in `openhands/integrations/vscode` directory to fix 2 vulnerabilities (1 critical, 1 low).

## Honorable Mentions / Runner-ups

These issues are also good candidates but may require slightly more investigation or have some complexity:

### **Issue #10059**: [Bug]: OpenHands CLI hangs on "Initializing..." when uvx command not found  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10059  
**Labels**: bug, CLI, mcp  
**Why it's notable**: Dependency update fix with clear root cause analysis and tested solution - upgrade FastMCP dependency from 2.6.1 to 2.11.0.

### **Issue #10525**: Document SecurityAnalyzer: event stream subscription pattern and architecture overview  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10525  
**Labels**: None  
**Why it's notable**: Documentation task with detailed requirements and code examples provided - create developer guide for SecurityAnalyzer event stream subscription pattern.

### **Issue #10563**: Question regarding E2B runtime and the other remote runtime  
**URL**: https://github.com/All-Hands-AI/OpenHands/issues/10563  
**Labels**: enhancement  
**Why it's notable**: Documentation/clarification issue about E2B runtime status and third-party directory - good for someone familiar with runtime architecture.

## Analysis Summary

- **Total Issues Analyzed**: ~100 recent issues from OpenHands repository
- **Issues Identified**: 10 primary good first issues + 3 runner-ups
- **Common Categories**: Frontend bugs, CLI improvements, documentation updates, dependency updates, configuration changes
- **Complexity Level**: All selected issues are scoped for completion within reasonable timeframes for new contributors
- **Assignment Status**: All issues are currently unassigned and available for work

## Contribution Guidelines

For contributors interested in these issues:

1. **Check Assignment**: Verify the issue is still unassigned before starting work
2. **Comment First**: Leave a comment indicating your intent to work on the issue
3. **Follow Repository Guidelines**: Review the CONTRIBUTING.md and ensure pre-commit hooks are installed
4. **Test Changes**: Ensure all lint checks pass before submitting PRs
5. **Small Scope**: Keep changes focused and minimal to address the specific issue

## Repository Context

- **Repository**: All-Hands-AI/OpenHands
- **Analysis Date**: August 21, 2025
- **Issue Range**: Most recent 100+ open issues
- **Focus**: Issues suitable for first-time contributors to the OpenHands codebase

---

*This analysis was conducted to help identify accessible entry points for new contributors to the OpenHands project. Issues were selected based on clear problem definitions, straightforward solutions, and appropriate scope for first-time contributors.*
