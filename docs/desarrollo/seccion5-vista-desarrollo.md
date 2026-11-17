# 5. Vista de desarrollo

## 5.1 Diagrama de paquetes

Archivo fuente: `docs/desarrollo/vision360-paquetes.puml`. Imagen: `docs/desarrollo/vision360-paquetes.png`.

| Paquete | Estereotipo | Piezas que contiene |
|---|---|---|
| Presentación web | «presentación» | VistaPanorama, PanelAdministracion |
| Seguimiento | «dominio» | ControlConsultaPanorama, ControlIndicadoresAvance |
| Núcleo de proyectos | «dominio» | Proyecto, Iniciativa, Requerimiento, Hito, Avance, FuenteInformacion, RegistroSincronizacion |
| Alertas | «dominio» | ControlAlertasDesviaciones, ReglaAlerta, Alerta, RegistroEvaluacion |
| Integración de fuentes | «integración» | ControlIntegracion, AdaptadorRedmine, AdaptadorExcel |
| Seguridad y permisos | «utilitario» | PerfilUsuario |
| Registro de errores | «utilitario» | RegistroErrores |
| Persistencia | «plataforma» | BaseDatosRelacional |
| Tareas programadas | «plataforma» | Planificador |

## 5.2 Tabla de dependencias

| # | Origen | Destino | Por qué existe |
|---|---|---|---|
| D1 | Presentación web | Seguimiento | La vista del panorama llama al control de consulta (CU-01). |
| D2 | Presentación web | Integración de fuentes | El panel de administración solicita la sincronización manual (CU-09, FA-04). |
| D3 | Seguimiento | Núcleo de proyectos | El control recupera proyectos, avances y fuentes para presentar el panorama. |
| D4 | Seguimiento | Alertas | El panorama muestra las alertas disponibles al consultar indicadores (CU-04). |
| D5 | Seguimiento | Seguridad y permisos | Antes de mostrar datos se verifican los permisos del perfil (CU-01, RF-07). |
| D6 | Alertas | Núcleo de proyectos | La evaluación de desviaciones necesita proyectos e hitos (CU-10). |
| D7 | Integración de fuentes | Núcleo de proyectos | La sincronización guarda los registros consolidados de Redmine y Excel (CU-09). |
| D8 | Integración de fuentes | Alertas | Al terminar una sincronización válida se evalúan alertas (CU-09 «include» CU-10). |
| D9 | Núcleo de proyectos | Persistencia | Los proyectos y avances se guardan y consultan en la base de datos. |
| D10 | Integración de fuentes | Registro de errores | Un fallo de Redmine o Excel debe quedar registrado (CU-09 FA-01, FA-02). |
| D11 | Alertas | Registro de errores | Si la evaluación no puede completarse, la causa queda registrada (CU-10 E-01). |

Dentro del paquete Seguimiento también existe la relación «include» de CU-01 a CU-04.

**Verificación de ciclos.** Ningún paquete recibe una flecha que regrese a su origen por otro camino. Las cadenas son Presentación → Seguimiento → Alertas → Núcleo, y Presentación → Integración → Alertas → Núcleo. Seguimiento y Alertas no dependen entre sí en sentido contrario, y Alertas no depende de Seguimiento. No hay ciclos.

**Regla de dirección.** Ninguna flecha sale de Persistencia, Seguridad o Registro de errores hacia un dominio. Los dominios sí dependen de la plataforma y de los utilitarios.

## 5.3 Tabla de plataformas

| Necesidad | Plataforma elegida | Justificación |
|---|---|---|
| Lenguaje y framework del backend | Python con Django | Trae ORM, autenticación y permisos por perfil (RF-07) y un panel de administración (CU-11). Reduce código propio en seguridad. *Por validar con el equipo.* |
| Base de datos | PostgreSQL | Relaciona proyectos, iniciativas y requerimientos con integridad referencial. Permite restricciones únicas para evitar alertas activas duplicadas (CU-10, fiabilidad). |
| Tareas programadas y asíncronas | Celery con Celery Beat y Redis | Beat ejecuta la sincronización y la evaluación programadas (temporizador). Celery procesa la sincronización manual sin bloquear la interfaz (200 registros en menos de 5 minutos). |
| Cliente web | Plantillas del servidor (Django templates) con Bootstrap | El proyecto requiere un panel web, no una app móvil. Evita un frontend separado y reduce el tiempo de desarrollo. |
| Acceso a Redmine | API REST de Redmine con clave en variables de entorno | Redmine expone su API REST. La clave no se escribe en el código (CU-09, seguridad). |
| Acceso a Excel online | Microsoft Graph API | Es el mecanismo estándar para leer archivos de Excel en la nube. *Pendiente de validar, como indica el DAS.* |
| Registro de errores | Sistema de logging de Django, más la tabla RegistroSincronizacion | Cubre la trazabilidad de fallos y resultados exigida en CU-09 (fiabilidad). |

## 5.4 Chequeo con la vista de procesos (Taller 5)

| Control o adaptador (robustez) | Caso de uso | Paquete donde queda | Estado |
|---|---|---|---|
| Vista de panorama de proyectos | CU-01 | Presentación web | Correcto |
| Panel de administración | CU-09 | Presentación web | Correcto |
| Control de consulta de panorama | CU-01 | Seguimiento | Correcto |
| Control de indicadores de avance | CU-04 | Seguimiento | Correcto |
| Perfil de usuario | CU-01 | Seguridad y permisos | Correcto |
| Control de integración | CU-09 | Integración de fuentes | Correcto |
| Adaptador Redmine | CU-09 | Integración de fuentes | Correcto |
| Adaptador Excel | CU-09 | Integración de fuentes | Correcto |
| Control de alertas por desviaciones | CU-10 | Alertas | Correcto |
| Proyecto, Avance, Fuente de información, Registro de sincronización | CU-01, CU-04, CU-09 | Núcleo de proyectos | Correcto |
| Hito, Regla de alerta, Alerta, Registro de evaluación | CU-10 | Núcleo (Hito) y Alertas (resto) | Correcto |

No existe ningún control por herramienta (como ControlRedmine). Los controles son por caso de uso y las herramientas se acceden solo mediante adaptadores.

## 5.5 Estructura de carpetas del repositorio

```
docs/
  desarrollo/
    vision360-paquetes.puml
    vision360-paquetes.png
    seccion5-vista-desarrollo.md
src/
  presentacion/
  seguimiento/
  nucleo/
  alertas/
  integracion/
  utilitarios/
    seguridad/
    registro/
  plataforma/
    persistencia/
    tareas/
```

Cada carpeta corresponde a un paquete del diagrama. No se usan carpetas por tipo técnico (controllers, models).

---

## Borrador de bitácora IA (IA-07 · Vista de desarrollo)

> Antes de entregar, reemplacen cada campo con sus consultas reales. Si alguien no puede explicar un punto, ese punto no se entrega.

- **Integrante:** [nombre]
- **Herramienta:** [ej. ChatGPT / Claude]
- **Objetivo:** Construir la vista de desarrollo (paquetes, dependencias, plataformas) a partir de las piezas de las vistas lógica y de procesos.
- **Prompt:** [resumen real de la consulta]
- **Respuesta (resumen):** [qué propuso la IA]
- **Qué usamos:** [por ejemplo: la separación en paquetes y la regla de dirección de dependencias]
- **Qué descartamos y por qué:** [por ejemplo: una carpeta de Redmine, porque violaba la regla de no tener controles por herramienta]
- **Verificación:** [cómo lo comprobaron: revisión de ciclos, cruce con la robustez del Taller 5, reglas del checklist]
- **¿Error de la IA?:** [qué corrigieron]
- **Decisión del grupo:** [decisión final]
