# Asistente_Inteligente_LLM_RAG_System
Este proyecto LLM-RAG añade una capa de IA Generativa, permitiendo a los usuarios finales realizar preguntas complejas sobre el inventario y las ventas utilizando lenguaje natural.



Sistema de Consulta Inteligente Basado en RAG (Retrieval-Augmented Generation)
Este proyecto implementa una arquitectura avanzada de IA Generativa para la extracción de conocimiento y análisis de datos mediante lenguaje natural. El sistema utiliza técnicas de RAG para conectar un modelo de lenguaje de gran escala (LLM) con fuentes de datos estructuradas y privadas, garantizando respuestas precisas, contextualizadas y libres de alucinaciones.

🧠 Arquitectura Técnica
El sistema no depende únicamente del conocimiento preentrenado del modelo, sino que consulta activamente una base de conocimientos antes de generar una respuesta.

1. Motor de Inteligencia Artificial
Model: gpt-4o-mini de OpenAI. Elegido por su equilibrio óptimo entre razonamiento lógico, velocidad de respuesta y eficiencia en el manejo de tokens.

Configuración Determinística: El modelo se ejecuta con una temperature=0. Esto es crítico en entornos analíticos para asegurar que, ante una misma pregunta sobre los datos, la respuesta sea consistente y no creativa.

2. Flujo de Recuperación (Retrieval)
El proceso de "Retrieval" actúa como un puente entre la pregunta del usuario y los datos crudos:

Filtro de Relevancia: Se implementó una función de búsqueda (Top-K) que extrae los k registros más significativos de los DataFrames de ventas o inventario.

Contextualización de Datos: Los registros recuperados se transforman dinámicamente en un formato de texto legible que el LLM puede interpretar como "evidencia" para sus cálculos.

3. Ingeniería de Prompts (Prompt Engineering)
Se diseñó un System Prompt robusto que actúa como el marco de gobierno del agente:

Asignación de Rol: El modelo es instruido para actuar como un "Analista de Datos Experto".

Instrucciones de Delimitación: Se utilizan delimitadores claros para separar el Contexto de la Pregunta, evitando que el modelo confunda las instrucciones con los datos.

Restricción de Conocimiento: Se incluye una directiva de seguridad que obliga al modelo a responder "No tengo esa información" si la respuesta no se encuentra estrictamente dentro del contexto proporcionado.

🛠️ Stack de Tecnologías
Orquestación: Databricks (Spark Runtime).

Procesamiento de Datos: PySpark y Pandas para la manipulación de las tablas de contexto.

LLM SDK: OpenAI API integration.

Entorno: Notebooks de Python con gestión de dependencias automatizada.

🔧 Detalles de Implementación Code-Level
Optimización de la Ventana de Contexto
Para evitar el desbordamiento de tokens y optimizar costos, el notebook incluye lógica para:

Limpieza de Texto: Eliminación de ruido y datos irrelevantes antes de la inyección en el prompt.

Estructuración de Salida: Instrucciones específicas para que el modelo responda en formatos claros (ej. tablas, listas o cifras directas).

Seguridad y Gobernanza
Secret Management: El código utiliza dbutils.secrets para la gestión de la API Key de OpenAI, asegurando que las credenciales nunca queden expuestas en texto plano dentro del código fuente.

Trazabilidad: Sistema de logging que registra la pregunta del usuario y la respuesta generada para auditorías de calidad de la IA.

🚀 Casos de Uso del Módulo
Análisis de Ventas: Consultas sobre totales, promedios y comparativas temporales (ej. "¿Cuánto crecieron las ventas en comparación con el mes anterior?").

Auditoría de Cumplimiento: Preguntas sobre el estado de inventario o KPIs específicos cargados en el sistema.

Automatización de Reportes: Generación de resúmenes ejecutivos a partir de tablas extensas de datos.



⚖️ Copyright y Licencia
© 2025 [joserivas25] - Todos los derechos reservados.

Aviso Legal
Este software y su documentación asociada son propiedad intelectual exclusiva del autor. Queda prohibido cualquier uso del código fuente, arquitectura o metodología con fines comerciales o de lucro sin el consentimiento expreso y por escrito del propietario.

Restricciones de Uso
Uso Académico/Portafolio: Se permite la visualización y estudio del código con fines de evaluación profesional o aprendizaje.

Prohibición de Redistribución: No se permite la redistribución de este código en otros repositorios, plataformas o productos sin atribución y permiso.

Sin Garantía: El software se proporciona "tal cual", sin garantía de ningún tipo, expresa o implícita, incluyendo pero no limitado a las garantías de comerciabilidad o idoneidad para un propósito particular.
