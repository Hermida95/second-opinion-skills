# Cuestionario y criterios por capa

## Preguntas de entrada (elige las que cambien la decisión)
1. **Qué y para quién:** ¿qué problema resuelve y quién lo usa (solo tú, tu casa, clientes, público)?
2. **Escala:** ¿cuántos usuarios a un año? ¿picos? ¿datos sensibles (salud, pagos, menores)?
3. **Acceso:** ¿web, móvil, instalable (PWA), ¿offline?, ¿notificaciones?
4. **Dinero:** ¿presupuesto mensual máximo? ¿gratis a toda costa o se paga por comodidad?
5. **Tú:** ¿qué sabes ya? ¿Quieres aprender algo concreto con este proyecto? ¿Quién lo mantendrá?
6. **Tiempo y vida útil:** ¿prototipo de fin de semana o algo para años?

## Criterios que pesan en cada capa
- **Escala real, no imaginada.** La mayoría de proyectos personales caben en un monolito y una BD pequeña.
- **Coste total:** dinero + tiempo de mantenimiento + curva de aprendizaje.
- **Reversibilidad:** ¿cuánto cuesta cambiar de opinión? Prefiere decisiones fáciles de deshacer.
- **Un lenguaje o dos:** unificar front y back en un lenguaje reduce carga mental; separar solo si hay motivo (ecosistema, rendimiento, datos/IA).
- **Lock-in:** qué te ata a un proveedor y si importa.
- **Operación:** quién se despierta si falla, cómo se restaura un backup.

## Señales de sobredimensionamiento
Microservicios sin equipos separados; Kubernetes para una sola app; BD distribuida para menos de miles de filas; colas y cachés sin cuello de botella medido; varios entornos para un uso personal.
