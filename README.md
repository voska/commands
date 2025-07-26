# Claude Code Slash Commands Collection

A comprehensive collection of production-ready slash commands for [Claude Code](https://docs.anthropic.com/en/docs/claude-code), designed to accelerate software development workflows through intelligent automation and agent orchestration.

## Overview

This repository contains 45 specialized slash commands that extend Claude Code's capabilities. Commands are organized into **workflows** (smart agent orchestration) and **tools** (single-purpose utilities) to provide comprehensive development automation.

## Installation

These commands are automatically available when placed in `~/.claude/commands/` directory.

```bash
cd ~/.claude
git clone https://github.com/wshobson/commands.git
```

## Available Commands

The collection is organized into:

- **🤖 Workflows** (`/workflows/`): Smart agent orchestration commands that coordinate multiple specialized subagents to complete complex, multi-step tasks
- **🔧 Tools** (`/tools/`): Single-purpose commands for specific development tasks with comprehensive implementations

## Usage

### Automatic Invocation
Claude Code will automatically suggest appropriate commands based on the task context and requirements.

### Explicit Invocation
Run any command directly by typing the command name:
```
/api-scaffold user management with authentication
/security-scan check for vulnerabilities in Docker images
/feature-development implement real-time chat functionality
```

### Key Features

- **Agent Orchestration**: Workflows intelligently delegate tasks to specialized agents (backend-architect, frontend-developer, security-auditor, etc.)
- **Framework-Specific Implementations**: Intelligent framework selection with complete implementations for FastAPI, Express.js, Django, Spring Boot, and more
- **Cross-Command Integration**: Commands work together seamlessly - API scaffolds integrate with testing, security scanning feeds into deployment
- **Production-Ready**: Complete implementations with no TODOs or placeholders

## 🤖 Workflows (Smart Agent Commands)

These commands use multiple specialized agents working together to complete complex tasks:

### Feature Development
- **[feature-development](workflows/feature-development.md)** - Orchestrates backend-architect, frontend-developer, test-automator, and deployment-engineer to implement complete features
- **[full-review](workflows/full-review.md)** - Comprehensive review using code-reviewer, security-auditor, architect-reviewer, performance-engineer, and test-automator
- **[smart-fix](workflows/smart-fix.md)** - Intelligently analyzes issues and delegates to the most appropriate specialist agents

### Development Processes
- **[git-workflow](workflows/git-workflow.md)** - Implements effective Git workflows with branching strategies and PR templates
- **[improve-agent](workflows/improve-agent.md)** - Enhances agent performance through prompt optimization and capability analysis
- **[legacy-modernize](workflows/legacy-modernize.md)** - Systematically modernizes legacy codebases using specialized migration agents
- **[ml-pipeline](workflows/ml-pipeline.md)** - Creates end-to-end ML pipelines with MLOps using data and ML engineering agents
- **[multi-platform](workflows/multi-platform.md)** - Builds cross-platform applications coordinating mobile, web, and backend agents
- **[workflow-automate](workflows/workflow-automate.md)** - Automates development workflows across CI/CD, monitoring, and deployment

## 🔧 Tools (Single-Purpose Commands)

### AI & Machine Learning
- **[ai-assistant](tools/ai-assistant.md)** - Build production-ready AI assistants and chatbots
- **[ai-review](tools/ai-review.md)** - Specialized review for AI/ML codebases
- **[langchain-agent](tools/langchain-agent.md)** - Create LangChain/LangGraph agents with modern patterns
- **[ml-pipeline](tools/ml-pipeline.md)** - Create end-to-end ML pipelines with MLOps
- **[prompt-optimize](tools/prompt-optimize.md)** - Optimize AI prompts for performance and quality

### Architecture & Code Quality
- **[arch-review](tools/arch-review.md)** - Comprehensive architecture analysis and recommendations
- **[code-explain](tools/code-explain.md)** - Generate detailed explanations of complex code
- **[code-migrate](tools/code-migrate.md)** - Migrate code between languages, frameworks, or versions
- **[legacy-modernize](tools/legacy-modernize.md)** - Modernize legacy codebases systematically
- **[refactor-clean](tools/refactor-clean.md)** - Refactor code for maintainability and performance
- **[tech-debt](tools/tech-debt.md)** - Analyze and prioritize technical debt

### Data & Database
- **[data-pipeline](tools/data-pipeline.md)** - Design scalable data pipeline architectures
- **[data-validation](tools/data-validation.md)** - Implement comprehensive data validation systems
- **[db-migrate](tools/db-migrate.md)** - Advanced database migration strategies
- **[db-optimize](tools/db-optimize.md)** - Optimize database performance and queries

### DevOps & Infrastructure
- **[deploy-checklist](tools/deploy-checklist.md)** - Generate deployment configurations and checklists
- **[docker-optimize](tools/docker-optimize.md)** - Advanced container optimization strategies
- **[k8s-manifest](tools/k8s-manifest.md)** - Production-grade Kubernetes deployments
- **[monitor-setup](tools/monitor-setup.md)** - Set up comprehensive monitoring and observability
- **[slo-implement](tools/slo-implement.md)** - Implement Service Level Objectives (SLOs)
- **[workflow-automate](tools/workflow-automate.md)** - Automate development and operational workflows

### Development & Testing
- **[api-mock](tools/api-mock.md)** - Create realistic API mocks for development and testing
- **[api-scaffold](tools/api-scaffold.md)** - Generate production-ready API endpoints with complete implementation stack
- **[test-harness](tools/test-harness.md)** - Create comprehensive test suites with framework detection
- **[frontend-optimize](tools/frontend-optimize.md)** - Modern frontend performance optimization

### Security & Compliance
- **[accessibility-audit](tools/accessibility-audit.md)** - Comprehensive accessibility testing and fixes
- **[compliance-check](tools/compliance-check.md)** - Ensure regulatory compliance (GDPR, HIPAA, SOC2)
- **[security-scan](tools/security-scan.md)** - Comprehensive security scanning with automated remediation

### Debugging & Analysis
- **[debug-trace](tools/debug-trace.md)** - Advanced debugging and tracing strategies
- **[error-analysis](tools/error-analysis.md)** - Deep error pattern analysis and resolution strategies
- **[error-trace](tools/error-trace.md)** - Trace and diagnose production errors
- **[performance-review](tools/performance-review.md)** - Profile and optimize application performance

### Dependencies & Configuration
- **[config-validate](tools/config-validate.md)** - Validate and manage application configuration
- **[deps-audit](tools/deps-audit.md)** - Audit dependencies for security and licensing
- **[deps-upgrade](tools/deps-upgrade.md)** - Safely upgrade project dependencies

### Documentation & Collaboration
- **[doc-generate](tools/doc-generate.md)** - Generate comprehensive documentation
- **[git-workflow](tools/git-workflow.md)** - Implement effective Git workflows
- **[issue](tools/issue.md)** - Create well-structured GitHub/GitLab issues
- **[pr-enhance](tools/pr-enhance.md)** - Enhance pull requests with quality checks

### Cost Optimization
- **[cost-optimize](tools/cost-optimize.md)** - Optimize cloud and infrastructure costs

### Onboarding & Setup
- **[onboard](tools/onboard.md)** - Set up development environments for new team members

## Command Features

All commands include:

- **Production-ready code** - Complete implementations with no placeholders or TODOs
- **Framework Intelligence** - Automatic detection and optimization for your tech stack
- **Security best practices** - Authentication, validation, sanitization, vulnerability scanning
- **Monitoring & observability** - Prometheus metrics, OpenTelemetry tracing, structured logging
- **Comprehensive testing** - Unit, integration, performance tests with modern frameworks
- **Documentation** - API docs, architecture diagrams, deployment guides, runbooks
- **Performance optimization** - Caching, async patterns, resource efficiency, CDN integration
- **Error handling** - Graceful degradation, circuit breakers, recovery strategies
- **Cross-Command Workflows** - Commands integrate seamlessly for complete development workflows

## Command Count

**Total: 45 production-ready slash commands** organized into:

### 🤖 Workflows (9 commands)

- Feature Development & Review (3 commands)
- Development Process Automation (6 commands)

### 🔧 Tools (36 commands)

- AI & Machine Learning (5 commands)
- Architecture & Code Quality (6 commands)
- Data & Database (4 commands)
- DevOps & Infrastructure (6 commands)
- Development & Testing (4 commands)
- Security & Compliance (3 commands)
- Debugging & Analysis (4 commands)
- Dependencies & Configuration (3 commands)
- Documentation & Collaboration (1 command)
- Onboarding & Setup (1 command)

## Usage Examples

### 🤖 Workflow Examples (Multi-Agent Orchestration)

```bash
# Implement a complete feature with multiple agents
/feature-development Add user authentication with OAuth2, profile management, and email verification

# Perform comprehensive code review with specialist agents
/full-review Review the authentication module for security, performance, and architecture

# Smart issue resolution with automatic agent selection
/smart-fix Fix performance degradation in API response times

# Modernize legacy system with coordinated agents
/legacy-modernize Migrate monolithic Java app to microservices architecture
```

### 🔧 Tool Examples (Single-Purpose Commands)

```bash
# Create a user management API
/api-scaffold user CRUD operations with JWT auth and role-based access

# Review microservices architecture
/arch-review analyze our microservices for coupling and scalability issues

# Optimize LLM chat application
/prompt-optimize reduce latency for customer support chatbot while maintaining accuracy

# Create fraud detection pipeline
/data-pipeline real-time fraud detection with feature store and monitoring

# Debug production issue
/error-trace analyze high memory usage in production pods

# Secure container images
/security-scan scan and fix vulnerabilities in Docker images

# Generate API documentation
/doc-generate create OpenAPI docs with examples for REST endpoints

# Onboard new developer
/onboard Setup development environment for React/Node.js project
```

## Enhanced Commands

### Security & DevOps

#### [`/security-scan`](tools/security-scan.md)

Comprehensive security scanning with automated remediation.

- **Multi-Tool Scanning**: Bandit, Safety, Trivy, Semgrep, ESLint Security, Snyk
- **Automated Fixes**: Common vulnerabilities auto-remediated
- **CI/CD Integration**: Security gates for GitHub Actions/GitLab CI
- **Container Scanning**: Image vulnerability analysis
- **Secret Detection**: GitLeaks and TruffleHog integration

#### [`/docker-optimize`](tools/docker-optimize.md)

Advanced container optimization strategies.

- **Smart Optimization**: Analyzes and suggests improvements
- **Multi-Stage Builds**: Framework-specific optimized Dockerfiles
- **Modern Tools**: BuildKit, Bun, UV for faster builds
- **Security Hardening**: Distroless images, non-root users
- **Cross-Command Integration**: Works with /api-scaffold outputs

#### [`/k8s-manifest`](tools/k8s-manifest.md)

Production-grade Kubernetes deployments.

- **Advanced Patterns**: Pod Security Standards, Network Policies, OPA
- **GitOps Ready**: FluxCD and ArgoCD configurations
- **Observability**: Prometheus ServiceMonitors, OpenTelemetry
- **Auto-Scaling**: HPA, VPA, and cluster autoscaler configs
- **Service Mesh**: Istio/Linkerd integration

### Frontend & Data

#### [`/frontend-optimize`](tools/frontend-optimize.md)

Modern frontend performance optimization.

- **Framework Detection**: React, Vue, Angular, Svelte optimizations
- **Bundle Analysis**: Webpack, Vite, Turbopack configurations
- **Performance Monitoring**: Core Web Vitals, Lighthouse CI
- **Modern Patterns**: Code splitting, lazy loading, prefetching
- **CDN & Caching**: Cloudflare, Fastly configurations

#### [`/db-migrate`](tools/db-migrate.md)

Advanced database migration strategies.

- **Multi-Database**: PostgreSQL, MySQL, MongoDB, DynamoDB
- **Zero-Downtime**: Blue-green deployments, rolling migrations
- **Event Sourcing**: Kafka/Kinesis integration for CDC
- **Cross-Platform**: Handles polyglot persistence
- **Monitoring**: Migration health checks and rollback

## Combining Workflows and Tools

The real power comes from combining workflows and tools for complete development cycles:

### Example: Building a New Feature

```bash
# 1. Use a workflow to implement the feature with multiple agents
/feature-development Add real-time chat feature with WebSocket support

# 2. Use tools for specific enhancements
/test-harness Add integration tests for WebSocket connections
/security-scan Check for WebSocket vulnerabilities
/docker-optimize Optimize container for WebSocket connections

# 3. Use a workflow for comprehensive review
/full-review Review the entire chat feature implementation
```

### Example: Modernizing Legacy Code

```bash
# 1. Start with the modernization workflow
/legacy-modernize Migrate Express.js v4 app to modern architecture

# 2. Use specific tools for cleanup
/deps-upgrade Update all dependencies to latest versions
/refactor-clean Remove deprecated patterns and dead code
/test-harness Ensure 100% test coverage

# 3. Optimize and deploy
/docker-optimize Create multi-stage production build
/k8s-manifest Deploy with zero-downtime strategy
```

## Command Orchestration Patterns

Commands can be used individually or combined in powerful patterns:

### Sequential Execution
```bash
# Build → Test → Secure → Deploy pipeline
/api-scaffold user management API
/test-harness comprehensive test suite for user API  
/security-scan check user API for vulnerabilities
/k8s-manifest deploy user API to production
```

### Parallel Analysis
```bash
# Multiple perspectives on the same codebase
/arch-review analyze system architecture
/security-scan audit security posture  
/performance-review identify bottlenecks
# Then consolidate findings
```

### Iterative Refinement
```bash
# Start broad, then narrow focus
/feature-development implement payment processing
/security-scan focus on payment security
/compliance-check ensure PCI compliance
/test-harness add payment-specific tests
```

### Cross-Domain Integration
```bash
# Frontend + Backend + Infrastructure
/api-scaffold backend payment API
/frontend-optimize payment UI components
/docker-optimize containerize payment service
/monitor-setup payment metrics and alerts
```

## When to Use Workflows vs Tools

### 🤖 Use Workflows When:
- **Multi-domain coordination needed** - Feature touches backend, frontend, and infrastructure
- **Complex agent orchestration required** - Need multiple specialists working together
- **End-to-end implementation desired** - Want complete feature from design to deployment
- **Uncertain about approach** - Let agents determine best implementation strategy
- **Time constraints** - Need rapid, comprehensive implementation

**Examples:**
- "Implement user authentication system" → `/feature-development`
- "Fix performance issues across the stack" → `/smart-fix`
- "Modernize legacy monolith" → `/legacy-modernize`

### 🔧 Use Tools When:
- **Specific expertise needed** - Clear, focused task in one domain
- **Precise control desired** - Want to direct specific implementation details
- **Part of manual workflow** - Integrating into existing processes
- **Deep specialization required** - Need expert-level implementation
- **Building on existing work** - Enhancing or refining previous outputs

**Examples:**
- "Create Kubernetes manifests" → `/k8s-manifest`
- "Scan for security vulnerabilities" → `/security-scan`
- "Generate API documentation" → `/doc-generate`

## Command Format

Each command follows this structure:
```markdown
---
name: command-name
description: Brief description of what the command does
---

Detailed command implementation with:
- Framework detection and intelligent selection
- Complete, production-ready code
- Security best practices
- Cross-command integration points
```

## Best Practices

### 🎯 Command Selection
1. **Let Claude Code suggest automatically** - The main agent analyzes context and selects optimal commands
2. **Start with workflows for complex tasks** - Let agents coordinate multi-domain implementations
3. **Use tools for focused expertise** - Apply specific commands for targeted improvements
4. **Consider command dependencies** - Some tools work better after specific workflows

### 📝 Request Optimization  
5. **Provide comprehensive context** - Include tech stack, constraints, existing patterns, and quality requirements
6. **Be specific about integration points** - Mention how outputs should connect to existing systems
7. **Specify success criteria** - Define what "done" looks like for your use case
8. **Include examples when helpful** - Show desired output format or similar implementations

### 🔄 Workflow Management
9. **Combine commands strategically** - Chain related commands for complete solutions
10. **Use iterative refinement** - Start broad with workflows, then narrow with tools
11. **Leverage cross-command integration** - Commands are designed to work together seamlessly
12. **Monitor progress and provide feedback** - Guide agents with clarifications and corrections

### ⚡ Performance Optimization
13. **Batch related operations** - Combine similar commands to reduce context switching
14. **Reuse command outputs** - Build on previous results rather than starting fresh
15. **Choose appropriate command scope** - Match complexity to command capabilities

## Contributing

To add a new command:
1. Create a new `.md` file in the appropriate directory (`workflows/` or `tools/`)
2. Use lowercase, hyphen-separated names
3. Follow the command format structure above
4. Include comprehensive implementation details
5. Write clear descriptions for when the command should be used
6. Use the `$ARGUMENTS` placeholder for user input

## Troubleshooting

### Common Issues

**Command not found or not working:**
- Ensure commands are in `~/.claude/commands/` directory
- Check command file syntax and format
- Verify the command name matches the file name

**Unexpected output or behavior:**
- Provide more context about your project and tech stack
- Be specific about requirements and constraints
- Try breaking complex requests into smaller commands

**Workflow commands taking too long:**
- This is normal - workflows coordinate multiple agents
- Consider using specific tools for faster, focused results
- Monitor progress and provide feedback to guide agents

**Tools producing generic outputs:**
- Include framework/language-specific details in your request
- Mention existing patterns or preferences in your codebase
- Provide examples of desired output format

**Cross-command integration issues:**
- Check that file paths and naming conventions align
- Ensure commands are run in the correct sequence
- Verify that dependencies between commands are met

### Getting Help

If commands aren't working as expected:
1. Check individual command documentation for specific requirements
2. Try simpler, more focused requests first
3. Provide more context about your project structure and goals
4. Use explicit tool invocation to test specific functionality

## Performance Optimization

### 🎯 Efficient Usage Patterns

**Command Selection Strategy:**
- **Workflows**: Multi-agent coordination, end-to-end implementation
- **Tools**: Focused, single-domain tasks
- **Simple requests**: Stay with main agent for basic operations

**Optimization Strategies:**
1. **Start simple**: Try tools before workflows for known problems
2. **Batch operations**: Combine multiple related requests
3. **Reuse context**: Build on previous command outputs
4. **Early termination**: Stop and adjust if commands aren't producing expected results

### ⚡ Performance Tips

**Faster Command Execution:**
- Use specific tools for focused tasks rather than broad workflows
- Provide clear, detailed requirements upfront to avoid iterations
- Reference existing code patterns and preferences
- Choose commands that match your exact use case

**Efficient Workflows:**
- Let workflows complete before requesting modifications
- Provide comprehensive context in initial request
- Use cross-command integration rather than isolated commands
- Monitor agent progress and provide real-time feedback

### Adding a New Workflow:
- Focus on agent orchestration and delegation logic
- Specify which specialized agents to use and in what order
- Define coordination patterns between agents

### Adding a New Tool:
- Include complete, production-ready implementations
- Structure content with clear sections and actionable outputs
- Include examples, best practices, and integration points

## Learn More

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Slash Commands Documentation](https://docs.anthropic.com/en/docs/claude-code/slash-commands)
- [Subagents Documentation](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Claude Code GitHub](https://github.com/anthropics/claude-code)
