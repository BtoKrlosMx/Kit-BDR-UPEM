# Guías de Laboratorio — Sesión a sesión (Miércoles)
**Bases de Datos Relacionales (IS0737) · UPEM · Periodo 27/1**

> Cada guía está pensada para las 3 horas de laboratorio. Antes de empezar, verifica que XAMPP (Apache + MySQL) esté en verde y que tu conexión en MySQL Workbench abra sin errores (ver *Guía de instalación XAMPP y MySQL Workbench*).

---

## Sesión 1 — 09-sep — Instalación y arranque del entorno
**Objetivo:** dejar listo el entorno de trabajo del semestre.
**Herramientas:** XAMPP, MySQL Workbench, GitHub.

**Pasos:**
1. Sigue completa la **Guía de instalación de XAMPP y MySQL Workbench**.
2. Sigue las secciones 1 y 2 de la **Guía de uso de GitHub**: crea tu cuenta y tu repositorio del proyecto.
3. Verifica tu instalación con el script de prueba de la guía de instalación.
4. Sube la evidencia (captura de pantalla) y la liga de tu repositorio en la tarea correspondiente de Classroom.

**Entregable:** cuenta de GitHub + repositorio creado + evidencia de instalación funcionando.

---

## Sesión 3 — 23-sep — Primeras sentencias DDL
**Objetivo:** crear tu primera base de datos y tablas relacionadas en MySQL Workbench.
**Herramientas:** MySQL Workbench.

**Pasos:**
1. Abre tu conexión en MySQL Workbench.
2. Crea una base de datos de práctica:
   ```sql
   CREATE DATABASE practica_ddl;
   USE practica_ddl;
   ```
3. Crea al menos dos tablas relacionadas, por ejemplo:
   ```sql
   CREATE TABLE cliente (
       id_cliente INT PRIMARY KEY AUTO_INCREMENT,
       nombre VARCHAR(100) NOT NULL,
       correo VARCHAR(100)
   );

   CREATE TABLE pedido (
       id_pedido INT PRIMARY KEY AUTO_INCREMENT,
       fecha DATE,
       id_cliente INT,
       FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente)
   );
   ```
4. Ejecuta el script completo (ícono de rayo ⚡ o `Ctrl+Shift+Enter`) y confirma que no haya errores en el panel inferior.
5. Verifica en el panel **Schemas** (lado izquierdo) que aparezcan tus tablas; da clic derecho → **Refresh All** si no las ves.
6. Guarda tu script como `ejercicio1_ddl.sql`.

**Entregable:** script `.sql` con `CREATE DATABASE`/`CREATE TABLE` de tu propio caso (Ejercicio práctico #1) — súbelo también a la carpeta `/scripts` de tu repositorio.

---

## Sesión 4 — 30-sep — Modelado EER del proyecto
**Objetivo:** bosquejar el diagrama Entidad-Relación de tu proyecto en MySQL Workbench.
**Herramientas:** MySQL Workbench (módulo EER).

**Pasos:**
1. Menú **File → New Model**.
2. En el modelo nuevo, da doble clic en **Add Diagram**.
3. En la barra de herramientas izquierda del diagrama, usa el ícono de tabla para agregar cada entidad de tu proyecto (mínimo 4).
4. Doble clic sobre cada tabla para nombrarla y agregar sus columnas (nombre, tipo de dato, si es llave primaria marcando la casilla **PK**).
5. Usa el ícono de relación "1-n identifying/non-identifying" para conectar las tablas que se relacionan entre sí, arrastrando de una tabla a otra.
6. Guarda el modelo: **File → Save Model As** → `proyecto_[tu-nombre].mwb`.
7. Exporta una imagen: **File → Export → Export as PNG**.

**Entregable:** archivo `.mwb` o imagen del diagrama EER preliminar de tu proyecto (Avance de proyecto 2), subido a la carpeta `/diagramas` de tu repositorio.

---

## Sesión 5 — 07-oct — Repaso general y práctica calificada (previo al 1er parcial)
**Objetivo:** consolidar lo visto en la Unidad 1 antes del examen.
**Herramientas:** MySQL Workbench.

**Pasos:**
1. El docente entregará un caso nuevo (enunciado breve).
2. Diseña y ejecuta el script DDL completo para ese caso: base de datos, mínimo 3 tablas, llaves primarias y al menos una llave foránea.
3. Ejecuta el script sin errores y muestra el resultado en el panel de **Schemas**.
4. Esta práctica se califica como evidencia de desempeño en laboratorio, y sirve como repaso directo para el examen del viernes.

**Entregable:** script `.sql` de la práctica calificada.

---

## Sesión 6 — 14-oct — Llaves primarias y foráneas del proyecto
**Objetivo:** formalizar las llaves de tu modelo EER.
**Herramientas:** MySQL Workbench (módulo EER).

**Pasos:**
1. Antes de iniciar, responde el examen diagnóstico (sin valor) que se indique en Classroom.
2. Abre tu archivo `.mwb` del proyecto.
3. Para cada tabla, verifica/asigna su llave primaria (columna con casilla **PK** marcada).
4. Revisa cada relación: da doble clic sobre la línea de relación y confirma que la llave foránea se haya generado correctamente en la tabla "hija" (pestaña **Foreign Keys** del editor de tabla).
5. Si falta alguna relación entre entidades de tu proyecto, agrégala con el ícono de relación correspondiente (1:1, 1:N o N:M — para N:M se requiere una tabla intermedia).
6. Guarda tu modelo actualizado.

**Entregable:** modelo EER actualizado con llaves primarias/foráneas (Avance de proyecto 3).

---

## Sesión 7 — 21-oct — De diagrama E-R a tablas relacionales
**Objetivo:** generar el script SQL a partir de tu diagrama EER.
**Herramientas:** MySQL Workbench (Forward Engineer).

**Pasos:**
1. Con tu modelo `.mwb` abierto, ve a **Database → Forward Engineer...**.
2. Sigue el asistente: selecciona tu conexión, deja las opciones por defecto y avanza (**Next**) hasta la pantalla de revisión del script SQL generado.
3. Revisa el script generado (`CREATE TABLE` con sus llaves) antes de ejecutarlo.
4. Da clic en **Execute** para crear las tablas directamente en tu base de datos.
5. Verifica en el panel **Schemas** que las tablas se hayan creado correctamente.
6. Guarda también una copia del script generado: en la ventana de revisión hay un botón para guardarlo como `.sql`.

**Entregable:** script SQL resultante de la reducción de tu diagrama E-R a tablas (Avance de proyecto 4).

---

## Sesión 8 — 28-oct — Generalización/especialización
**Objetivo:** representar en tu modelo un caso de generalización, si tu proyecto lo requiere.
**Herramientas:** MySQL Workbench.

**Pasos:**
1. Identifica si en tu proyecto existe una entidad con "subtipos" (ejemplo: `Empleado` que puede ser `Administrativo` o `Docente`, cada uno con atributos propios).
2. Modélalo con una de estas dos estrategias:
   - **Tabla única con discriminador:** una tabla `empleado` con una columna `tipo` y columnas opcionales para los atributos específicos.
   - **Tablas separadas (recomendado si los atributos difieren mucho):** una tabla `empleado` con los atributos comunes, y tablas `administrativo`/`docente` con llave foránea hacia `empleado` (relación 1:1).
3. Actualiza tu diagrama EER con la estrategia elegida.
4. Vuelve a generar el script SQL (Forward Engineer) o ajusta manualmente las tablas afectadas.

**Entregable:** modelo EER actualizado con la generalización/especialización aplicada (Avance de proyecto 5).

---

## Sesión 9 — 04-nov — Poblar tablas y primeras consultas
**Objetivo:** insertar datos de prueba y practicar `SELECT`.
**Herramientas:** MySQL Workbench.

**Pasos:**
1. Para cada tabla de tu proyecto, inserta al menos 5 registros de prueba:
   ```sql
   INSERT INTO cliente (nombre, correo) VALUES
   ('Ana López', 'ana@correo.com'),
   ('Luis Pérez', 'luis@correo.com');
   ```
2. Ejecuta consultas simples para verificar los datos:
   ```sql
   SELECT * FROM cliente;
   SELECT nombre FROM cliente WHERE correo LIKE '%correo.com%';
   ```
3. Practica con `ORDER BY` y `LIMIT`:
   ```sql
   SELECT * FROM cliente ORDER BY nombre ASC LIMIT 5;
   ```

**Entregable:** script con los `INSERT` de tus tablas y al menos 3 consultas `SELECT` ejecutadas (Avance de proyecto 6).

---

## Sesión 10 — 11-nov — Repaso general y práctica calificada (previo al 2do parcial)
**Objetivo:** repasar Unidad 2 y 3.1 antes del examen.
**Herramientas:** MySQL Workbench.

**Pasos:**
1. El docente entrega un esquema de práctica.
2. Resuelve las consultas `SELECT` solicitadas (filtros, orden, límite).
3. Ejecuta y verifica los resultados en el panel inferior de Workbench.

**Entregable:** script de la práctica calificada.

---

## Sesión 11 — 18-nov — Álgebra relacional en SQL
**Objetivo:** traducir operaciones de álgebra relacional a consultas SQL.
**Herramientas:** MySQL Workbench.

**Pasos:**
1. Antes de iniciar, responde el examen diagnóstico (sin valor) indicado en Classroom.
2. Practica el equivalente SQL de las operaciones de álgebra relacional sobre tu proyecto:
   - **Selección (σ):**
     ```sql
     SELECT * FROM pedido WHERE fecha > '2026-01-01';
     ```
   - **Proyección (π):**
     ```sql
     SELECT nombre, correo FROM cliente;
     ```
   - **Join (⋈):**
     ```sql
     SELECT c.nombre, p.fecha
     FROM cliente c
     JOIN pedido p ON c.id_cliente = p.id_cliente;
     ```
   - **Unión (∪):** (requiere tablas con mismas columnas)
     ```sql
     SELECT nombre FROM cliente
     UNION
     SELECT nombre FROM proveedor;
     ```
3. Documenta al menos 3 operaciones distintas aplicadas a tu propio proyecto.

**Entregable:** script con las consultas de álgebra relacional traducidas a SQL, usando `JOIN`/`UNION` sobre tu proyecto (Avance de proyecto 7).

---

## Sesión 12 — 25-nov — Vistas y modificación de datos
**Objetivo:** crear una vista útil para tu proyecto y practicar `UPDATE`/`DELETE`.
**Herramientas:** MySQL Workbench.

**Pasos:**
1. Crea una vista que resuma información frecuente de consultar, por ejemplo:
   ```sql
   CREATE VIEW vista_pedidos_cliente AS
   SELECT c.nombre, p.id_pedido, p.fecha
   FROM cliente c
   JOIN pedido p ON c.id_cliente = p.id_cliente;
   ```
2. Consulta la vista como si fuera una tabla:
   ```sql
   SELECT * FROM vista_pedidos_cliente;
   ```
3. Practica una actualización controlada:
   ```sql
   UPDATE cliente SET correo = 'nuevo_correo@correo.com' WHERE id_cliente = 1;
   ```
4. Practica una eliminación controlada (siempre con `WHERE`, nunca sin filtro):
   ```sql
   DELETE FROM pedido WHERE id_pedido = 10;
   ```

**Entregable:** al menos una vista creada sobre tu proyecto, y una consulta `UPDATE`/`DELETE` justificada (Avance de proyecto 8).

---

## Sesión 13 — 02-dic — Dependencias funcionales
**Objetivo:** identificar las dependencias funcionales del esquema de tu proyecto.
**Herramientas:** documento de análisis (puede ser Word/Excel), apoyándote en tu script SQL.

**Pasos:**
1. Para cada tabla de tu proyecto, lista todas sus columnas.
2. Escribe las dependencias funcionales en notación `X → Y` (X determina a Y). Ejemplo: `id_cliente → nombre, correo`.
3. Clasifica cada dependencia como trivial (Y es subconjunto de X) o no trivial.
4. Verifica que no haya dependencias no deseadas (por ejemplo, un atributo no llave que determine a otro no llave — señal de que falta normalizar).

**Entregable:** documento con el listado de dependencias funcionales de tu proyecto (Avance de proyecto 9).

---

## Sesión 14 — 09-dic — Normalización hasta 3FN/BCNF
**Objetivo:** aplicar el proceso de normalización a tu esquema.
**Herramientas:** MySQL Workbench + tu documento de dependencias funcionales.

**Pasos:**
1. Revisa cada tabla contra 1FN (valores atómicos, sin grupos repetitivos).
2. Revisa 2FN (sin dependencias parciales de la llave primaria compuesta, si aplica).
3. Revisa 3FN (sin dependencias transitivas: un atributo no llave que dependa de otro atributo no llave).
4. Si detectas una violación, descompón la tabla en dos, moviendo el atributo problemático a una nueva tabla con su propia llave y una llave foránea de regreso.
5. Ajusta tu script SQL con las tablas ya normalizadas:
   ```sql
   ALTER TABLE pedido DROP COLUMN nombre_cliente; -- ejemplo de columna redundante eliminada
   ```
6. Verifica que las consultas que ya tenías (vistas, joins) sigan funcionando; ajusta si es necesario.

**Entregable:** esquema normalizado (documentando el proceso) y script SQL actualizado (Avance de proyecto 10).

---

## Sesión 15 — 06-ene — Repaso general y entrega final
**Objetivo:** integrar y cerrar el proyecto del semestre.
**Herramientas:** MySQL Workbench, GitHub.

**Pasos:**
1. Verifica que tu script SQL final incluya: creación de base de datos, todas las tablas normalizadas con llaves, datos de prueba (`INSERT`), al menos una vista y consultas relevantes.
2. Ejecuta el script completo desde cero en una base de datos nueva para confirmar que no tiene errores (`DROP DATABASE` + volver a crear, si es necesario probarlo limpio).
3. Sube a tu repositorio de GitHub: el diagrama E-R final, el script `.sql` completo, y un documento breve (1–2 páginas) que describa tu proyecto.
4. Resuelve la práctica calificada final que te indique el docente (repaso general de consultas).
5. Verifica que la liga de tu repositorio esté correctamente publicada en la tarea "Entrega final de proyecto" de Classroom.

**Entregable:** proyecto integrador completo (entrega final) + práctica calificada final de laboratorio.

---

## Recordatorios generales para todas las sesiones
- Guarda tu progreso constantemente (`Ctrl+S` en Workbench).
- Haz un commit en GitHub al final de cada sesión, aunque el avance sea pequeño.
- Si tu script marca error, lee el mensaje en el panel inferior de Workbench: casi siempre indica la línea exacta del problema.
- Ante cualquier duda técnica, pregunta durante la sesión: las prácticas de laboratorio se califican también por participación.
