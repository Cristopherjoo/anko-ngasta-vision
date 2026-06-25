# Documento 1: Visión de Producto y Arquitectura

## Anko Ngasta Enterprise (v4.4.1)

**Plataforma de Ejecución de IA con Gobernanza Enforced y Arquitectura Dual-Domain**

### 🎯 1. Declaración de Visión

Anko Ngasta es un ecosistema avanzado de interfaces y orquestación de Inteligencia Artificial diseñado bajo el paradigma de **Soberanía Operativa**. El sistema mitiga los riesgos de autonomía descontrolada y alucinaciones en entornos productivos mediante un modelo _Human-in-the-loop_ (HITL), actuando como un cortafuegos inteligente donde los agentes sintéticos proponen y justifican acciones, pero el operador humano retiene el control de ejecución definitivo.

> 💡 **Principio Central:** La Inteligencia Artificial en entornos críticos debe ser gobernada, no obedecida.

### 🏗️ 2. Arquitectura de Control: El Modelo Dual-Domain

Para garantizar la estabilidad del sistema y el respeto absoluto a las invariantes del diseño, la aplicación divide las responsabilidades en dos áreas estrictamente aisladas:

- **SYSTEM (`shared/`):** El núcleo inmutable que gestiona la infraestructura, la seguridad, el registro de tokens y las reglas de gobernanza.
    
- **APPLICATION (`apps/`):** La capa volátil donde residen los flujos de trabajo, las integraciones y las capacidades generativas de la IA.
    

**Enforcement:** Las capacidades generativas tienen prohibido el acceso directo a funciones críticas de la infraestructura. Toda interacción se realiza obligatoriamente a través de una fachada única y unificada (`shared.domain_bridge.SystemAccessLayer`), auditada en tiempo de validación.

### 🖥️ 3. Ecosistema de Interfaces de la Aplicación

<br>

<p align="center">
  <img width="650" alt="Anko Ngasta Enterprise Interface" src="https://github.com" />
</p>

<br>

Anko Ngasta materializa su infraestructura a través de una interfaz reactiva avanzada en **PyQt6 (HighDPI-aware)**, estructurada en tres módulos visuales especializados:

- **🧪 El Sandbox de Co-Procesamiento (Team Sandbox):** Entorno colaborativo y aislado donde el usuario y la IA interactúan. Gestiona hilos de forma segura (_thread-safe_) mediante un enrutador de señales centralizado (`SignalRouter`), permitiendo inyectar contexto y probar código sin riesgo de contaminar el entorno productivo.
    
- **🕸️ El Visor de Grafos Semánticos (Knowledge Management):** Interfaz gráfica que mapea el repositorio de forma geométrica. Visualiza los límites de dominio (_Bounded Contexts_), las dependencias y los contratos de importación en tiempo real, permitiendo tanto al usuario como a la IA "ver" la estructura macro del proyecto.
    
- **📑 Panel de Auditoría y Trazabilidad (Approval Gateway):** La consola central de gobernanza humana. Muestra el flujo de propuestas de la IA, su análisis automatizado de riesgo y su bitácora de justificación en un cuaderno de notas visible para su autorización final.
    

### 🔄 4. Motor de Metadatos Globales (El Whisper Codex)

El sistema recolecta continuamente información analítica tanto a nivel **micro** (métricas de cobertura de Pytest, análisis estático de Mypy, validaciones de importación) como **macro** (estado operativo del roadmap, contratos constitucionales). Toda esta metadata es consolidada dinámicamente en un **Diccionario Global persistido en JSON** (_Whisper Codex_), sincronizándose automáticamente con los disparadores de integración continua (CI/CD) mediante el guardrail de automatización `doc_sync_check.py`.

### 📊 5. Gestión de Deuda Técnica y Roadmap (Bootstrapping de Integridad)

El repositorio se encuentra en una fase activa de estabilización de su runtime bajo el siguiente mapa de ingeniería:

- **Fronteras en Refactorización:** El foco actual está en la migración de acoplamientos remanentes (accesos directos detectados desde la capa de aplicación hacia `shared.infrastructure`) para redirigirlos exclusivamente a través del Bridge.
    
- **Próximos Stoppers Críticos:** 1) Saneamiento de la inicialización en el entorno de `shared.security`. 2) Calibración de las políticas de importaciones permitidas del _Boundary Validator_ (`domain_boundary_validator_strict.py`).
