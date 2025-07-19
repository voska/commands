# Claude Code Slash Commands

A collection of production-ready slash commands for Claude Code to accelerate software development workflows. Enhanced with framework-specific implementations, cross-command integration, and modern tooling support.

## Installation

Clone this repository to your local `.claude` directory for easy access:

```bash
cd ~/.claude
git clone https://github.com/wshobson/commands.git
```

This will make all slash commands available to Claude Code in any project.

## Overview

These commands provide instant access to comprehensive scaffolding, analysis, and optimization tools. Each command accepts context-specific arguments and generates production-ready code with best practices built-in.

### Key Features
- **Framework-Specific Implementations**: Intelligent framework selection with complete implementations for FastAPI, Express.js, Django, Spring Boot, and more
- **Cross-Command Integration**: Commands work together seamlessly - API scaffolds integrate with testing, security scanning feeds into deployment, and all commands share configuration
- **Modern Tooling**: Support for latest tools including Bun, UV, Ruff, BuildKit, Trivy, and cloud-native technologies
- **Production-Ready**: Complete implementations with no TODOs or placeholders

## Available Commands

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

**Total: 41 production-ready slash commands** organized into 8 categories:
- AI & Machine Learning (5 commands)
- Architecture & Code Quality (6 commands)
- Data & Database (4 commands)
- DevOps & Infrastructure (6 commands)
- Development & Testing (4 commands)
- Security & Compliance (3 commands)
- Debugging & Analysis (4 commands)
- Dependencies & Configuration (3 commands)
- Documentation & Collaboration (4 commands)
- Cost Optimization (1 command)

## Usage Examples

```bash
# Create a user management API
/api-scaffold user CRUD operations with JWT auth and role-based access

# Review microservices architecture
/arch-review analyze our microservices for coupling and scalability issues

# Optimize LLM chat application
/prompt-optimize reduce latency for customer support chatbot while maintaining accuracy

# Create fraud detection pipeline
/ml-pipeline real-time fraud detection with feature store and model monitoring

# Modernize legacy Java application
/legacy-modernize migrate Spring Boot 2.x to 3.x with cloud-native patterns

# Debug production issue
/error-trace analyze high memory usage in production pods

# Secure container images
/security-scan scan and fix vulnerabilities in Docker images

# Generate API documentation
/doc-generate create OpenAPI docs with examples for REST endpoints
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

## Cross-Command Workflows

Commands are designed to work together. Example workflow:

```bash
# 1. Scaffold an API
/api-scaffold user authentication service with JWT

# 2. Add comprehensive tests
/test-harness test the authentication endpoints

# 3. Security scan
/security-scan analyze for vulnerabilities

# 4. Optimize container
/docker-optimize create production dockerfile

# 5. Deploy to Kubernetes
/k8s-manifest generate deployment with autoscaling

# 6. Setup monitoring
/performance-review add observability stack
```

## Best Practices

1. **Provide context** - Include relevant details about your tech stack, constraints, and requirements
2. **Use framework detection** - Commands automatically detect and optimize for your stack
3. **Leverage integration** - Commands share configuration and work together seamlessly
4. **Iterate** - Commands can be refined with follow-up requests
5. **Customize output** - Specify preferences for frameworks, patterns, or approaches

## Contributing

To add new commands:
1. Create a markdown file in the commands directory
2. Use the `$ARGUMENTS` placeholder for user input
3. Structure content with clear sections and actionable outputs
4. Include severity levels, examples, and best practices

## License

These commands are provided as development accelerators. Customize generated code to meet your specific requirements and security policies.