# AI Assistant Guidelines for AI-Native PM Framework

**⚠️ IMPORTANT: Keep Synchronized**
This file must be kept in sync with `.cursorrules` and `CLAUDE.md`. If you update one, update all three to maintain consistency across different AI coding assistants.

## General Principles
- Challenge assumptions, don't just agree with proposals
- Think critically about user needs and evidence
- Help identify blog post opportunities from framework development
- Maintain healthy skepticism and propose alternatives
- Focus on solving real problems, not building solutions in search of problems

## Agent Routing
When working on specific tasks, read the relevant agents.md file first:

- **Blog writing**: Read agents.md in dev/blog-drafts/
- **Customer insights**: Read agents.md in customer-insights/
- **PRD generation**: Read agents.md in prds/ (when created)
- **Decision logs**: Read agents.md in decision-logs/ (when created)

## Project Context
This is a staging platform for Product Managers to transition from fragmented AI chat interactions to structured, knowledge-driven workflows using AI coding assistants like Google Code, Cursor, or Claude Code.

**Target Audience**: PMs currently using ChatGPT/Claude like a "calculator" (ask → answer → move on)
**Goal**: 80% of enterprise framework benefits with 20% of the complexity
**End State**: Clear progression path to advanced frameworks

## Critical Thinking Requirements
- Is this actually solving a real problem?
- What's the evidence vs assumptions?
- What could go wrong?
- Is this the simplest solution?
- Who is this really for?

## Blog Strategy
Each framework development decision becomes blog content:
1. "Why chatbots aren't enough" → Problem identification
2. "Beginner's guide" → Solution implementation
3. "Avoiding pitfalls" → Wisdom sharing
4. "Personal journey" → Thought leadership
5. "Advanced concepts" → Community building

## File Structure Standards
- **README.md**: Technical documentation
- **howto-*.md**: Step-by-step guides for junior PMs
- **prompt-*.md**: AI processing instructions
- **agents.md**: AI agent guidance for specific modules

## Working Style
- Use appropriate task tracking tools to manage progress on complex tasks
- Read existing files before making changes
- Follow the established tone and voice patterns in blog content
- Maintain consistency with existing code conventions and patterns
- Focus on practical, actionable solutions over theoretical frameworks

## Configuration File Synchronization
**CRITICAL**: When modifying this file, also update:
- `.cursorrules` (for Cursor users)
- `CLAUDE.md` (for Claude Code users)
- `AI_GUIDELINES.md` (for Google Code and other AI assistants)

All three files should contain identical guidance to ensure consistent AI behavior across the team.