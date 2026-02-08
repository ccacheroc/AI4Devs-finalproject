# Metodología GAIA (Governance, Architecture, and Intelligent Agents)

GAIA es la aproximación metodológica utilizada en este proyecto para el desarrollo de software asistido por IA de alta fidelidad. Se basa en tres pilares fundamentales:
1.  **Governance**: Control estricto del ciclo de vida, trazabilidad absoluta y cumplimiento de reglas predefinidas.
2.  **Architecture**: Una base técnica sólida basada en **Arquitectura Hexagonal** (Backend) y **Feature-First** (Frontend).
3.  **Intelligent Agents**: El uso de flujos de trabajo (Workflows) y habilidades (Skills) especializadas que guían al agente en cada paso.

---

## 1. El Flujo Principal (Ciclo de Vida de Features)

El desarrollo de cualquier funcionalidad sigue una cadena lógica de refinamiento, desde la intención del usuario hasta el código probado:

### Fase A: Definición y Especificación
1.  **`/plan-feature-descr-from-user-conversation`**: Transforma una conversación informal con el usuario en un documento técnico `feature-descr.md`. Este documento define el "Qué" y el "Por qué".
2.  **`/plan-user-stories-from-features`**: Descompone la descripción en historias de usuario navegables (`user-stories.md`) en formato Gherkin (Given/When/Then).
3.  **`/plan-tickets-from-user-stories`**: Traduce las historias de usuario en unidades mínimas de trabajo técnico (`tickets.md`).

### Fase B: Descubrimiento y Planificación Técnica
4.  **`/technical-discovery`**: Antes de codificar, el agente analiza el codebase actual para identificar componentes reutilizables, tablas existentes o lógica de negocio compartida, evitando duplicidades.
5.  **`/plan-implementation-from-tickets`**: Se crean documentos `plan_TICKET-ID.md` específicos para cada ticket. Estos planes son revisados (y ajustados si es necesario) para asegurar que las decisiones técnicas son explícitas.

### Fase C: Ejecución y TDD
6.  **`/execute-plan`**: Es el motor de ejecución. Sigue un ciclo **Red-Green-Refactor**:
    -   **Red**: Crea un test que falla para demostrar la necesidad del cambio o el bug.
    -   **Green**: Implementa el código mínimo necesario.
    -   **Refactor**: Limpia y optimiza preservando el estado funcional.

---

## 2. Flujos Auxiliares y de Calidad

Para mantener la robustez del sistema, se utilizan flujos de apoyo:

-   **`/fix-error`**: Flujo optimizado para resolver incidencias detectadas en logs o consola, asegurando que la solución se documente y se añadan reglas para evitar regresiones.
-   **`/governance-check`**: Valida que cualquier nuevo contenido (Regla, Workflow o Skill) cumpla con los estándares del proyecto antes de ser integrado.
-   **`/audit-security-compliance`**: Audita el código generado contra los checklists de seguridad (OWASP ASVS, BOLA, XSS, etc.).
-   **`/generate-e2e-test`**: Crea pruebas de extremo a extremo con Playwright utilizando el patrón Page Object Model (POM).
-   **`/refactor-ui-to-brand`**: Asegura que cualquier componente nuevo se alinee con la identidad visual (**VibeCoding**, Glassmorphism, Shadcn UI).

---

## 3. Gobernanza y Reglas del Workspace (`.agent/rules/`)

El comportamiento del agente está restringido por un "marco constitucional" de reglas:
-   **OperationalPhilosophy.md**: Mandato de "No Ticket, No Action", TDD mandatorio y sincronización de artefactos (Zero-Drift).
-   **techstack-backend.md / techstack-frontend.md**: Definición técnica inamovible de las herramientas y patrones permitidos.
-   **security-*.md**: Protocolos de seguridad obligatorios.
-   **brand-guidelines.md**: El "alma" visual del proyecto.

---

## 4. Skills de Apoyo (`.agent/skills/`)

Las skills son capacidades especializadas que el agente "aprende" para tareas complejas:
-   **fastapi-domain-generator**: Para crear dominios de arquitectura hexagonal de forma consistente.
-   **brand-identity**: Proporciona los tokens de diseño y el tono de voz de la aplicación.
-   **testing-e2e-with-playwright**: Conocimiento experto en automatización de UI.
-   **notebooklm-management**: Capacidad de investigación profunda y síntesis de documentación externa.

---

## 5. Trazabilidad y Journaling (`specs/`)

La carpeta `specs/` es la "Caja Negra" del proyecto. Nada ocurre sin dejar rastro:
-   **Journaling (`progress.md`)**: Registro diario de hitos, errores bloqueantes y decisiones tomadas. Es fundamental para retomar el contexto en sesiones posteriores.
-   **Trazabilidad Atómica**: Cada bloque de código modificado lleva un comentario `// [Feature: ...] [Story: ...] [Ticket: ...]` que vincula el código directamente con los documentos de diseño en `specs/`.
-   **Zero-Drift**: Cualquier cambio en el código debe reflejarse en las `specs` y viceversa en el mismo PR.

---

*GAIA no es solo un proceso, es una garantía de que el código generado no solo funciona, sino que es seguro, mantenible y coherente con la visión original.*
