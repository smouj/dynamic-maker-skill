name: Dynamic Maker
description: AI-powered maker for generating, refining, and automating coding tasks using advanced language models
tags: [coding, ai, automation, code-generation, refactoring]
author: OpenClaw Team
version: 1.0.0
dependencies: [openai-api, anthropic-api, huggingface-transformers, python>=3.8, node>=14, git]
environment_variables:
  - DYNAMIC_MAKER_API_KEY: API key for AI provider (OpenAI or Anthropic)
  - DYNAMIC_MAKER_MODEL: Preferred model (e.g., gpt-4, claude-3)
  - DYNAMIC_MAKER_TIMEOUT: Request timeout in seconds (default: 60)
  - DYNAMIC_MAKER_LOG_LEVEL: Logging verbosity (debug, info, warn, error)
requirements:
  - API access to OpenAI or Anthropic
  - Python environment with required libraries
  - Git repository for code management
  - Node.js for JavaScript/TypeScript projects
  - Sufficient API credits for AI calls

---

# Dynamic Maker

## Purpose

Dynamic Maker is an AI-powered tool designed to accelerate coding workflows by generating code snippets, refactoring existing codebases, automating repetitive tasks, and providing intelligent suggestions for bug fixes and optimizations. It integrates seamlessly with development environments to assist developers in real-time coding sessions.

### Real Use Cases
- **Automated Code Generation**: Generate complete functions, classes, or modules based on natural language descriptions (e.g., "create a REST API endpoint for user authentication in Flask").
- **Refactoring Assistance**: Identify and refactor legacy code for better performance, readability, or maintainability (e.g., converting callback-based code to async/await in Node.js).
- **Bug Detection and Fixes**: Analyze code for potential bugs, security vulnerabilities, or performance issues and suggest targeted fixes.
- **Test Generation**: Automatically create unit tests, integration tests, or mock data for existing functions and APIs.
- **Documentation Automation**: Generate comprehensive README files, API documentation, or inline comments for undocumented code.
- **Code Review Support**: Provide AI-driven feedback on pull requests, highlighting best practices, potential issues, and improvement suggestions.

## Scope

Dynamic Maker operates on code files across multiple languages and frameworks, focusing on productive coding tasks rather than infrastructure or deployment.

### Specific Commands
- `dynamic-maker generate <prompt>`: Generate code based on a natural language prompt
- `dynamic-maker refactor <file> [--type=performance|readability|security]`: Refactor specified file with AI suggestions
- `dynamic-maker fix <file> --issue=<description>`: Apply targeted fixes to code issues
- `dynamic-maker test <file|function>`: Generate tests for the specified code
- `dynamic-maker docs <file|project>`: Create documentation for code
- `dynamic-maker review <pr-url>`: Analyze and provide feedback on pull requests
- `dynamic-maker optimize <file> --metric=cpu|memory|complexity`: Optimize code for specific metrics
- `dynamic-maker explain <code-snippet>`: Provide detailed explanations of code functionality

## Work Process

### Detailed Steps
1. **Initialization**: Load project context by scanning the codebase, reading package.json, requirements.txt, or equivalent files to understand dependencies and project structure.
2. **Prompt Analysis**: Parse the user's prompt or command, extracting intent, target files, and specific requirements (e.g., language, framework, constraints).
3. **AI Model Selection**: Choose the appropriate AI model based on task complexity (GPT-4 for complex generation, Claude for detailed analysis).
4. **Code Analysis**: If working on existing files, analyze the code structure, dependencies, and context using static analysis tools.
5. **Generation/Modification**: Use the AI model to generate or modify code, ensuring it follows project conventions (linting, formatting).
6. **Validation**: Run syntax checks, linting, and basic tests to verify the generated/modified code.
7. **Integration**: Apply changes to the codebase, staging them in git if applicable.
8. **Feedback Loop**: Present results to user, allowing for iterative refinements based on feedback.

### Verification Steps
- Syntax validation using language-specific tools (e.g., `python -m py_compile` for Python, `tsc --noEmit` for TypeScript)
- Linting with configured rules (eslint, pylint, etc.)
- Basic functionality tests by running generated code in a sandbox environment
- Dependency resolution checks to ensure no breaking changes

## Golden Rules

1. **Never Overwrite Without Backup**: Always create backups of modified files before applying changes.
2. **Respect Project Conventions**: Analyze and mimic existing code style, naming conventions, and architectural patterns.
3. **Prioritize Security**: Flag and avoid generating code with potential security vulnerabilities (e.g., SQL injection, XSS).
4. **Maintain Code Quality**: Ensure generated code passes all project linting and testing standards.
5. **Be Transparent**: Clearly indicate AI-generated sections with comments and provide reasoning for changes.
6. **Limit Scope**: Focus on coding tasks only; do not handle deployment, infrastructure, or non-code automation.
7. **Handle Errors Gracefully**: If AI generation fails, provide clear error messages and fallback suggestions.
8. **Preserve Functionality**: Ensure that refactoring or optimization does not break existing functionality.

## Examples

### Code Generation
**Input**: `dynamic-maker generate "Create a Python function to validate email addresses using regex"`

**Output**:
```python
import re

def validate_email(email: str) -> bool:
    """
    Validate an email address using a regular expression.
    
    Args:
        email (str): The email address to validate.
    
    Returns:
        bool: True if the email is valid, False otherwise.
    """
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None
```

### Refactoring
**Input**: `dynamic-maker refactor src/auth.py --type=readability`

**Output** (before/after diff):
```diff
- def authenticate(user,password):return True if user=='admin'and password=='secret'else False
+ def authenticate_user(username: str, password: str) -> bool:
+     """
+     Authenticate a user with username and password.
+     
+     Args:
+         username (str): The user's username.
+         password (str): The user's password.
+     
+     Returns:
+         bool: True if authentication succeeds, False otherwise.
+     """
+     # TODO: Implement proper authentication logic
+     return False
```

### Bug Fix
**Input**: `dynamic-maker fix app.js --issue="Potential null pointer exception in user lookup"`

**Output**:
```javascript
// Before
function getUser(id) {
    return users.find(u => u.id === id).name;
}

// After
function getUser(id) {
    const user = users.find(u => u.id === id);
    return user ? user.name : null;
}
```

### Test Generation
**Input**: `dynamic-maker test utils/math.js`

**Output**:
```javascript
const { add, multiply } = require('./math');

describe('Math Utils', () => {
    describe('add', () => {
        test('should add two positive numbers', () => {
            expect(add(2, 3)).toBe(5);
        });
        
        test('should add negative numbers', () => {
            expect(add(-1, -1)).toBe(-2);
        });
    });
    
    describe('multiply', () => {
        test('should multiply two numbers', () => {
            expect(multiply(3, 4)).toBe(12);
        });
    });
});
```

## Rollback Commands

- `dynamic-maker rollback <file>`: Revert the last change made to a file using git or local backup
- `dynamic-maker undo --commit=<hash>`: Undo changes up to a specific commit hash
- `dynamic-maker reset --file=<file>`: Reset a file to its state before the last Dynamic Maker operation
- `dynamic-maker backup <file>`: Manually create a backup of a file before modification

## Troubleshooting

### Common Issues
1. **API Rate Limits**: If hitting rate limits, implement exponential backoff or switch to a different AI provider.
2. **Model Hallucinations**: For critical code, always review AI-generated output manually before integration.
3. **Dependency Conflicts**: Run `dynamic-maker validate-deps` to check for conflicts before applying changes.
4. **Timeout Errors**: Increase `DYNAMIC_MAKER_TIMEOUT` environment variable for complex tasks.
5. **Code Style Mismatches**: Ensure project has consistent linting rules configured (e.g., .eslintrc, pyproject.toml).

### Debug Mode
Enable debug logging with `export DYNAMIC_MAKER_LOG_LEVEL=debug` to get detailed information about AI prompts, responses, and processing steps.