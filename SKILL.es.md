description: Herramienta impulsada por IA para generar, refinar y automatizar tareas de codificación utilizando modelos de lenguaje avanzados
tags: [coding, ai, automation, code-generation, refactoring]
author: OpenClaw Team
version: 1.0.0
dependencies: [openai-api, anthropic-api, huggingface-transformers, python>=3.8, node>=14, git]
environment_variables:
  - DYNAMIC_MAKER_API_KEY: Clave API para proveedor de IA (OpenAI o Anthropic)
  - DYNAMIC_MAKER_MODEL: Modelo preferido (ej., gpt-4, claude-3)
  - DYNAMIC_MAKER_TIMEOUT: Tiempo de espera de solicitud en segundos (predeterminado: 60)
  - DYNAMIC_MAKER_LOG_LEVEL: Verbosidad del registro (debug, info, warn, error)
requirements:
  - Acceso API a OpenAI o Anthropic
  - Entorno Python con bibliotecas requeridas
  - Repositorio Git para gestión de código
  - Node.js para proyectos JavaScript/TypeScript
  - Créditos API suficientes para llamadas de IA

---

# Dynamic Maker

## Purpose

Dynamic Maker es una herramienta impulsada por IA diseñada para acelerar flujos de trabajo de codificación generando fragmentos de código, refactorizando bases de código existentes, automatizando tareas repetitivas y proporcionando sugerencias inteligentes para correcciones de errores y optimizaciones. Se integra perfectamente con entornos de desarrollo para asistir a los desarrolladores en sesiones de codificación en tiempo real.

### Real Use Cases
- **Generación Automatizada de Código**: Genera funciones completas, clases o módulos basados en descripciones en lenguaje natural (ej., "crear un endpoint de API REST para autenticación de usuario en Flask").
- **Asistencia en Refactorización**: Identifica y refactoriza código heredado para mejorar el rendimiento, la legibilidad o la mantenibilidad (ej., convertir código basado en callbacks a async/await en Node.js).
- **Detección y Corrección de Errores**: Analiza código en busca de posibles errores, vulnerabilidades de seguridad o problemas de rendimiento y sugiere correcciones específicas.
- **Generación de Pruebas**: Crea automáticamente pruebas unitarias, de integración o datos simulados para funciones y APIs existentes.
- **Automatización de Documentación**: Genera archivos README completos, documentación de API o comentarios en línea para código no documentado.
- **Soporte para Revisión de Código**: Proporciona retroalimentación impulsada por IA en pull requests, destacando mejores prácticas, posibles problemas y sugerencias de mejora.

## Scope

Dynamic Maker opera en archivos de código en múltiples lenguajes y frameworks, enfocándose en tareas productivas de codificación en lugar de infraestructura o despliegue.

### Specific Commands
- `dynamic-maker generate <prompt>`: Genera código basado en un prompt en lenguaje natural
- `dynamic-maker refactor <file> [--type=performance|readability|security]`: Refactoriza el archivo especificado con sugerencias de IA
- `dynamic-maker fix <file> --issue=<description>`: Aplica correcciones específicas a problemas de código
- `dynamic-maker test <file|function>`: Genera pruebas para el código especificado
- `dynamic-maker docs <file|project>`: Crea documentación para código
- `dynamic-maker review <pr-url>`: Analiza y proporciona retroalimentación en pull requests
- `dynamic-maker optimize <file> --metric=cpu|memory|complexity`: Optimiza código para métricas específicas
- `dynamic-maker explain <code-snippet>`: Proporciona explicaciones detalladas de la funcionalidad del código

## Work Process

### Detailed Steps
1. **Inicialización**: Carga el contexto del proyecto escaneando la base de código, leyendo archivos como package.json, requirements.txt o equivalentes para entender dependencias y estructura del proyecto.
2. **Análisis de Prompt**: Analiza el prompt o comando del usuario, extrayendo intención, archivos objetivo y requisitos específicos (ej., lenguaje, framework, restricciones).
3. **Selección de Modelo de IA**: Elige el modelo de IA apropiado basado en la complejidad de la tarea (GPT-4 para generación compleja, Claude para análisis detallado).
4. **Análisis de Código**: Si se trabaja en archivos existentes, analiza la estructura del código, dependencias y contexto utilizando herramientas de análisis estático.
5. **Generación/Modificación**: Utiliza el modelo de IA para generar o modificar código, asegurando que siga las convenciones del proyecto (linting, formateo).
6. **Validación**: Ejecuta verificaciones de sintaxis, linting y pruebas básicas para verificar el código generado/modificado.
7. **Integración**: Aplica cambios a la base de código, preparándolos en git si corresponde.
8. **Bucle de Retroalimentación**: Presenta resultados al usuario, permitiendo refinamientos iterativos basados en retroalimentación.

### Verification Steps
- Validación de sintaxis utilizando herramientas específicas del lenguaje (ej., `python -m py_compile` para Python, `tsc --noEmit` para TypeScript)
- Linting con reglas configuradas (eslint, pylint, etc.)
- Pruebas de funcionalidad básica ejecutando código generado en un entorno sandbox
- Verificaciones de resolución de dependencias para asegurar que no haya cambios disruptivos

## Golden Rules

1. **Nunca Sobrescribir Sin Respaldo**: Siempre crea respaldos de archivos modificados antes de aplicar cambios.
2. **Respetar Convenciones del Proyecto**: Analiza e imita el estilo de código existente, convenciones de nomenclatura y patrones arquitectónicos.
3. **Priorizar Seguridad**: Marca y evita generar código con posibles vulnerabilidades de seguridad (ej., inyección SQL, XSS).
4. **Mantener Calidad del Código**: Asegura que el código generado pase todos los estándares de linting y pruebas del proyecto.
5. **Ser Transparente**: Indica claramente secciones generadas por IA con comentarios y proporciona razonamiento para cambios.
6. **Limitar Alcance**: Enfócate solo en tareas de codificación; no manejes despliegue, infraestructura o automatización no relacionada con código.
7. **Manejar Errores con Elegancia**: Si falla la generación de IA, proporciona mensajes de error claros y sugerencias alternativas.
8. **Preservar Funcionalidad**: Asegura que la refactorización u optimización no rompa la funcionalidad existente.

## Examples

### Code Generation
**Input**: `dynamic-maker generate \"Create a Python function to validate email addresses using regex\"`

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
**Input**: `dynamic-maker fix app.js --issue=\"Potential null pointer exception in user lookup\"`

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

- `dynamic-maker rollback <file>`: Revertir el último cambio realizado en un archivo utilizando git o respaldo local
- `dynamic-maker undo --commit=<hash>`: Deshacer cambios hasta un hash de commit específico
- `dynamic-maker reset --file=<file>`: Restablecer un archivo a su estado antes de la última operación de Dynamic Maker
- `dynamic-maker backup <file>`: Crear manualmente un respaldo de un archivo antes de la modificación

## Troubleshooting

### Common Issues
1. **Límites de Tasa de API**: Si se alcanzan límites de tasa, implementa retroceso exponencial o cambia a un proveedor de IA diferente.
2. **Alucinaciones del Modelo**: Para código crítico, siempre revisa manualmente la salida generada por IA antes de la integración.
3. **Conflictos de Dependencias**: Ejecuta `dynamic-maker validate-deps` para verificar conflictos antes de aplicar cambios.
4. **Errores de Tiempo de Espera**: Aumenta la variable de entorno `DYNAMIC_MAKER_TIMEOUT` para tareas complejas.
5. **Desajustes de Estilo de Código**: Asegura que el proyecto tenga reglas de linting consistentes configuradas (ej., .eslintrc, pyproject.toml).

### Debug Mode
Habilita el registro de depuración con `export DYNAMIC_MAKER_LOG_LEVEL=debug` para obtener información detallada sobre prompts de IA, respuestas y pasos de procesamiento.