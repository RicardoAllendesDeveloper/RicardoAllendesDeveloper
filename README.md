# Ricardo Allendes Osorio

**Developer — TypeScript · Supabase · Postgres · RLS**

[ricardo.allendes.dev@gmail.com](mailto:ricardo.allendes.dev@gmail.com) · Valparaíso, Chile

Construyo sistemas donde **la base de datos es la parte difícil**, no la capa que se esconde debajo
de un formulario. Me interesa el momento en que una regla de negocio tiene que vivir en el motor
de datos para que sea imposible de saltarse, no solo en la interfaz.

Especialidad: **aplicaciones multi-rol sobre Postgres con Row Level Security**, desarrolladas con
React + TypeScript.

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

También trabajo en **TramaBPM** y **NeoBarber** como colaborador: sistemas en producción, y en
NeoBarber hice el QA del módulo de agenda (62/62 tests, incluida una condición de carrera
verificada en navegador).

---

## Lo que busco

Trabajo como **developer junior→pleno**, idealmente en un equipo donde la base de datos y la
seguridad importen de verdad, o como **freelance** en proyectos donde el reto no sea solo pintar
pantallas.

C#/Godot y Electron son mi segundo eje, no el principal.

## Contacto

**ricardo.allendes.dev@gmail.com** — respondo en español

---

*Los repositorios de trabajos de práctica están archivados: eran aprendizaje, no trabajo real.
Este perfil muestra lo que construí.*