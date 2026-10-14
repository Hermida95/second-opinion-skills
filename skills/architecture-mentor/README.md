# architecture-mentor

**Un profesor de arquitectura, infraestructura y stack dentro de tu asistente de IA.**

Normalmente, cuando le pides a una IA «hazme una app de tareas», se pone a programar y elige por ti el lenguaje, la base de datos y dónde alojarla. Tú recibes una app que funciona, pero no sabes *por qué* está hecha así ni cómo decidir la próxima vez.

Esta skill cambia eso. **Antes de escribir una sola línea, te hace decidir**, una decisión cada vez, y te explica cada opción con sus pros y contras. Tú aprendes a decidir; la IA construye después.

> El objetivo no es programar mejor. Es **saber qué pedir y por qué**.

## Qué hace

Tiene dos modos:

### Modo A: antes de construir
Le dices lo que quieres hacer y, en lugar de empezar a programar:

1. **Mira lo que ya existe** (si estás dentro de un proyecto): stack, hosting, límites reales.
2. **Te hace unas pocas preguntas** que cambian la decisión: cuántos usuarios, cuánto quieres gastar, qué sabes ya, qué quieres aprender.
3. **Recorre las decisiones una por una**: arquitectura, backend, frontend, datos, autenticación, hosting, despliegue, costes, seguridad. Para cada una te da:
   - qué es y por qué importa (con el vocabulario explicado),
   - 2-4 opciones, cada una con **«mejor si…»**, lo que ganas y lo que pierdes,
   - **una recomendación razonada para tu caso**,
   - qué te haría cambiar de opinión.
4. **Te avisa del sobredimensionamiento**: si lo de moda es excesivo para lo que necesitas (por ejemplo, microservicios para una app doméstica), te lo dice.
5. **Termina con un documento de decisiones** (`docs/DECISIONES.md`) que puedes pasar a la IA constructora como especificación.

### Modo B: explicar un proyecto que ya existe
Le pasas un proyecto (o varios) y te explica **qué tiene y por qué**: capa por capa, qué usa, por qué probablemente se eligió así, qué alternativas había, si encaja con la escala real y qué cambiaría. Sirve para entender algo ya construido, revisar un plan antes de empezar o comparar proyectos entre sí.

## Cómo se usa

### Instalación

Como plugin:

```bash
claude plugin marketplace add Hermida95/second-opinion-skills
claude plugin install architecture-mentor@second-opinion
```

O copiando la carpeta a tu directorio de skills (el nombre de la carpeta debe ser `architecture-mentor`):

```bash
git clone https://github.com/Hermida95/second-opinion-skills
cp -R second-opinion-skills/skills/architecture-mentor ~/.claude/skills/architecture-mentor
```

### Cómo invocarla

Se activa sola cuando le pides crear algo o preguntas qué usar. Nombrarla es lo más fiable:

| Quieres… | Dile algo como… |
|---|---|
| Decidir antes de construir | *«Quiero hacer una app de tareas para mi casa. Usa architecture-mentor.»* |
| Una sola duda | *«¿Dónde debería alojar esto y por qué?»* |
| Que decida por ti, pero explicado | *«Decide tú el stack, pero explícame por qué.»* |
| Entender un proyecto hecho | *«Explícame este proyecto con architecture-mentor: ruta/del/proyecto»* |
| Comparar varios | *«Compara estos tres proyectos y dime qué decisiones repiten.»* |

## Ejemplo (resumido)

> **Tú:** Quiero una app de tareas del hogar para mi pareja y para mí. Usa architecture-mentor.
>
> **IA:** *(pregunta)* ¿Cuántas personas la usarán? ¿Desde el móvil o el ordenador? ¿Cuánto quieres pagar al mes? ¿Qué quieres aprender además de la app?
>
> **Tú:** Dos personas, desde el móvil, 0 €, y quiero entender hosting y datos.
>
> **IA:**
> ### Arquitectura: ¿cómo se organizan las piezas?
> - **A. Monolito (recomendada para ti):** una sola aplicación. *Mejor si* sois 1-2 personas. Ganas simplicidad; pierdes poco.
> - **B. Serverless:** sin servidor que mantener. *Mejor si* el tráfico es irregular. Ganas cero operación; pierdes depuración sencilla.
> - **C. Microservicios:** *Mejor si* hay equipos y escalas distintas. Para 2 usuarios es sobredimensionado.
>
> **Recomendación:** A. Con 2 usuarios y 0 €, un monolito te deja ver todas las piezas sin el ruido de coordinar servicios.
> **Cambiaría de opinión si** quisieras abrirla a miles de hogares.
>
> ¿Con cuál vamos?

Después seguiría con la siguiente decisión, y al final escribiría el documento de decisiones.

## Qué obtienes al final

Un `docs/DECISIONES.md` con: contexto, tabla del stack elegido y por qué, diagrama simple, cada decisión con sus alternativas y cuándo revisarla, coste mensual estimado, riesgos, siguientes pasos para construir y tres conceptos que merece la pena aprender para mantenerlo.

## Funciona mejor con graphify

Si el proyecto ya existe y es mediano o grande, la skill puede usar un grafo de [graphify](https://github.com/safishamsi/graphify) como mapa, en vez de releer todos los ficheros. Esto ahorra tokens y da una visión de conjunto.

```bash
graphify .    # genera graphify-out/ en el proyecto
```

La skill lo usa si existe y te ofrece crearlo si no. En proyectos pequeños no hace falta. El grafo no sustituye la lectura de la configuración de despliegue ni de los README: eso se lee aparte.

## Qué no hace

- **No escribe el código de la app.** Eso viene después, ya con las decisiones tomadas.
- **No decide por ti sin explicarte.** Si le pides que decida, lo hace razonado.
- **No garantiza precios ni límites de planes.** Cambian: la skill te avisa de verificarlos en la web del proveedor.
- **No es un juicio crítico con evidencias de código ajeno.** Para eso está `code-teardown`, que se complementa con ésta.

## Qué esperar de la conversación

Consume **más tokens y más turnos** que pedirle directamente la app: es a propósito. A cambio, cada decisión llega explicada y la puedes defender.

## Contenido de la carpeta

```
architecture-mentor/
  SKILL.md                    instrucciones y flujo de la skill
  references/
    decision-layers.md        cuestionario y criterios por capa
    catalog.md                catálogo de opciones por capa
    adr-template.md           plantilla del documento de decisiones
    review-mode.md            modo B: explicar un proyecto existente
    graphify.md               cómo usar un grafo como mapa
```

## Estado

v0.1. Probada a mano con un caso real (un módulo de tareas dentro de una app existente). Aún sin evals automáticos.

## Licencia

MIT, © Miguel Garcia Hermida.
