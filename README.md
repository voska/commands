# Claude Code Slash Commands

A collection of production-ready slash commands for Claude Code to accelerate software development workflows.

## Installation

Clone this repository to your local `.claude` directory for easy access:

```bash
cd ~/.claude
git clone https://github.com/wshobson/commands.git
```

This will make all slash commands available to Claude Code in any project.

## Overview

These commands provide instant access to comprehensive scaffolding, analysis, and optimization tools. Each command accepts context-specific arguments and generates production-ready code with best practices built-in.

## Available Commands

### Development & Scaffolding

#### `/api-scaffold`
Generate production-ready API endpoints with complete implementation stack.
- Route definitions with FastAPI/Flask/Express
- Request/response models with validation
- Service layers and database operations
- Authentication, rate limiting, and error handling
- Comprehensive test suites
- API documentation

**Usage:** `/api-scaffold [endpoint description or requirements]`

#### `/langchain-agent`
Create LangChain/LangGraph agents with modern patterns.
- Tool implementations and chain definitions
- Memory systems (conversation, entity, summary)
- RAG integration with vector stores
- Streaming and async support
- Observability with LangSmith
- Production deployment configs

**Usage:** `/langchain-agent [agent type and requirements]`

### Code Analysis & Review

#### `/arch-review`
Comprehensive architecture analysis and recommendations.
- SOLID principles compliance
- Scalability and performance patterns
- Security vulnerability assessment
- Technical debt identification
- Modernization roadmap
- Dependency analysis

**Usage:** `/arch-review [codebase or component path]`

#### `/ai-review`
Specialized review for AI/ML codebases.
- Model reproducibility and data leakage checks
- LLM security (prompt injection, token limits)
- Vector database optimization
- GPU/CPU resource utilization
- MLOps best practices
- Production readiness assessment

**Usage:** `/ai-review [AI/ML code or project]`

#### `/error-analysis`
Deep error pattern analysis and resolution strategies.
- Root cause analysis
- Error handling improvements
- Logging and monitoring enhancements
- Recovery mechanisms
- Prevention strategies
- Performance impact assessment

**Usage:** `/error-analysis [error logs or patterns]`

### Data Engineering

#### `/data-pipeline`
Design scalable data pipeline architectures.
- ETL/ELT workflows with Airflow/Prefect
- Streaming with Kafka/Kinesis
- Data quality and validation layers
- Storage strategies (data lake/warehouse)
- Monitoring and alerting
- Cost optimization

**Usage:** `/data-pipeline [data flow requirements]`

#### `/data-validation`
Implement comprehensive data validation systems.
- Schema validation with Pydantic/JSON Schema
- Statistical quality checks
- Custom business rule validation
- Data profiling and anomaly detection
- Performance optimization
- Integration with various data sources

**Usage:** `/data-validation [data types and validation rules]`

### Machine Learning

#### `/ml-pipeline`
Create end-to-end ML pipelines with MLOps.
- Feature engineering pipelines
- Model training and versioning
- Hyperparameter optimization
- A/B testing frameworks
- Model monitoring and drift detection
- Deployment strategies (batch/real-time)

**Usage:** `/ml-pipeline [ML project requirements]`

#### `/prompt-optimize`
Optimize AI prompts for performance and quality.
- Prompt engineering techniques
- Context window optimization
- Few-shot learning examples
- Chain-of-thought prompting
- Model-specific optimizations
- Cost and latency reduction

**Usage:** `/prompt-optimize [current prompt and goals]`

### DevOps & Testing

#### `/deploy-checklist`
Generate deployment configurations and checklists.
- Environment-specific configs
- CI/CD pipeline definitions
- Infrastructure as Code templates
- Security configurations
- Monitoring and alerting setup
- Rollback procedures

**Usage:** `/deploy-checklist [application type and environment]`

#### `/test-harness`
Create comprehensive test suites.
- Unit tests with mocking strategies
- Integration and E2E tests
- Performance and load tests
- Security test scenarios
- Test data generation
- CI/CD integration

**Usage:** `/test-harness [code to test or test requirements]`

#### `/performance-review`
Profile and optimize application performance.
- CPU and memory profiling
- Database query optimization
- Caching strategy implementation
- Async/concurrent optimizations
- Frontend performance improvements
- Monitoring dashboard setup

**Usage:** `/performance-review [application or component]`

## Command Features

All commands include:
- **Production-ready code** - No placeholders or TODOs
- **Security best practices** - Authentication, validation, sanitization
- **Monitoring & observability** - Metrics, logging, tracing
- **Comprehensive testing** - Unit, integration, performance tests
- **Documentation** - API docs, architecture diagrams, deployment guides
- **Performance optimization** - Caching, async patterns, resource efficiency
- **Error handling** - Graceful degradation, recovery strategies

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
```

## Best Practices

1. **Provide context** - Include relevant details about your tech stack, constraints, and requirements
2. **Iterate** - Commands can be refined with follow-up requests
3. **Combine commands** - Use multiple commands for comprehensive solutions
4. **Customize output** - Specify preferences for frameworks, patterns, or approaches

## Contributing

To add new commands:
1. Create a markdown file in the commands directory
2. Use the `$ARGUMENTS` placeholder for user input
3. Structure content with clear sections and actionable outputs
4. Include severity levels, examples, and best practices

## License

These commands are provided as development accelerators. Customize generated code to meet your specific requirements and security policies.