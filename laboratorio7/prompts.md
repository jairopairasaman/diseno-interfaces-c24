# Biblioteca de prompts — Laboratorio 07
## Tarea N — [Nombre de la tarea]
**Herramienta:** Claude / ChatGPT / Gemini / Copilot
### Versión A — Sin ejemplos (zero-shot)
| Issue | Tipo | Prioridad | Módulo |
|---|---|---|---|
| 1. "Al pagar con tarjeta aparece error 500 y el pedido queda duplicado." | Bug / Critical Bug | Alta / Crítica | Pagos / Checkout |
| 2. "Agregar modo oscuro en la pantalla de perfil." | Feature / Enhancement | Baja / Media | Perfil / UI |
| 3. "¿El endpoint /api/pedidos acepta paginación?" | Question / Support | Baja | API / Pedidos |
| 4. "El login tarda 8 segundos cuando hay más de 100 usuarios conectados." | Performance / Bug | Alta | Autenticación / Login |
| 5. "Actualizar la librería axios por una alerta de seguridad." | Security / Maintenance | Alta / Crítica | Dependencias / Seguridad |

**Prompt:**
> (pegar aquí el prompt utilizado)
Clasifica cada issue de GitHub indicando su tipo, prioridad y módulo.
1. "Al pagar con tarjeta aparece error 500 y el pedido queda duplicado."
2. "Agregar modo oscuro en la pantalla de perfil."
3. "¿El endpoint /api/pedidos acepta paginación?"
4. "El login tarda 8 segundos cuando hay más de 100 usuarios conectados."
5. "Actualizar la librería axios por una alerta de seguridad."

**Resultado (resumen):** ...
### Versión B — Few-shot (3 ejemplos)

Issue: "Al pagar con tarjeta aparece error 500 y el pedido queda duplicado."
Tipo: BUG | Prioridad: ALTA | Módulo: pagos

Issue: "Agregar modo oscuro en la pantalla de perfil."
Tipo: FEATURE | Prioridad: BAJA | Módulo: perfil

Issue: "¿El endpoint /api/pedidos acepta paginación?"
Tipo: CONSULTA | Prioridad: BAJA | Módulo: pedidos

Issue: "El login tarda 8 segundos cuando hay más de 100 usuarios conectados."
Tipo: RENDIMIENTO | Prioridad: MEDIA | Módulo: autenticación

Issue: "Actualizar la librería axios por una alerta de seguridad."
Tipo: SEGURIDAD | Prioridad: ALTA | Módulo: dependencias

**Prompt:**
> (pegar aquí el prompt utilizado)

# Instrucción
Clasifica cada issue siguiendo exactamente el formato de los ejemplos.
Tipos válidos: BUG, FEATURE, CONSULTA, RENDIMIENTO, SEGURIDAD.
Prioridad: ALTA (afecta dinero, datos o seguridad), MEDIA o BAJA.

# Ejemplos
Issue: "La app se cierra al subir una foto de perfil."
Tipo: BUG | Prioridad: MEDIA | Módulo: perfil

Issue: "Permitir exportar el historial de pedidos a Excel."
Tipo: FEATURE | Prioridad: BAJA | Módulo: pedidos

Issue: "Las contraseñas se guardan en texto plano en la tabla usuarios."
Tipo: SEGURIDAD | Prioridad: ALTA | Módulo: autenticación

# Issues a clasificar
1. "Al pagar con tarjeta aparece error 500 y el pedido queda duplicado."
2. "Agregar modo oscuro en la pantalla de perfil."
3. "¿El endpoint /api/pedidos acepta paginación?"
4. "El login tarda 8 segundos cuando hay más de 100 usuarios conectados."
5. "Actualizar la librería axios por una alerta de seguridad."

**Resultado (resumen):** ...
**Mejora observada:** ...

# Instrucción
Resuelve el problema razonando ronda por ronda, igual que en los ejemplos.
# Ejemplo 1
Servicios: A, B. B depende de A.
Razonamiento: Ronda 1: A (sin dependencias). Ronda 2: B (A ya está desplegado).
Respuesta: 2 rondas.

3

# Ejemplo 2
Servicios: A, B, C. C depende de A y B.
Razonamiento: Ronda 1: A y B en paralelo. Ronda 2: C.
Respuesta: 2 rondas.

Razonamiento:

Ronda 1: auth y catalogo en paralelo (no tienen dependencias).

Ronda 2: usuarios (auth ya está desplegado).

Ronda 3: pagos (usuarios ya está desplegado).

Ronda 4: pedidos (usuarios, pagos y catalogo ya están desplegados).

Ronda 5: notificaciones (pedidos ya está desplegado).

Ronda 6: gateway (auth y notificaciones ya están desplegados).

Respuesta: 6 rondas.

# Ejemplo 3
Servicios: A, B, C, D. B y C dependen de A. D depende de B y C.
Razonamiento: Ronda 1: A. Ronda 2: B y C en paralelo. Ronda 3: D.
Respuesta: 3 rondas.
# Problema
(pegar aquí el problema del paso 2.1 sin la frase "Responde solo con el número")

---

## Tarea 3: Extracción estructurada

**Herramienta:** ChatGPT / Gemini / Claude

### Versión A — Sin ejemplos (zero-shot)
**Prompt:**
> Extrae los datos importantes de estos reportes de error en formato JSON.
> Reporte 1: "Desde ayer, en la versión 2.3.1 de Android, cuando un cliente aplica el cupón BIENVENIDA20 el total no se actualiza. Lo reportó Ana Díaz de soporte."
> Reporte 2: "En la web el botón Descargar factura no hace nada y no muestra ningún error. Reportado por Luis Paredes el 3 de octubre."

**Resultado (resumen):**
(pegar aquí el JSON que te devolvió la IA)

[
  {
    "reporte_id": 1,
    "plataforma": "Android",
    "version": "2.3.1",
    "fecha_inicio_incidencia": "Ayer",
    "descripcion_error": "Al aplicar el cupón BIENVENIDA20, el monto total no se actualiza",
    "reportado_por": "Ana Díaz (Soporte)"
  },
  {
    "reporte_id": 2,
    "plataforma": "Web",
    "version": null,
    "fecha_reporte": "3 de octubre",
    "descripcion_error": "El botón 'Descargar factura' no realiza ninguna acción ni muestra mensajes de error",
    "reportado_por": "Luis Paredes"
  }
]

---

## Tarea 4: Revisión de código (Role prompting y XML)

**Herramienta:** ChatGPT / Gemini / Claude

### Versión A — Sin rol ni estructura
**Prompt:**
> Revisa este código:
> def login(usuario, clave):
>     query = "SELECT * FROM usuarios WHERE nombre='" + usuario + "' AND clave='" + clave + "'"
>     return db.execute(query).fetchone() is not None

**Resultado (resumen):**
El asistente identificó una vulnerabilidad de Inyección SQL por concatenar variables en la consulta y recomendó usar consultas preparadas.

### Versión B — Con rol y prompt estructurado en XML
**Prompt:**
> <rol>
> Eres un revisor de seguridad de aplicaciones web con experiencia en OWASP Top 10.
> </rol>
> <contexto>
> Función de login de una API en Python con SQLite. El equipo de desarrollo es junior.
> </contexto>
> <codigo>
> def login(usuario, clave):
>     query = "SELECT * FROM usuarios WHERE nombre='" + usuario + "' AND clave='" + clave + "'"
>     return db.execute(query).fetchone() is not None
> </codigo>
> <tarea>
> 1. Identifica las vulnerabilidades y explica el riesgo de cada una.
> 2. Propón el código corregido usando consultas parametrizadas.
> </tarea>
> <formato>
> Tabla Markdown: Vulnerabilidad | Riesgo | Corrección. Luego, el código corregido.
> </formato>

**Resultado (resumen):**

| Vulnerabilidad | Riesgo | Corrección |
| --- | --- | --- |
| Inyección SQL (OWASP A03:2021) | Permite autenticarse sin credenciales e inyectar código destructivo. | Utilizar placeholders `?` para parametrizar la consulta. |
| Contraseñas en texto plano | Exposición masiva de credenciales ante brechas de seguridad. | Almacenar y comparar hashes usando librerías como `bcrypt`. |

```python
def login(usuario, clave):
    query = "SELECT clave_hash FROM usuarios WHERE nombre = ?"
    user = db.execute(query, (usuario,)).fetchone()
    if user and verificar_hash(clave, user['clave_hash']):
        return True
    return False

    ## 📍 FASE 5 — Evaluación comparativa

### ¿Qué hacer?
Abre **VS Code** y copia/pega exactamente este bloque al final de tu archivo `prompts.md`:

```markdown
---

## FASE 5 — Evaluación comparativa

### Paso 5.1 — Rúbrica de evaluación
| Criterio     | Descripción                                    | Puntaje (1-5) |
| ------------ | ---------------------------------------------- | :-----------: |
| Exactitud    | La respuesta es correcta (verificada por ti)   |       5       |
| Formato      | Respeta el formato o esquema solicitado        |       5       |
| Consistencia | Aplica el mismo criterio en todos los casos    |       5       |
| Utilidad     | Se puede usar directamente en el proyecto      |       5       |

### Paso 5.2 — Comparación: sin ejemplos vs. técnica avanzada
| Tarea                       | Versión A | Versión B | Mejora principal |
| --------------------------- | :-------: | :-------: | ---------------- |
| 1. Clasificación de issues  |   13/20   |   20/20   | Respetó estrictamente las categorías permitidas y el formato de una sola línea. |
| 2. Razonamiento lógico      |   12/20   |   20/20   | Desglosó el razonamiento por rondas permitiendo detectar dependencias correctamente. |
| 3. Extracción estructurada  |   14/20   |   20/20   | Mantuvo un esquema JSON estricto utilizando `null` para los datos faltantes. |
| 4. Revisión de código (rol) |   15/20   |   20/20   | Estructuró el informe bajo OWASP Top 10 en formato de tabla con solución parametrizada. |

## Plantilla: Clasificación few-shot

```text
Actúa como {{rol}}.
Clasifica cada {{elemento}} siguiendo el formato de los ejemplos.
Categorías válidas: {{categorias}}.


Ejemplo 1: {{entrada_1}} → {{salida_1}}
Ejemplo 2: {{entrada_2}} → {{salida_2}}
Ejemplo 3: {{entrada_3}} → {{salida_3}}


Elementos a clasificar: {{datos}}
```
