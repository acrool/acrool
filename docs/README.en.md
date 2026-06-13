# Acrool Desktop App

[Documentation Home](../README.md) | [繁體中文](README.zh-TW.md) | English

Acrool is a cloud task management platform designed from a software developer perspective. It helps teams manage tasks, projects, team collaboration, status workflows, and delivery progress in one focused workspace.

## Table of Contents

- [Product Overview](#product-overview)
- [Features](#features)
- [Download Acrool App](#download-acrool-app)
- [MCP Connection](#mcp-connection)
- [Report Issues](#report-issues)
- [Links](#links)

## Product Overview

Acrool is a user-experience-focused cloud task management system for software development, product, design, and cross-functional teams. Built around developer workflows, Acrool brings tasks, projects, teams, customer information, status workflows, and activity history into one workspace so teams can understand progress, assign ownership, and track delivery with less friction.

## Features

- **Status-grouped task lists**: Organize tasks by status and quickly review work that needs confirmation, testing, progress updates, or attention.
- **Task and project management**: Manage daily maintenance tasks and project tasks, including project stages, task status, quotations, user stories, design references, and customer information.
- **Gantt charts**: Visualize project schedules and team allocation with project and personnel Gantt views.
- **Team collaboration**: Create teams, invite members, and manage repositories / project libraries so every task has clear ownership.
- **RBAC access control**: Give the right access to the right team or person for safer collaboration.
- **State control and collaborative workflows**: Keep status changes synchronized across collaborative workflows.
- **PWA notifications**: Notify assignees through app notifications and reduce manual follow-up.
- **Activity history**: Review recent workspace task changes and operation records.
- **Hotkey shortcuts**: Speed up task editing in lists, Markdown editors, dropdowns, and dialogs.
- **Multi-language interface**: Switch the interface language based on user preference.

## Download Acrool App

Download the latest Acrool Desktop App from [Releases](https://github.com/acrool/acrool/releases).

After installing on macOS, if you see a warning that the app is damaged or cannot be opened, run:

```bash
xattr -cr /Applications/Acrool.app
```

Reference: [Fix macOS Ventura 13 damaged app warning](https://medium.com/@imaginechiu/%E8%A7%A3%E6%B1%BAmacos-ventura-13-%E6%AA%94%E6%A1%88%E5%B7%B2%E6%90%8D%E6%AF%80%E7%84%A1%E6%B3%95%E6%89%93%E9%96%8B%E6%8A%80%E5%B7%A7%E6%96%B9%E6%B3%95-2aa4f28e181e)

## MCP Connection

Acrool provides an MCP (Model Context Protocol) connection so AI assistants such as Claude Desktop, Claude Code (CLI), and OpenAI Codex CLI can read and update your tasks directly inside a conversation.

For full setup steps, see: [Connect Acrool to Claude / AI (MCP)](connect-claude-mcp.en.md).

## Report Issues

If you encounter a bug while using the Acrool App, please open an [Issue](https://github.com/acrool/acrool/issues) and include:

- Operating system and version
- Acrool App version
- Steps to reproduce
- Expected result and actual result
- Screenshots, screen recordings, or error messages

## Links

- Website: [acrool.com](https://acrool.com/)
- Documentation: [docs.acrool.com](https://docs.acrool.com/)
- Changelog: [docs.acrool.com/changelog](https://docs.acrool.com/changelog)
