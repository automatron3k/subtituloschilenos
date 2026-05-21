# subtituloschilenos.cl

> Creado por un weón viviendo afuera.

**Subtítulos chilenos**

> Proyecto open source. Desarrollado con Claude Opus 4.7+.

---

## ¿Qué es esto?

Una plataforma que toma subtítulos existentes (en cualquier idioma) y los traduce al español chileno — no como traducción plana, sino con modismos, refranes, referencias culturales y la ironía característica del habla popular de Chile.

**El matiz lo es todo:** sutil, no exagerado. El objetivo es que el chileno sienta que alguien de aquí los escribió — no que alguien caricaturizó lo chileno.

---

## Por qué existe

Un proyecto que quise hacer. No hace daño a nadie. Puede crear unas cuantas sonrisas en el público que conoce el español chileno.

---

## Cómo funciona

```
Archivo de subtítulos (.srt / .vtt)
    ↓
Claude Opus 4.7+ (motor de traducción)
    ↓
Diccionario chileno (modismos, refranes, memes pop)
    ↓
Subtítulo en español chileno
    ↓
Revisión comunitaria + feedback WhatsApp
```

1. Subes (o buscas por URL de IMDb / Letterboxd) el subtítulo fuente
2. Claude lo traduce usando el diccionario chileno + criterios de tono
3. El resultado llega con una línea de atribución en el timestamp `00:00`
4. La comunidad propone correcciones vía web o WhatsApp

---

## Principios de tono

1. **Sutil primero** — si hay duda entre neutro y chilenismo, se elige sutil
2. **Nunca caricatura** — exagerar destruye el efecto; la gracia está en que suene natural
3. **Ironía > traducción literal** — equivalente cultural, no la palabra
4. **Actualizable** — el habla evoluciona; el diccionario se puede contribuir sin tocar código

---

## Stack


| Componente                     | Tecnología                              |
| ------------------------------ | --------------------------------------- |
| Servidor                       | VM Hetzner                              |
| Base de datos / Auth / Storage | Supabase (self-hosted)                  |
| Motor IA                       | Claude Opus 4.7+ vía API                |
| Frontend                       | SvelteKit                               |
| Canal WhatsApp                 | Twilio → Meta Cloud API                 |
| Diccionario                    | Este mismo repositorio (`/diccionario`) |


---

## Estructura del repositorio

```
subtituloschilenos/
├── diccionario/
│   ├── modismos.json          # Expresiones y modismos cotidianos
│   ├── garabatos-soft.json    # Garabatos suaves (siempre activos)
│   ├── garabatos-hard.json    # Garabatos fuertes (solo modo explicit)
│   ├── refranes.json          # Equivalencias culturales de refranes
│   ├── memes-pop.json         # Referencias pop chilenas actualizables
│   └── CONTRIBUTING.md        # Cómo contribuir al diccionario
├── prompts/
│   └── traduccion-base.md     # Instrucción base del motor de traducción
├── README.md
└── PROYECTO.md                # Documento interno de diseño del proyecto
```

---

## Cómo contribuir

### Al diccionario

El diccionario chileno es el corazón del proyecto y es completamente contribuible.

**Desde GitHub (modo dev):**

1. Fork del repositorio
2. Edita el JSON correspondiente en `/diccionario`
3. Abre un Pull Request con descripción del aporte

**Desde la plataforma (modo usuario):**

- Formulario en subtituloschilenos.cl
- Mensaje al canal WhatsApp

Todo aporte pasa primero por revisión de IA (detecta duplicados, evalúa calidad) y luego, si hay dudas, por revisión humana de los maintainers.

### Al código

- Issues en GitHub para reportar bugs o proponer funcionalidades
- PRs bienvenidos — revisar `CONTRIBUTING.md` antes

### A los subtítulos

- Propón correcciones en la plataforma o por WhatsApp mientras ves la película
- Rating y comentarios en el catálogo

---

## Catálogo y modo explicit

Cada subtítulo en el catálogo tiene un flag `explicit`. Cuando está activo, la traducción incluye garabatos fuertes (`garabatos-hard.json`). Cuando está desactivado, solo se usan garabatos suaves o ninguno.

El creador del subtítulo define este flag al subirlo.

---

## Derechos de autor

- La plataforma **no almacena ni redistribuye** subtítulos originales
- El usuario que sube un archivo declara en los ToS que tiene derecho a usarlo
- Los subtítulos generados (versión chilena) son obra derivada del proyecto

---

## Licencias


| Componente                   | Licencia                            |
| ---------------------------- | ----------------------------------- |
| Código fuente                | [MIT](LICENSE)                      |
| Diccionario (`/diccionario`) | [CC BY-SA 4.0](diccionario/LICENSE) |


Las expresiones populares chilenas son dominio cultural público. Lo que se licencia bajo CC BY-SA 4.0 es la compilación, la estructura editorial y las definiciones redactadas por el proyecto y la comunidad.

---

## Estado del proyecto

🚧 En desarrollo activo. Primera versión pública en construcción.

---

## Donaciones

Si te sirve y quieres apoyar: **"Rájate con un cafecito"** ☕  
*(link próximamente)*