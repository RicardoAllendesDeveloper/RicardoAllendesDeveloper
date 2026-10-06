# Ricardo Allendes Osorio

**Desarrollador full-stack — TypeScript · Supabase · Postgres · RLS**

ricardo.allendes.dev@gmail.com · Santiago, Chile (La Florida) · Trabajo remoto

> **In English:** Full-stack developer (TypeScript · Supabase · Postgres · RLS). I harden Postgres
> databases: RLS policies, reproducible migrations and SQL test suites that run against the real
> database. AI-assisted delivery, human review. Available for remote work.

**Endurezco bases de datos Postgres.** Políticas RLS que no se pueden saltar, migraciones
reproducibles y suites de pruebas que corren contra la base real, no contra mocks.

Trabajo con agentes de IA, así que entrego rápido. El criterio está en revisar lo que producen, y
ahí es donde aparecen las reglas que aguantan: un trigger que escribe en otra tabla, una política
que decide filas, una migración que se puede volver a aplicar.

---

## Lo que hago

**Auditoría de seguridad en Supabase / Postgres.** Reviso tus políticas RLS, tus funciones RPC y tus
roles, y entrego un informe con lo que falta, la matriz de permisos y el SQL para cerrarlo.

**Suites de pruebas sobre la base de datos real.** Cada caso corre dentro de una transacción con
`ROLLBACK`: no ensucian datos y no hay mocks que escondan el problema.

**Entrega de features por encargo.** Frontend React/TypeScript con backend Supabase, o escritorio
con Electron.

---

## El proyecto principal

### [SWIMyti](https://github.com/RicardoAllendesDeveloper/SWIMyti) — ficha clínica inmutable

SaaS de ficha clínica digital para centros de salud de baja complejidad en Chile.

No es un CRUD con roles: la ficha clínica es **append-only** por requisito legal (Ley 19.628).
No se edita ni se borra, y eso lo imponen triggers de Postgres, no una validación de formulario.

- **61 migraciones** versionadas y aplicadas de forma reproducible
- **42 casos de prueba SQL** que corren dentro de transacciones con `ROLLBACK` sobre la base real
- **71 tests de frontend** (Vitest) y un validador que ejecuta **todas** las consultas del cliente
  contra la base de datos, no un mock
- 7 roles con permisos acumulativos; la seguridad vive en **RLS + RPC `SECURITY DEFINER`**

![SWIMyti](https://github.com/RicardoAllendesDeveloper/SWIMyti/raw/main/capturas/04-agenda.png)

Lo que más me costó, y lo que más enseñó:

- **Un trigger que escribe en otra tabla debe ser `SECURITY DEFINER`.** Corriendo como `invoker`
  toma los permisos de quien lo disparó: si ese rol no puede escribir en la tabla destino, el
  `UPDATE` afecta **cero filas sin dar error**. El síntoma era silencioso, que es lo peor.
- **PostgREST no acepta espacio entre dos paréntesis de cierre**, y ese error rompió siete pantallas
  a la vez porque los dos estilos convivían en el mismo archivo. De ahí salió el validador de
  consultas.
- **RLS decide filas; los triggers deciden columnas.** Las restricciones por columna no se pueden
  expresar en una política.

---

## Otros proyectos

| Proyecto | Qué es |
|---|---|
| **NELA** | App de escritorio para la gestión de una consulta médica. Electron + auto-update. |
| **Calc_IMC_Personal** | Calculadora de IMC e índice de obesidad en HTML/CSS. |
| **Juegos en Godot (C#/.NET)** | *Gray Cats* y *Suruvanus*: ARPG 3D, multijugador en LAN, bots con autoridad de servidor. |

### Experiencia en producción

**TramaBPM** — desarrollo por módulos en una plataforma BPM en producción (Next.js, Resend). Cada
módulo se entrega con su migración SQL, sus RPC y sus pruebas. Construí el motor de emails completo
(envío con opt-out, trazabilidad de envíos y clics, plantillas, segmentación por artista, digest
automático) y módulos de visualización con 31 pruebas nuevas. Flujo de trabajo: rama propia y PR a
`main` con revisión.

**NeoBarber** — QA del módulo de agenda: **62/62 tests**, incluida una condición de carrera
verificada en navegador sobre la aplicación en producción.

---

## Contacto

**ricardo.allendes.dev@gmail.com** — escribo en español e inglés

---

*Los repositorios de trabajos de práctica están archivados a propósito: este perfil muestra lo que
construí, no lo que estudié.*
