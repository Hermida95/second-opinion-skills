# Usar graphify como mapa (modo B y paso 0a)

[graphify](https://github.com/safishamsi/graphify) convierte un proyecto en un grafo de conocimiento persistente (`graphify-out/graph.json`, `GRAPH_REPORT.md`, `graph.html`). Esta skill lo usa como **mapa para no releer el proyecto entero**; el juicio de arquitectura sigue siendo suyo.

## Qué aporta y qué no

| El grafo sirve para | El grafo NO sustituye |
|---|---|
| Ver módulos, comunidades y dependencias de un vistazo | Config de infraestructura: `fly.toml`, `Dockerfile`, CI, variables de entorno |
| Localizar los «nodos dios» (donde todo converge) | El **porqué** de las decisiones (README, DEPLOY, ADRs, historial) |
| Seguir un camino concreto: `graphify path "A" "B"` | Costes, planes, límites del proveedor |
| Responder «¿qué toca esto?» sin abrir 40 ficheros | Una lectura puntual de los ficheros que vayas a citar |

Ahorra tokens sobre todo en proyectos medianos o grandes. En uno pequeño (decenas de ficheros) leerlo directamente puede salir igual de barato; no lo construyas solo por usarlo.

## Procedimiento

1. **¿Existe ya?** Busca `graphify-out/graph.json` en la raíz del proyecto.
   - Si existe: úsalo. Comprueba la fecha; si el código cambió mucho desde entonces, avisa de que puede estar desfasado y sugiere `graphify <ruta> --update`.
   - Si no existe y el proyecto es mediano o grande: **ofrécelo** (cuesta tokens la primera vez; luego es incremental y cacheado). No lo lances sin que el usuario lo acepte.
2. **Orientación (barato):** lee `GRAPH_REPORT.md`: comunidades, nodos dios, conexiones sorprendentes.
3. **Preguntas dirigidas:** `graphify query "<pregunta>"` (amplio), `--dfs` para trazar un camino, `graphify explain "<nodo>"`, `graphify path "A" "B"`.
4. **Radiografía por capas:** mapea comunidades del grafo a capas (API, datos, front, jobs, auth). Una comunidad sin etiqueta clara es una pista de falta de estructura, dilo.
5. **Confirma lo que vayas a afirmar:** abre el fichero concreto y cita `ruta:línea`. El grafo orienta; la cita prueba.
6. **Infra aparte:** lee a mano los ficheros de despliegue, que el grafo no modela bien.

## Honestidad
- Las aristas `INFERRED` y `AMBIGUOUS` son hipótesis: no las presentes como hechos.
- Un grafo de código sin docs describe la estructura, no la intención.
- Si el grafo y los ficheros discrepan, manda el fichero.
