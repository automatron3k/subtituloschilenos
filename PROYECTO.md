# subtituloschilenos.cl

Dominio comprado. Proyecto open source. Desarrollado con Claude (Opus 4.7+).

---

## Qué es

Plataforma open source que toma archivos de subtítulos existentes (en cualquier idioma) y los traduce al español chileno — no como traducción plana, sino como una versión con picardía, ironía, modismos, refranes, expresiones y memes característicos de la cultura popular chilena.

**El matiz es clave:** sutil, no exagerado. El objetivo es que el chileno sienta que alguien de aquí los escribió, no que alguien caricaturizó lo chileno.

---

## Por qué existe

Un proyecto que quise desarrollar. No hace daño a nadie. Puede crear unas cuantas sonrisas en el público que conoce el español chileno.

---

## Público objetivo

Chilenos que ya entienden el idioma original (o no), pero que quieren ver contenido con subtítulos que les resulten propios, chistosos, cercanos. La "humorada" es el producto, no la traducción.

---

## Ideas y funcionalidades

### Landing page
- Catálogo de subtítulos disponibles para descargar
  - Campo `explicit` por subtítulo: cuando está activo, garabatos-hard (cursing) son admitidos en la traducción
  - Búsqueda por URL de IMDb o Letterboxd — el sistema extrae título, año y datos de la película automáticamente
- Solicitar subtítulos para contenido no disponible
- Proponer correcciones a subtítulos existentes
- Calificar subtítulos existentes (sistema de rating)
- Botón "Rájate con un cafecito" (donaciones)

### Marca de agua en subtítulos generados
- En timestamp `00:00:00,000` se inserta línea fija:
  > Subtítulos desarrollados por subtituloschilenos.cl — correcciones en subtituloschilenos.cl o por WhatsApp al +56 X XXXX XXXX
- Sirve como atribución, canal de feedback y tracción orgánica

### UX canal WhatsApp
- Canal donde usuarios envían correcciones en tiempo real mientras ven una película o serie
- Reduce fricción: no hay que entrar a una web, simplemente mandas el mensaje mientras pausas
- Stack: Twilio para desarrollo/prototipo → migrar a Meta Cloud API cuando haya volumen

### Motor de traducción / "alma" del proyecto
- **Diccionario chileno**: modismos, garabatos soft, expresiones cotidianas
- **Garabatos hard**: separados, solo activos cuando subtítulo tiene flag `explicit`
- **Refranes típicos**: mapeo de equivalencias culturales (ej. proverbio inglés → refrán chileno equivalente)
- **Memes y referencias pop chilenas**: actualizables por la comunidad
- Claude como motor principal de traducción + interpretación cultural
- El prompt/instrucción base define el tono: *sutil, pícaro, con ironía chilena — jamás caricatura*

### Diccionario — versionamiento y aportes

Estructura en GitHub:
```
diccionario/
  modismos.json
  garabatos-soft.json
  garabatos-hard.json
  refranes.json
  memes-pop.json
  CONTRIBUTING.md
```

Flujo de aportes (desde landing o WhatsApp):
```
Propuesta entrante
  → Claude revisa:
      - ¿Ya existe entrada similar? → sugiere modificar en vez de duplicar
      - ¿Definición aporta algo nuevo? → mide delta semántico
      - ¿Calidad mínima? → rechaza o pide más contexto
  → Si pasa → PR automático al repo
  → Si duda → flag + cola humana
  → Maintainer mergea / cierra con feedback
```

Comunidad también puede hacer PRs directos a GitHub.

### Moderación de aportes comunitarios
- **Primer filtro:** Claude revisa calidad, duplicados, contenido ofensivo real, spam
- **Segundo filtro (humano):** solo cuando Claude detecta ambigüedad o alarma
- Humanos solo ven casos difíciles — Claude maneja el volumen

### Comunidad y revisión humana
- Usuarios autenticados con sistema de puntuaciones / reputación
- Revisiones humanas de subtítulos generados por IA
- Sistema de benchmarks para calidad de traducción
- PR e Issues en GitHub para aportes al algoritmo, al diccionario y al código

### Kickoff — distribución masiva inicial

Una vez probado el modelo en 5–10 películas o episodios reales con feedback validado:

1. Tomar los **150 filmes mejor puntuados en IMDb**
2. Tomar los **300 episodios mejor puntuados en IMDb**
3. Generar todas las traducciones al español chileno
4. Distribuirlas en los principales motores de búsqueda de subtítulos (OpenSubtitles, Subdivx, etc.)

Objetivo: presencia masiva desde el día uno del lanzamiento público. Que alguien que busca subtítulos de cualquier clásico ya encuentre la versión chilena disponible.

### Open source
- Repositorio GitHub con README explicando:
  - Génesis del proyecto
  - Qué busca
  - Cómo funciona
  - Cómo contribuir
- Skills/prompts de traducción publicados para que la comunidad proponga mejoras
- Instrucciones para que otros devs puedan levantar su propia instancia

---

## Stack

| Componente | Tecnología |
|------------|-----------|
| Servidor | VM Hetzner |
| Base de datos / Auth / Storage | Supabase (self-hosted en Hetzner) |
| Motor IA | Claude Opus 4.7+ vía API |
| Traducción / skills | Claude Code con skills de traducción e interpretación cultural |
| Frontend | SvelteKit |
| Canal WhatsApp | Twilio (prototipo) → Meta Cloud API (producción) |
| Repositorio | GitHub (público, open source) |
| Diccionario | GitHub repo versionado, contribuible vía PR |

---

## Formatos de subtítulos soportados

| Formato | Prioridad | Notas |
|---------|-----------|-------|
| `.srt` | Obligatorio — Fase 1 | Universal, todos los players |
| `.vtt` | Obligatorio — Fase 1 | Estándar web HTML5 |
| `.ass` / `.ssa` | Fase 2 | Estilos, colores, karaoke |
| `.sub` | Opcional | MicroDVD, legacy |

---

## Principios de diseño del tono

1. **Sutil primero** — si hay duda entre neutro y chilenismo, elegir sutil
2. **Nunca caricatura** — exagerar destruye el efecto; la gracia está en que suene natural
3. **Ironía > traducción literal** — buscar el equivalente cultural, no la palabra
4. **Actualizable** — el habla chilena evoluciona; el diccionario debe poder actualizarse sin tocar código
5. **Explicit es opt-in** — garabatos hard solo cuando el creador/uploader lo marca explícitamente

---

## Derechos de autor — política

- Plataforma **no almacena ni redistribuye** el `.srt` original
- Usuario sube archivo → se procesa → se entrega versión chilena → original descartado
- ToS incluye declaración: usuario confirma que tiene derecho de usar el archivo que sube
- Subtítulos generados (versión chilena) son obra derivada del proyecto

---

## Licencias

| Componente | Licencia |
|-----------|----------|
| Código fuente | MIT |
| Diccionario (compilación + definiciones) | CC BY-SA 4.0 |

Las expresiones populares chilenas son dominio cultural público — no son propiedad del proyecto. Lo que se licencia es la compilación, estructura editorial y definiciones redactadas.

---

## Preguntas abiertas

- ¿Número de WhatsApp definitivo para el canal?
- ¿Modelo de puntuaciones/reputación para usuarios contribuidores?
- ¿Cómo manejar subtítulos con múltiples versiones (distintos aportes) de la misma película?
- ¿Proceso de verificación de identidad para moderadores humanos?

---

## Log de decisiones

| Fecha | Decisión | Razón |
|-------|----------|-------|
| 2026-05-21 | Compra dominio subtituloschilenos.cl | Asegurar nombre antes de arrancar |
| 2026-05-21 | Stack base: Hetzner + Supabase + Claude API | Consistente con otros proyectos del usuario; control total |
| 2026-05-21 | Tono: sutil + pícaro, jamás caricatura | Exceso destruye el producto; el público detecta la diferencia |
| 2026-05-21 | Frontend: SvelteKit | Bundle pequeño, animaciones nativas, buen fit con Supabase, bajo costo de aprendizaje |
| 2026-05-21 | WhatsApp: Twilio → Meta Cloud API | Twilio para prototipo rápido, migrar a Meta directo en producción |
| 2026-05-21 | Formatos Fase 1: SRT + VTT | Cubre 95% de casos; ASS queda para Fase 2 |
| 2026-05-21 | Política derechos autor: no almacenar original | Reduce riesgo legal; usuario declara derechos en ToS |
| 2026-05-21 | Moderación: IA primero, humano solo si alarma | Escala con volumen; humanos solo ven casos difíciles |
| 2026-05-21 | Diccionario: GitHub + PR automático vía IA | Versionado, contribuible, revisión IA reduce carga manual |
| 2026-05-21 | Licencias: MIT (código) + CC BY-SA 4.0 (diccionario) | MIT maximiza adopción; CC BY-SA protege compilación sin poseer habla popular |
| 2026-05-21 | Campo `explicit` en catálogo | Garabatos hard opt-in; protege a usuarios que no quieren ese tono |
| 2026-05-21 | Búsqueda por URL IMDb / Letterboxd | Reduce fricción al buscar — no hay que saber el título exacto |
| 2026-05-21 | Marca de agua en timestamp 00:00 | Atribución + canal de feedback + tracción orgánica |
