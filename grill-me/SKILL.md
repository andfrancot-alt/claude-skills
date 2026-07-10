---
name: grill-me
description: Entrevista al usuario implacablemente sobre un plan o diseño hasta lograr un entendimiento compartido, resolviendo cada rama del árbol de decisiones. Úsala siempre que el usuario quiera someter a prueba de estrés un plan, validar un diseño o arquitectura antes de implementar, ser interrogado exhaustivamente sobre sus decisiones, o cuando diga "grill me", "interrógame", "cuestiona mi plan", "hazme de abogado del diablo" — incluso si no pide explícitamente una entrevista formal.
---

# Grill me

Interroga al usuario implacablemente sobre cada aspecto de su plan o diseño hasta alcanzar un entendimiento compartido. Recorre cada rama del árbol de decisiones, resolviendo las dependencias entre decisiones una por una. El objetivo no es ganar la discusión ni encontrar defectos por deporte: es que al final ambos puedan describir el plan igual, con sus riesgos y trade-offs sobre la mesa.

## Antes de preguntar

Si una pregunta puede responderse explorando la base de código, los documentos del proyecto o el historial de git, **explora en lugar de preguntar**. Cada pregunta cuyo respuesta ya existe en el repo desperdicia un turno del usuario y erosiona su confianza en la entrevista. Reserva las preguntas para lo que solo el usuario sabe: intención, restricciones externas, prioridades, apetito de riesgo.

Construye primero un mapa mental del plan: identifica las decisiones que lo componen y sus dependencias. Las decisiones fundacionales (de las que cuelgan otras) se interrogan primero; no tiene sentido debatir detalles de una rama que podría desaparecer con una decisión aguas arriba.

## Cómo entrevistar

- **Una línea de interrogatorio a la vez.** Haz una pregunta (o un grupo pequeño y coherente) y espera. No dispares diez preguntas en una lista; el usuario responderá superficialmente a todas en vez de profundamente a una.
- **Usa AskUserQuestion cuando las opciones sean enumerables** (¿A, B o C?); pregunta en texto libre cuando la respuesta sea abierta.
- **No aceptes respuestas vagas.** "Ya lo veremos", "no debería pasar", "es lo estándar" son señales para insistir: ¿qué pasa exactamente si ocurre? ¿estándar según quién? ¿qué alternativa descartaste y por qué?
- **Ataca los flancos clásicos**: casos límite, modos de fallo, concurrencia, migración de datos existentes, qué pasa al hacer rollback, costos operativos, qué se rompe si la suposición X resulta falsa, alternativas consideradas y descartadas.
- **Lleva registro de las ramas abiertas.** Cuando una respuesta abra dos hilos nuevos, sigue uno y anota el otro; no dejes ramas colgando sin resolver. Antes de cerrar, verifica que ninguna quedó pendiente.
- **Cede cuando corresponda.** Si el usuario defiende bien una decisión, reconócelo explícitamente y marca la rama como resuelta. Implacable no significa terco.

## Cómo terminar

La entrevista termina cuando no quedan ramas abiertas, no cuando se acaban las preguntas obvias. Al cerrar, entrega un resumen del entendimiento compartido:

1. **Decisiones acordadas** — cada una con su porqué en una línea.
2. **Riesgos aceptados** — lo que ambos saben que puede fallar y se decidió tolerar.
3. **Cambios respecto al plan original** — qué se modificó a raíz de la entrevista.
4. **Pendientes** — lo que quedó explícitamente fuera o para después.

Pide al usuario que confirme el resumen. Si corrige algo, esa corrección es una rama nueva: resuélvela antes de dar por terminada la sesión.
