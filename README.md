# Claude Code Slash Commands

A collection of production-ready slash commands for Claude Code to accelerate software development workflows. Commands are organized into two categories: **workflows** (smart agent orchestration) and **tools** (single-purpose utilities).

## Installation

Clone this repository to your local `.claude` directory for easy access:

```bash
cd ~/.claude
git clone https://github.com/wshobson/commands.git
```

This will make all slash commands available to Claude Code in any project.

## Overview

These commands leverage Claude Code's specialized agent system to provide intelligent automation for complex development tasks. The collection is organized into:

- **🤖 Workflows** (`/workflows/`): Smart agent orchestration commands that coordinate multiple specialized subagents to complete complex, multi-step tasks
- **🔧 Tools** (`/tools/`): Single-purpose commands for specific development tasks with comprehensive implementations

### Key Features

- **Agent Orchestration**: Workflows intelligently delegate tasks to specialized agents (backend-architect, frontend-developer, security-auditor, etc.)
- **Framework-Specific Implementations**: Intelligent framework selection with complete implementations for FastAPI, Express.js, Django, Spring Boot, and more
- **Cross-Command Integration**: Commands work together seamlessly - API scaffolds integrate with testing, security scanning feeds into deployment
- **Production-Ready**: Complete implementations with no TODOs or placeholders

## 🤖 Workflows (Smart Agent Commands)

These commands use multiple specialized agents working together to complete complex tasks:

### Feature Development

- **`/feature-development`** - Orchestrates backend-architect, frontend-developer, test-automator, and deployment-engineer to implement complete features
- **`/full-review`** - Comprehensive review using code-reviewer, security-auditor, architect-reviewer, performance-engineer, and test-automator
- **`/smart-fix`** - Intelligently analyzes issues and delegates to the most appropriate specialist agents

### Development Processes

- **`/git-workflow`** - Implements effective Git workflows with branching strategies and PR templates
- **`/improve-agent`** - Enhances agent performance through prompt optimization and capability analysis
- **`/legacy-modernize`** - Systematically modernizes legacy codebases using specialized migration agents
- **`/ml-pipeline`** - Creates end-to-end ML pipelines with MLOps using data and ML engineering agents
- **`/multi-platform`** - Builds cross-platform applications coordinating mobile, web, and backend agents
- **`/workflow-automate`** - Automates development workflows across CI/CD, monitoring, and deployment

## 🔧 Tools (Single-Purpose Commands)

### AI & Machine Learning

#### `/ai-assistant`

Build production-ready AI assistants and chatbots.

- LLM integration (OpenAI, Anthropic, local models)
- Conversation management and memory
- Function calling and tool use
- Streaming responses
- Rate limiting and cost controls

#### `/ai-review`

Specialized review for AI/ML codebases.

- Model reproducibility and data leakage checks
- LLM security (prompt injection, token limits)
- Vector database optimization
- GPU/CPU resource utilization
- MLOps best practices

#### `/langchain-agent`

Create LangChain/LangGraph agents with modern patterns.

- Tool implementations and chain definitions
- Memory systems (conversation, entity, summary)
- RAG integration with vector stores
- Streaming and async support
- Observability with LangSmith

#### `/ml-pipeline`

Create end-to-end ML pipelines with MLOps.

- Feature engineering pipelines
- Model training and versioning
- Hyperparameter optimization
- A/B testing frameworks
- Model monitoring and drift detection

#### `/prompt-optimize`

Optimize AI prompts for performance and quality.

- Prompt engineering techniques
- Context window optimization
- Few-shot learning examples
- Chain-of-thought prompting
- Cost and latency reduction

### Architecture & Code Quality

#### `/arch-review`

Comprehensive architecture analysis and recommendations.

- SOLID principles compliance
- Scalability and performance patterns
- Security vulnerability assessment
- Technical debt identification
- Modernization roadmap

#### `/code-explain`

Generate detailed explanations of complex code.

- Function and class documentation
- Architecture diagrams
- Flow charts and sequence diagrams
- Complexity analysis
- Best practice recommendations

#### `/code-migrate`

Migrate code between languages, frameworks, or versions.

- Language translation (Python↔JS, Java↔C#)
- Framework migration (Express→Fastify, Django→FastAPI)
- Version upgrades with breaking changes
- Dependency updates
- Test migration

#### `/legacy-modernize`

Modernize legacy codebases systematically.

- Monolith to microservices migration
- Database modernization
- API versioning strategies
- Gradual migration plans
- Risk assessment

#### `/refactor-clean`

Refactor code for maintainability and performance.

- Design pattern implementation
- Code smell elimination
- Performance optimizations
- Complexity reduction
- Test coverage improvement

#### `/tech-debt`

Analyze and prioritize technical debt.

- Debt quantification metrics
- Impact analysis
- Remediation roadmap
- Cost/benefit analysis
- Quick wins identification

### Data & Database

#### `/data-pipeline`

Design scalable data pipeline architectures.

- ETL/ELT workflows with Airflow/Prefect
- Streaming with Kafka/Kinesis
- Data quality and validation layers
- Storage strategies (data lake/warehouse)
- Monitoring and alerting

#### `/data-validation`

Implement comprehensive data validation systems.

- Schema validation with Pydantic/JSON Schema
- Statistical quality checks
- Custom business rule validation
- Data profiling and anomaly detection
- Performance optimization

#### `/db-migrate`

Advanced database migration strategies.

- **Multi-Database**: PostgreSQL, MySQL, MongoDB, DynamoDB
- **Zero-Downtime**: Blue-green deployments, rolling migrations
- **Event Sourcing**: Kafka/Kinesis integration for CDC
- **Cross-Platform**: Handles polyglot persistence
- **Cross-Command Integration**: API-aware migrations

#### `/db-optimize`

Optimize database performance and queries.

- Query performance analysis
- Index optimization
- Connection pooling
- Caching strategies
- Partitioning and sharding

### DevOps & Infrastructure

#### `/deploy-checklist`

Generate deployment configurations and checklists.

- Environment-specific configs
- CI/CD pipeline definitions
- Infrastructure as Code templates
- Security configurations
- Rollback procedures

#### `/docker-optimize`

Advanced container optimization strategies.

- **Smart Optimization**: Analyzes and suggests improvements
- **Multi-Stage Builds**: Framework-specific optimized Dockerfiles
- **Modern Tools**: BuildKit, Bun, UV for faster builds
- **Security Hardening**: Distroless images, non-root users
- **Cross-Command Integration**: Works with /api-scaffold outputs

#### `/k8s-manifest`

Production-grade Kubernetes deployments.

- **Advanced Patterns**: Pod Security Standards, Network Policies, OPA
- **GitOps Ready**: FluxCD and ArgoCD configurations
- **Observability**: Prometheus ServiceMonitors, OpenTelemetry
- **Auto-Scaling**: HPA, VPA, and cluster autoscaler configs
- **Service Mesh**: Istio/Linkerd integration

#### `/monitor-setup`

Set up comprehensive monitoring and observability.

- Prometheus and Grafana dashboards
- OpenTelemetry instrumentation
- Log aggregation (ELK/Loki)
- Alerting rules and runbooks
- SLI/SLO definitions

#### `/slo-implement`

Implement Service Level Objectives (SLOs).

- SLI identification and measurement
- Error budget tracking
- Alerting based on burn rates
- SLO dashboards
- Reliability reporting

#### `/workflow-automate`

Automate development and operational workflows.

- GitHub Actions workflows
- GitLab CI pipelines
- Jenkins pipelines
- Terraform automation
- Release automation

### Development & Testing

#### `/api-mock`

Create realistic API mocks for development and testing.

- OpenAPI-based mock generation
- Dynamic response generation
- Stateful mocks
- Performance simulation
- Error scenario testing

#### `/api-scaffold`

Generate production-ready API endpoints with complete implementation stack.

- **Framework Selection**: Intelligent choice between FastAPI, Django REST, Express.js, Spring Boot
- **Complete Stack**: Routes, models, schemas, services, repositories, middleware
- **Security Built-in**: JWT auth, bcrypt hashing, rate limiting, CORS
- **Database Integration**: SQLAlchemy, Prisma, Django ORM with migrations
- **Cross-Command Integration**: Works with /test-harness, /security-scan, /docker-optimize

#### `/test-harness`

Create comprehensive test suites with framework detection.

- **Framework Detection**: Automatically selects pytest, Jest, Vitest
- **Test Types**: Unit, integration, E2E, performance (Locust), security
- **Modern Patterns**: Fixtures, mocks, factories, parallel execution
- **CI/CD Ready**: GitHub Actions and GitLab CI workflows included
- **Cross-Command Integration**: Tests APIs, containers, and more

#### `/frontend-optimize`

Modern frontend performance optimization.

- **Framework Detection**: React, Vue, Angular, Svelte optimizations
- **Bundle Analysis**: Webpack, Vite, Turbopack configurations
- **Performance Monitoring**: Core Web Vitals, Lighthouse CI
- **Modern Patterns**: Code splitting, lazy loading, prefetching
- **Cross-Command Integration**: API integration, deployment pipelines

### Security & Compliance

#### `/accessibility-audit`

Comprehensive accessibility testing and fixes.

- WCAG 2.1 compliance checking
- Automated testing setup
- Screen reader optimization
- Keyboard navigation
- ARIA implementation

#### `/compliance-check`

Ensure regulatory compliance (GDPR, HIPAA, SOC2).

- Data privacy audits
- Security control verification
- Compliance documentation
- Automated compliance tests
- Remediation guidance

#### `/security-scan`

Comprehensive security scanning with automated remediation.

- **Multi-Tool Scanning**: Bandit, Safety, Trivy, Semgrep, ESLint Security
- **Automated Fixes**: Common vulnerabilities auto-remediated
- **CI/CD Integration**: Security gates for GitHub Actions/GitLab CI
- **Container Scanning**: Image vulnerability analysis
- **Cross-Command Integration**: Secures APIs, containers, deployments

### Debugging & Analysis

#### `/debug-trace`

Advanced debugging and tracing strategies.

- Distributed tracing setup
- Debug symbol management
- Remote debugging configuration
- Performance profiling
- Memory leak detection

#### `/error-analysis`

Deep error pattern analysis and resolution strategies.

- Root cause analysis
- Error handling improvements
- Logging and monitoring enhancements
- Recovery mechanisms
- Prevention strategies

#### `/error-trace`

Trace and diagnose production errors.

- Stack trace analysis
- Error correlation
- User impact assessment
- Reproduction steps
- Fix verification

#### `/performance-review`

Profile and optimize application performance.

- CPU and memory profiling
- Database query optimization
- Caching strategy implementation
- Async/concurrent optimizations
- Frontend performance improvements

### Dependencies & Configuration

#### `/config-validate`

Validate and manage application configuration.

- Schema validation
- Environment variable management
- Secret handling
- Configuration drift detection
- Multi-environment configs

#### `/deps-audit`

Audit dependencies for security and licensing.

- Vulnerability scanning
- License compliance
- Outdated package detection
- Dependency graph analysis
- Risk assessment

#### `/deps-upgrade`

Safely upgrade project dependencies.

- Breaking change analysis
- Compatibility testing
- Gradual upgrade strategies
- Rollback plans
- Automated testing

### Documentation & Collaboration

#### `/doc-generate`

Generate comprehensive documentation.

- API documentation
- Architecture diagrams
- Setup guides
- Runbooks
- Code examples

#### `/git-workflow`

Implement effective Git workflows.

- Branching strategies
- Commit conventions
- PR templates
- Merge strategies
- Release workflows

#### `/issue`

Create well-structured GitHub/GitLab issues.

- Bug report templates
- Feature request templates
- Task breakdowns
- Acceptance criteria
- Labels and milestones

#### `/pr-enhance`

Enhance pull requests with quality checks.

- PR templates
- Automated checks
- Review checklists
- Change impact analysis
- Documentation updates

### Cost Optimization

#### `/cost-optimize`

Optimize cloud and infrastructure costs.

- Resource utilization analysis
- Right-sizing recommendations
- Reserved instance planning
- Spot instance strategies
- Cost allocation and tagging

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

#### `/security-scan`

Comprehensive security scanning with automated remediation.

- **Multi-Tool Scanning**: Bandit, Safety, Trivy, Semgrep, ESLint Security, Snyk
- **Automated Fixes**: Common vulnerabilities auto-remediated
- **CI/CD Integration**: Security gates for GitHub Actions/GitLab CI
- **Container Scanning**: Image vulnerability analysis
- **Secret Detection**: GitLeaks and TruffleHog integration

#### `/docker-optimize`

Advanced container optimization strategies.

- **Smart Optimization**: Analyzes and suggests improvements
- **Multi-Stage Builds**: Framework-specific optimized Dockerfiles
- **Modern Tools**: BuildKit, Bun, UV for faster builds
- **Security Hardening**: Distroless images, non-root users
- **Cross-Command Integration**: Works with /api-scaffold outputs

#### `/k8s-manifest`

Production-grade Kubernetes deployments.

- **Advanced Patterns**: Pod Security Standards, Network Policies, OPA
- **GitOps Ready**: FluxCD and ArgoCD configurations
- **Observability**: Prometheus ServiceMonitors, OpenTelemetry
- **Auto-Scaling**: HPA, VPA, and cluster autoscaler configs
- **Service Mesh**: Istio/Linkerd integration

### Frontend & Data

#### `/frontend-optimize`

Modern frontend performance optimization.

- **Framework Detection**: React, Vue, Angular, Svelte optimizations
- **Bundle Analysis**: Webpack, Vite, Turbopack configurations
- **Performance Monitoring**: Core Web Vitals, Lighthouse CI
- **Modern Patterns**: Code splitting, lazy loading, prefetching
- **CDN & Caching**: Cloudflare, Fastly configurations

#### `/db-migrate`

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

## When to Use Workflows vs Tools

### Use Workflows When:

- You need multiple specialized agents working together
- The task requires coordination across different domains
- You want intelligent task delegation and orchestration
- The problem is complex and benefits from diverse expertise
- You need end-to-end implementation of a feature

### Use Tools When:

- You have a specific, well-defined task
- You need deep expertise in a single domain
- You want direct control over the implementation
- The task is part of a larger manual workflow
- You need to customize or iterate on specific aspects

## Best Practices

1. **Start with workflows** for complex tasks - Let agents coordinate the implementation
2. **Use tools for refinement** - Apply specific tools to enhance workflow outputs
3. **Provide context** - Include tech stack, constraints, and requirements
4. **Leverage agent expertise** - Trust specialized agents with their domains
5. **Combine approaches** - Use workflows for implementation, tools for optimization

## Contributing

### Adding a New Workflow:

1. Create a markdown file in the `workflows/` directory
2. Define the agent orchestration sequence
3. Specify which specialized agents to use and in what order
4. Use the `$ARGUMENTS` placeholder for user input
5. Focus on coordination and delegation logic

### Adding a New Tool:

1. Create a markdown file in the `tools/` directory
2. Include comprehensive implementation details
3. Use the `$ARGUMENTS` placeholder for user input
4. Structure content with clear sections and actionable outputs
5. Include examples, best practices, and integration points

## License

These commands are provided as development accelerators. Customize generated code to meet your specific requirements and security policies.
