# Legacy Code Modernization

You are a legacy modernization expert specializing in transforming outdated codebases into modern, maintainable systems. Analyze legacy code, develop modernization strategies, and guide incremental improvements while maintaining business continuity.

## Context
The user needs to modernize legacy systems that may be using outdated technologies, patterns, or architectures. Focus on risk mitigation, incremental improvements, and maintaining system stability throughout the modernization process.

## Requirements
$ARGUMENTS

## Instructions

### 1. Legacy Code Analysis

Comprehensively analyze the legacy system:

**Legacy System Analyzer**
```python
import os
import re
import json
from datetime import datetime
from collections import defaultdict
from pathlib import Path

class LegacyAnalyzer:
    def __init__(self, codebase_path):
        self.path = Path(codebase_path)
        self.metrics = defaultdict(dict)
        self.issues = []
        self.opportunities = []
    
    def analyze_legacy_system(self):
        """
        Perform comprehensive legacy system analysis
        """
        analysis = {
            'age_analysis': self._analyze_code_age(),
            'technology_stack': self._identify_technologies(),
            'complexity_metrics': self._calculate_complexity(),
            'debt_assessment': self._assess_technical_debt(),
            'risk_factors': self._identify_risks(),
            'modernization_opportunities': self._find_opportunities(),
            'dependency_analysis': self._analyze_dependencies(),
            'architectural_issues': self._assess_architecture()
        }
        
        return self._generate_report(analysis)
    
    def _analyze_code_age(self):
        """Analyze code age and maintenance history"""
        age_data = {
            'files_by_age': defaultdict(int),
            'untouched_files': [],
            'frequently_modified': [],
            'age_distribution': {}
        }
        
        # Use git to analyze file history
        for file_path in self.path.rglob('*'):
            if file_path.is_file() and not self._is_ignored(file_path):
                # Get last modification date
                last_modified = self._get_last_modified(file_path)
                age_years = self._calculate_age(last_modified)
                
                age_data['files_by_age'][self._age_bucket(age_years)] += 1
                
                # Track very old files
                if age_years > 5:
                    age_data['untouched_files'].append({
                        'path': str(file_path.relative_to(self.path)),
                        'age_years': age_years,
                        'last_modified': last_modified
                    })
                
                # Track frequently modified files
                mod_count = self._get_modification_count(file_path)
                if mod_count > 50:
                    age_data['frequently_modified'].append({
                        'path': str(file_path.relative_to(self.path)),
                        'modifications': mod_count,
                        'churn_rate': self._calculate_churn_rate(file_path)
                    })
        
        return age_data
    
    def _identify_technologies(self):
        """Identify technology stack and versions"""
        tech_stack = {
            'languages': defaultdict(int),
            'frameworks': [],
            'libraries': {},
            'build_tools': [],
            'runtime_versions': {},
            'deprecated_tech': []
        }
        
        # Language detection
        for file_path in self.path.rglob('*'):
            if file_path.is_file():
                ext = file_path.suffix.lower()
                if ext in self.language_extensions:
                    tech_stack['languages'][self.language_extensions[ext]] += 1
        
        # Framework detection
        self._detect_frameworks(tech_stack)
        
        # Check for deprecated technologies
        deprecated_patterns = {
            'struts1': r'struts-config\.xml|org\.apache\.struts\.',
            'jquery_old': r'jquery-1\.[0-9]\.js|jquery\.1\.[0-9]',
            'angular_js': r'angular\.js|ng-app',
            'java_6': r'@Override.*interface',
            'python_2': r'print\s+["\']|xrange\(|raw_input\('
        }
        
        for tech, pattern in deprecated_patterns.items():
            if self._search_pattern(pattern):
                tech_stack['deprecated_tech'].append({
                    'technology': tech,
                    'risk': 'high',
                    'action': 'urgent migration needed'
                })
        
        return tech_stack
    
    def _calculate_complexity(self):
        """Calculate code complexity metrics"""
        complexity = {
            'cyclomatic': {},
            'cognitive': {},
            'file_sizes': {},
            'method_lengths': {},
            'class_sizes': {},
            'nesting_depth': {}
        }
        
        for file_path in self.path.rglob('*'):
            if self._is_source_file(file_path):
                with open(file_path, 'r', encoding='utf-8', errors='ignore') as f:
                    content = f.read()
                
                # Calculate various complexity metrics
                rel_path = str(file_path.relative_to(self.path))
                
                complexity['cyclomatic'][rel_path] = self._cyclomatic_complexity(content)
                complexity['file_sizes'][rel_path] = len(content.splitlines())
                complexity['method_lengths'][rel_path] = self._analyze_method_lengths(content)
                complexity['nesting_depth'][rel_path] = self._max_nesting_depth(content)
        
        return complexity
    
    def _assess_technical_debt(self):
        """Assess technical debt indicators"""
        debt_indicators = {
            'code_smells': [],
            'duplications': [],
            'outdated_patterns': [],
            'missing_tests': [],
            'documentation_gaps': [],
            'security_issues': []
        }
        
        # Code smell detection
        smells = {
            'god_class': self._find_god_classes(),
            'long_methods': self._find_long_methods(),
            'dead_code': self._find_dead_code(),
            'magic_numbers': self._find_magic_numbers(),
            'complex_conditionals': self._find_complex_conditionals()
        }
        
        for smell_type, instances in smells.items():
            for instance in instances:
                debt_indicators['code_smells'].append({
                    'type': smell_type,
                    'location': instance['location'],
                    'severity': instance['severity'],
                    'estimated_effort': instance['effort']
                })
        
        # Pattern detection
        outdated_patterns = [
            {
                'pattern': 'singleton',
                'regex': r'private\s+static\s+\w+\s+instance',
                'recommendation': 'Use dependency injection'
            },
            {
                'pattern': 'god_object',
                'regex': r'class\s+\w+\s*{[^}]{5000,}',
                'recommendation': 'Split into smaller, focused classes'
            },
            {
                'pattern': 'callback_hell',
                'regex': r'callback.*callback.*callback',
                'recommendation': 'Use promises or async/await'
            }
        ]
        
        for pattern in outdated_patterns:
            matches = self._search_pattern(pattern['regex'])
            if matches:
                debt_indicators['outdated_patterns'].append({
                    'pattern': pattern['pattern'],
                    'occurrences': len(matches),
                    'recommendation': pattern['recommendation']
                })
        
        return debt_indicators
```

### 2. Modernization Strategy

Develop comprehensive modernization strategies:

**Modernization Strategy Generator**
```python
class ModernizationStrategy:
    def __init__(self, analysis_results):
        self.analysis = analysis_results
        self.strategies = []
    
    def generate_strategy(self):
        """
        Generate modernization strategy based on analysis
        """
        # Assess current state
        risk_level = self._calculate_risk_level()
        complexity = self._assess_complexity()
        business_criticality = self._assess_business_criticality()
        
        # Choose strategy
        if risk_level == 'high' or business_criticality == 'critical':
            strategy = self._strangler_fig_strategy()
        elif complexity == 'low':
            strategy = self._big_bang_strategy()
        else:
            strategy = self._incremental_strategy()
        
        return self._format_strategy(strategy)
    
    def _strangler_fig_strategy(self):
        """Strangler Fig pattern for gradual replacement"""
        return {
            'name': 'Strangler Fig Pattern',
            'description': 'Gradually replace legacy system with new implementation',
            'phases': [
                {
                    'phase': 1,
                    'name': 'Facade Creation',
                    'duration': '2-4 weeks',
                    'tasks': [
                        'Create API facade over legacy system',
                        'Implement logging and monitoring',
                        'Document existing interfaces',
                        'Set up feature toggles'
                    ]
                },
                {
                    'phase': 2,
                    'name': 'Incremental Migration',
                    'duration': '3-6 months',
                    'tasks': [
                        'Identify bounded contexts',
                        'Migrate one context at a time',
                        'Implement new services',
                        'Route traffic through facade'
                    ]
                },
                {
                    'phase': 3,
                    'name': 'Legacy Decommission',
                    'duration': '1-2 months',
                    'tasks': [
                        'Verify all functionality migrated',
                        'Remove legacy code',
                        'Update documentation',
                        'Archive legacy system'
                    ]
                }
            ],
            'benefits': [
                'Low risk approach',
                'Continuous delivery possible',
                'Easy rollback',
                'Business continuity maintained'
            ],
            'challenges': [
                'Longer timeline',
                'Temporary complexity increase',
                'Requires careful coordination'
            ]
        }
    
    def _incremental_strategy(self):
        """Incremental modernization approach"""
        return {
            'name': 'Incremental Modernization',
            'description': 'Modernize system component by component',
            'phases': [
                {
                    'phase': 1,
                    'name': 'Foundation',
                    'duration': '4-6 weeks',
                    'tasks': [
                        'Set up modern build pipeline',
                        'Introduce automated testing',
                        'Establish coding standards',
                        'Create modernization backlog'
                    ]
                },
                {
                    'phase': 2,
                    'name': 'Core Modernization',
                    'duration': '4-8 months',
                    'tasks': [
                        'Upgrade frameworks incrementally',
                        'Refactor critical components',
                        'Introduce modern patterns',
                        'Improve test coverage'
                    ]
                },
                {
                    'phase': 3,
                    'name': 'Architecture Evolution',
                    'duration': '2-4 months',
                    'tasks': [
                        'Extract microservices',
                        'Implement API gateway',
                        'Modernize data layer',
                        'Cloud migration'
                    ]
                }
            ]
        }
```

### 3. Code Transformation

Transform legacy code patterns:

**Legacy Code Transformer**
```python
class LegacyCodeTransformer:
    def __init__(self):
        self.transformations = {
            'callback_to_promise': self.transform_callbacks_to_promises,
            'class_to_functional': self.transform_class_to_functional,
            'xml_to_annotation': self.transform_xml_to_annotations,
            'sync_to_async': self.transform_sync_to_async,
            'procedural_to_oop': self.transform_procedural_to_oop
        }
    
    def transform_callbacks_to_promises(self, code):
        """Transform callback-based code to promises"""
        # Example: Node.js callback to promise
        pattern = r'function\s+(\w+)\s*\([^)]*,\s*callback\s*\)\s*{'
        
        transformed = re.sub(
            pattern,
            lambda m: f'async function {m.group(1)}(...args) {{',
            code
        )
        
        # Transform callback calls
        transformed = re.sub(
            r'callback\s*\(\s*null\s*,\s*(.+?)\s*\)',
            r'return \1',
            transformed
        )
        
        transformed = re.sub(
            r'callback\s*\(\s*(.+?)\s*\)',
            r'throw new Error(\1)',
            transformed
        )
        
        return transformed
    
    def modernize_java_code(self, code):
        """Modernize Java code patterns"""
        transformations = [
            # Use var for local variables (Java 10+)
            (r'(\s+)([A-Z]\w+)\s+(\w+)\s*=\s*new\s+\2\s*\(',
             r'\1var \3 = new \2('),
            
            # Convert to Stream API
            (r'for\s*\(\s*(\w+)\s+(\w+)\s*:\s*(\w+)\s*\)\s*{\s*if\s*\((.+?)\)\s*{\s*(\w+)\.add\(\2\);\s*}\s*}',
             r'\5 = \3.stream().filter(\2 -> \4).collect(Collectors.toList());'),
            
            # Use method references
            (r'\.map\(\s*(\w+)\s*->\s*\1\.(\w+)\(\)\s*\)',
             r'.map(\1::\2)'),
            
            # Convert anonymous classes to lambdas
            (r'new\s+\w+\s*\(\s*\)\s*{\s*@Override\s*public\s+\w+\s+(\w+)\([^)]*\)\s*{\s*(.+?)\s*}\s*}',
             r'() -> { \2 }')
        ]
        
        result = code
        for pattern, replacement in transformations:
            result = re.sub(pattern, replacement, result, flags=re.DOTALL)
        
        return result
    
    def modernize_python_code(self, code):
        """Modernize Python code (2 to 3 and modern patterns)"""
        transformations = [
            # String formatting
            (r'"%s"\s*%\s*\(([^)]+)\)', r'f"{\1}"'),
            (r'"{}".format\(([^)]+)\)', r'f"{\1}"'),
            
            # Type hints
            (r'def\s+(\w+)\(self,\s*(\w+),\s*(\w+)\):',
             r'def \1(self, \2: Any, \3: Any) -> None:'),
            
            # Dictionary comprehensions
            (r'dict\(\[(.*?)\sfor\s+(.*?)\sin\s+(.*?)\]\)',
             r'{\1 for \2 in \3}'),
            
            # Context managers
            (r'(\w+)\s*=\s*open\((.+?)\)\s*\n(.+?)\n\1\.close\(\)',
             r'with open(\2) as \1:\n\3')
        ]
        
        result = code
        for pattern, replacement in transformations:
            result = re.sub(pattern, replacement, result, flags=re.MULTILINE)
        
        return result
```

### 4. Architecture Modernization

Modernize system architecture:

**Architecture Modernizer**
```python
class ArchitectureModernizer:
    def analyze_current_architecture(self, codebase):
        """Analyze and classify current architecture"""
        patterns = {
            'monolithic': self._detect_monolith,
            'layered': self._detect_layered,
            'soa': self._detect_soa,
            'microservices': self._detect_microservices
        }
        
        current_arch = None
        for arch_type, detector in patterns.items():
            if detector(codebase):
                current_arch = arch_type
                break
        
        return {
            'current': current_arch,
            'issues': self._identify_architectural_issues(current_arch),
            'target': self._recommend_target_architecture(current_arch),
            'migration_path': self._design_migration_path(current_arch)
        }
    
    def _design_migration_path(self, current_arch):
        """Design path from current to target architecture"""
        if current_arch == 'monolithic':
            return self._monolith_to_microservices()
        elif current_arch == 'layered':
            return self._layered_to_hexagonal()
        else:
            return self._general_modernization()
    
    def _monolith_to_microservices(self):
        """Migration path from monolith to microservices"""
        return {
            'approach': 'Domain-Driven Design Decomposition',
            'steps': [
                {
                    'step': 1,
                    'name': 'Identify Bounded Contexts',
                    'description': 'Use DDD to identify service boundaries',
                    'deliverables': [
                        'Context map',
                        'Domain model',
                        'Service boundaries'
                    ],
                    'code_example': '''
# Service boundary identification
class BoundedContextAnalyzer:
    def identify_contexts(self, codebase):
        contexts = []
        
        # Analyze package/module dependencies
        dependencies = self.analyze_dependencies(codebase)
        
        # Find clusters of high cohesion
        clusters = self.find_cohesive_clusters(dependencies)
        
        # Map to business capabilities
        for cluster in clusters:
            context = {
                'name': self.derive_context_name(cluster),
                'modules': cluster['modules'],
                'entities': self.extract_entities(cluster),
                'services': self.extract_services(cluster),
                'external_dependencies': self.find_external_deps(cluster)
            }
            contexts.append(context)
        
        return contexts
'''
                },
                {
                    'step': 2,
                    'name': 'Extract First Service',
                    'description': 'Start with least coupled context',
                    'code_example': '''
# Service extraction pattern
class ServiceExtractor:
    def extract_service(self, context, monolith):
        # Create service structure
        service = {
            'name': context['name'] + '-service',
            'api': self.design_api(context),
            'data': self.extract_data_model(context),
            'business_logic': self.extract_business_logic(context)
        }
        
        # Create anti-corruption layer
        acl = self.create_anti_corruption_layer(service, monolith)
        
        # Set up communication
        self.setup_service_communication(service, monolith, acl)
        
        return service, acl
'''
                }
            ]
        }
```

### 5. Testing Legacy Code

Strategies for testing untestable legacy code:

**Legacy Testing Framework**
```python
class LegacyTestingStrategy:
    def create_test_strategy(self, legacy_code):
        """Create testing strategy for legacy code"""
        return {
            'characterization_tests': self._create_characterization_tests(),
            'seam_identification': self._identify_test_seams(),
            'test_harness': self._build_test_harness(),
            'coverage_improvement': self._plan_coverage_improvement()
        }
    
    def _create_characterization_tests(self):
        """Create tests that capture current behavior"""
        return '''
import unittest
from unittest.mock import patch, MagicMock
import json

class CharacterizationTest(unittest.TestCase):
    """
    Characterization tests capture current behavior
    without judging if it's correct
    """
    
    def setUp(self):
        # Capture current state
        self.legacy_system = LegacySystem()
        self.golden_master = self.load_golden_master()
    
    def test_current_behavior(self):
        """Test that system behaves as it currently does"""
        # Run system with known inputs
        inputs = self.golden_master['inputs']
        actual_outputs = []
        
        for input_data in inputs:
            result = self.legacy_system.process(input_data)
            actual_outputs.append(result)
        
        # Compare with recorded outputs
        expected_outputs = self.golden_master['outputs']
        
        for i, (actual, expected) in enumerate(zip(actual_outputs, expected_outputs)):
            with self.subTest(i=i):
                self.assertEqual(
                    actual, expected,
                    f"Behavior changed for input {i}"
                )
    
    def test_with_approval_testing(self):
        """Use approval testing for complex outputs"""
        result = self.legacy_system.generate_report(test_data)
        
        # Save result to file
        with open('approval_test_output.txt', 'w') as f:
            f.write(result)
        
        # Compare with approved version
        self.assert_files_equal(
            'approval_test_output.txt',
            'approved/report_output.txt'
        )
    
    @patch('legacy_system.external_service')
    def test_with_mocked_dependencies(self, mock_service):
        """Test legacy code with external dependencies mocked"""
        # Record actual calls to external service
        mock_service.side_effect = self.record_and_return
        
        # Run legacy code
        result = self.legacy_system.complex_operation()
        
        # Verify behavior matches recorded interactions
        self.verify_recorded_interactions()
'''
    
    def _identify_test_seams(self):
        """Identify seams for testing"""
        return '''
class SeamIdentifier:
    """
    Find seams in legacy code where tests can be inserted
    """
    
    def find_seams(self, code_file):
        seams = []
        
        # Object seam - where objects are created
        object_seams = self.find_object_creation_points(code_file)
        seams.extend([
            {
                'type': 'object',
                'location': seam,
                'strategy': 'Extract factory method'
            }
            for seam in object_seams
        ])
        
        # Link seam - where methods are called
        link_seams = self.find_method_calls(code_file)
        seams.extend([
            {
                'type': 'link',
                'location': seam,
                'strategy': 'Extract interface'
            }
            for seam in link_seams
        ])
        
        # Preprocessing seam - compile-time substitution
        preprocess_seams = self.find_preprocessor_directives(code_file)
        seams.extend([
            {
                'type': 'preprocessing',
                'location': seam,
                'strategy': 'Use test configuration'
            }
            for seam in preprocess_seams
        ])
        
        return seams
'''
```

### 6. Incremental Modernization

Implement safe, incremental improvements:

**Incremental Modernizer**
```python
class IncrementalModernizer:
    def create_modernization_pipeline(self):
        """Create pipeline for incremental modernization"""
        return {
            'stages': [
                self._stage_1_stabilize(),
                self._stage_2_test(),
                self._stage_3_refactor(),
                self._stage_4_modernize(),
                self._stage_5_optimize()
            ],
            'validation': self._create_validation_gates(),
            'rollback': self._create_rollback_procedures()
        }
    
    def _stage_1_stabilize(self):
        """Stabilize the legacy system"""
        return {
            'name': 'Stabilization',
            'duration': '2-4 weeks',
            'goals': [
                'Stop the bleeding',
                'Fix critical bugs',
                'Improve monitoring'
            ],
            'tasks': [
                {
                    'task': 'Add logging',
                    'code': '''
# Add comprehensive logging
import logging
from functools import wraps

def add_logging(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        logger = logging.getLogger(func.__module__)
        logger.info(f"Calling {func.__name__} with args={args}, kwargs={kwargs}")
        try:
            result = func(*args, **kwargs)
            logger.info(f"{func.__name__} returned {result}")
            return result
        except Exception as e:
            logger.error(f"{func.__name__} failed with {e}")
            raise
    return wrapper

# Apply to legacy functions
@add_logging
def legacy_function(data):
    # Original legacy code
    pass
'''
                },
                {
                    'task': 'Add error handling',
                    'code': '''
# Wrap legacy code with proper error handling
class LegacyWrapper:
    def __init__(self, legacy_component):
        self.legacy = legacy_component
        self.error_handler = ErrorHandler()
    
    def safe_execute(self, operation, *args, **kwargs):
        try:
            return getattr(self.legacy, operation)(*args, **kwargs)
        except Exception as e:
            self.error_handler.handle(e, operation, args, kwargs)
            # Graceful degradation
            return self.get_fallback_result(operation)
'''
                }
            ]
        }
    
    def _stage_3_refactor(self):
        """Refactor for maintainability"""
        return {
            'name': 'Refactoring',
            'duration': '4-8 weeks',
            'goals': [
                'Improve code structure',
                'Reduce complexity',
                'Enable future changes'
            ],
            'patterns': [
                {
                    'pattern': 'Extract Method',
                    'before': '''
def process_order(order):
    # Validate order
    if not order.id or not order.items:
        raise ValueError("Invalid order")
    if order.total < 0:
        raise ValueError("Invalid total")
    
    # Calculate discount
    discount = 0
    if order.customer.type == 'premium':
        discount = order.total * 0.1
    elif order.customer.type == 'regular':
        discount = order.total * 0.05
    
    # Apply discount
    order.total = order.total - discount
    
    # Process payment
    if order.payment_method == 'credit':
        charge_credit_card(order.customer.card, order.total)
    elif order.payment_method == 'paypal':
        charge_paypal(order.customer.email, order.total)
''',
                    'after': '''
def process_order(order):
    validate_order(order)
    discount = calculate_discount(order)
    order.total = apply_discount(order.total, discount)
    process_payment(order)

def validate_order(order):
    if not order.id or not order.items:
        raise ValueError("Invalid order")
    if order.total < 0:
        raise ValueError("Invalid total")

def calculate_discount(order):
    discount_rates = {
        'premium': 0.1,
        'regular': 0.05
    }
    return order.total * discount_rates.get(order.customer.type, 0)

def process_payment(order):
    payment_processors = {
        'credit': lambda: charge_credit_card(order.customer.card, order.total),
        'paypal': lambda: charge_paypal(order.customer.email, order.total)
    }
    processor = payment_processors.get(order.payment_method)
    if processor:
        processor()
'''
                }
            ]
        }
```

### 7. Migration Validation

Ensure correctness during modernization:

**Migration Validator**
```python
class MigrationValidator:
    def create_validation_suite(self):
        """Create comprehensive validation suite"""
        return {
            'functional_validation': self._functional_tests(),
            'performance_validation': self._performance_tests(),
            'data_validation': self._data_integrity_tests(),
            'integration_validation': self._integration_tests(),
            'user_acceptance': self._uat_tests()
        }
    
    def _functional_tests(self):
        """Validate functional equivalence"""
        return '''
class FunctionalValidator:
    def __init__(self, legacy_system, modern_system):
        self.legacy = legacy_system
        self.modern = modern_system
        self.test_cases = self.load_test_cases()
    
    def validate_equivalence(self):
        """Ensure modern system behaves like legacy"""
        results = []
        
        for test_case in self.test_cases:
            legacy_result = self.execute_on_legacy(test_case)
            modern_result = self.execute_on_modern(test_case)
            
            comparison = self.compare_results(
                legacy_result,
                modern_result,
                test_case.tolerance
            )
            
            results.append({
                'test': test_case.name,
                'passed': comparison.equivalent,
                'legacy_output': legacy_result,
                'modern_output': modern_result,
                'differences': comparison.differences
            })
        
        return self.generate_validation_report(results)
    
    def regression_test_suite(self):
        """Generate regression tests from legacy behavior"""
        return """
import pytest
from hypothesis import given, strategies as st

class RegressionTests:
    @given(
        customer_id=st.integers(min_value=1),
        amount=st.floats(min_value=0, max_value=10000),
        date=st.dates()
    )
    def test_calculation_equivalence(self, customer_id, amount, date):
        # Run same calculation on both systems
        legacy_result = legacy_calculator.calculate(customer_id, amount, date)
        modern_result = modern_calculator.calculate(customer_id, amount, date)
        
        # Allow for floating point differences
        assert abs(legacy_result - modern_result) < 0.01
"""
'''
```

### 8. Risk Management

Manage modernization risks:

**Risk Management Framework**
```python
class ModernizationRiskManager:
    def assess_risks(self, modernization_plan):
        """Comprehensive risk assessment"""
        risks = {
            'technical': self._assess_technical_risks(),
            'business': self._assess_business_risks(),
            'operational': self._assess_operational_risks(),
            'timeline': self._assess_timeline_risks()
        }
        
        return self._create_risk_mitigation_plan(risks)
    
    def _assess_technical_risks(self):
        """Identify technical risks"""
        return [
            {
                'risk': 'Data loss during migration',
                'probability': 'medium',
                'impact': 'critical',
                'mitigation': [
                    'Implement comprehensive backup strategy',
                    'Create data validation checksums',
                    'Run parallel systems during transition',
                    'Implement rollback procedures'
                ]
            },
            {
                'risk': 'Performance degradation',
                'probability': 'high',
                'impact': 'high',
                'mitigation': [
                    'Establish performance baselines',
                    'Implement performance testing',
                    'Use feature flags for gradual rollout',
                    'Monitor key metrics continuously'
                ]
            },
            {
                'risk': 'Integration failures',
                'probability': 'high',
                'impact': 'medium',
                'mitigation': [
                    'Create integration test suite',
                    'Implement contract testing',
                    'Use adapter pattern for compatibility',
                    'Maintain backwards compatibility'
                ]
            }
        ]
    
    def create_contingency_plans(self):
        """Create contingency plans for common issues"""
        return {
            'rollback_procedures': '''
#!/bin/bash
# Emergency rollback procedure

echo "Initiating emergency rollback..."

# 1. Stop modern system
systemctl stop modern-app

# 2. Restore database to pre-migration state
pg_restore -h localhost -d appdb backup/pre_migration.dump

# 3. Restart legacy system
systemctl start legacy-app

# 4. Update load balancer
update_load_balancer.sh --route-to legacy

# 5. Notify stakeholders
send_notification.sh --template rollback_complete

echo "Rollback completed"
''',
            'data_recovery': '''
class DataRecoveryManager:
    def recover_from_corruption(self):
        """Recover from data corruption during migration"""
        # Identify corrupted records
        corrupted = self.identify_corrupted_records()
        
        # Attempt automatic recovery
        recovered = 0
        for record in corrupted:
            if self.can_recover_from_audit_log(record):
                self.recover_from_audit(record)
                recovered += 1
            elif self.can_recover_from_backup(record):
                self.recover_from_backup(record)
                recovered += 1
            else:
                self.log_unrecoverable(record)
        
        return {
            'total_corrupted': len(corrupted),
            'recovered': recovered,
            'unrecoverable': len(corrupted) - recovered
        }
'''
        }
```

### 9. Documentation and Knowledge Transfer

Document legacy system knowledge:

**Legacy Documentation Generator**
```python
class LegacyDocumentationGenerator:
    def generate_documentation(self, legacy_system):
        """Generate comprehensive documentation"""
        return {
            'system_overview': self._document_system_overview(),
            'architecture_diagrams': self._generate_architecture_diagrams(),
            'business_rules': self._extract_business_rules(),
            'data_dictionary': self._create_data_dictionary(),
            'integration_points': self._document_integrations(),
            'operational_runbook': self._create_runbook()
        }
    
    def _extract_business_rules(self):
        """Extract and document business rules"""
        return '''
# Business Rules Documentation

## Order Processing Rules

### Discount Calculation
```python
def calculate_discount(order):
    """
    Business Rule: Premium customers get 10% discount,
    Regular customers get 5% discount on orders over $100
    """
    if order.customer.is_premium:
        return order.subtotal * 0.10
    elif order.subtotal > 100:
        return order.subtotal * 0.05
    return 0
```

**Rule ID**: BR-001  
**Category**: Pricing  
**Last Modified**: 2019-03-15  
**Owner**: Sales Department  

### Validation Rules

1. **Order Minimum**: Orders must be at least $25
2. **Credit Limit**: Cannot exceed customer credit limit
3. **Inventory Check**: All items must be in stock

### Special Cases

- **Holiday Pricing**: Additional 5% discount in December
- **Bulk Orders**: Orders over 100 items get volume pricing
- **VIP Customers**: No minimum order requirement
'''
```

### 10. Success Metrics

Define and track modernization success:

```python
class ModernizationMetrics:
    def define_success_metrics(self):
        """Define comprehensive success metrics"""
        return {
            'technical_metrics': {
                'code_quality': {
                    'cyclomatic_complexity': {'target': '<10', 'measure': 'per method'},
                    'test_coverage': {'target': '>80%', 'measure': 'line coverage'},
                    'technical_debt': {'target': '<5%', 'measure': 'of total effort'}
                },
                'performance': {
                    'response_time': {'target': '<200ms', 'measure': 'p95'},
                    'throughput': {'target': '>1000 rps', 'measure': 'sustained'},
                    'error_rate': {'target': '<0.1%', 'measure': 'of requests'}
                }
            },
            'business_metrics': {
                'deployment_frequency': {'target': 'daily', 'current': 'monthly'},
                'lead_time': {'target': '<1 day', 'current': '2 weeks'},
                'mttr': {'target': '<1 hour', 'current': '4 hours'},
                'change_failure_rate': {'target': '<5%', 'current': '15%'}
            },
            'team_metrics': {
                'developer_satisfaction': {'target': '>8/10', 'measure': 'survey'},
                'onboarding_time': {'target': '<1 week', 'current': '1 month'},
                'knowledge_sharing': {'target': '2 sessions/month', 'measure': 'documented'}
            }
        }
    
    def create_dashboard(self):
        """Create modernization progress dashboard"""
        return '''
<!DOCTYPE html>
<html>
<head>
    <title>Legacy Modernization Dashboard</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
    <h1>Modernization Progress</h1>
    
    <div class="metrics-grid">
        <div class="metric-card">
            <h3>Code Quality</h3>
            <canvas id="qualityChart"></canvas>
            <div class="metric-details">
                <p>Complexity: <span class="value">8.5</span> (Target: <10)</p>
                <p>Coverage: <span class="value">72%</span> (Target: >80%)</p>
                <p>Tech Debt: <span class="value">8%</span> (Target: <5%)</p>
            </div>
        </div>
        
        <div class="metric-card">
            <h3>Migration Progress</h3>
            <div class="progress-bar">
                <div class="progress" style="width: 65%">65%</div>
            </div>
            <ul class="milestones">
                <li class="completed">✓ Phase 1: Stabilization</li>
                <li class="completed">✓ Phase 2: Testing Framework</li>
                <li class="in-progress">→ Phase 3: Core Modernization</li>
                <li class="pending">○ Phase 4: Architecture Update</li>
            </ul>
        </div>
        
        <div class="metric-card">
            <h3>Risk Status</h3>
            <div class="risk-matrix">
                <div class="risk high">High: 2</div>
                <div class="risk medium">Medium: 5</div>
                <div class="risk low">Low: 8</div>
            </div>
        </div>
    </div>
    
    <script>
        // Real-time metrics updates
        setInterval(updateMetrics, 5000);
    </script>
</body>
</html>
'''
```

## Output Format

1. **Legacy Analysis Report**: Comprehensive assessment of current system
2. **Modernization Strategy**: Phased approach with timelines and milestones
3. **Risk Assessment**: Identified risks with mitigation strategies
4. **Technical Roadmap**: Detailed technical implementation plan
5. **Testing Strategy**: Approach for maintaining quality during modernization
6. **Progress Tracking**: Metrics and dashboards for monitoring progress
7. **Knowledge Documentation**: Captured business rules and system knowledge
8. **Success Criteria**: Clear metrics for measuring modernization success

Focus on gradual, low-risk modernization that maintains business continuity while transforming legacy systems into modern, maintainable architectures.