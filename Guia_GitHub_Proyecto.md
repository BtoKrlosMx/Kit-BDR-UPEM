# Guía de uso de GitHub para el proyecto integrador
**Bases de Datos Relacionales (IS0737) · UPEM · Periodo 27/1**

## Objetivo
Usar GitHub como repositorio de control de versiones para documentar y respaldar todos los avances de tu proyecto integrador durante el semestre (diagramas, scripts SQL y documentación).

---

## 1. Crear tu cuenta en GitHub
1. Entra a **https://github.com** y da clic en **Sign up**.
2. Regístrate con tu correo institucional o personal, elige un nombre de usuario profesional (evita apodos).
3. Verifica tu correo cuando te lo pida GitHub.

## 2. Crear el repositorio del proyecto
1. Ya dentro de GitHub, da clic en el botón **+** (arriba a la derecha) → **New repository**.
2. **Repository name:** `bases-datos-relacionales-[tu-nombre]` (ejemplo: `bases-datos-relacionales-jperez`).
3. Descripción breve: el nombre de tu proyecto (ej. "Sistema de gestión para clínica veterinaria").
4. Visibilidad: **Public** (así el docente puede revisarlo sin necesidad de invitación; si prefieres **Private**, agrega al docente como colaborador en **Settings → Collaborators**).
5. Marca la casilla **Add a README file**.
6. Clic en **Create repository**.
7. Copia la URL del repositorio (botón verde **Code** → copiar el link HTTPS) y súbela en la tarea correspondiente de Classroom.

## 3. Estructura sugerida de carpetas
Dentro de tu repositorio, organiza así tus archivos (puedes crearlas directamente desde la web con "Add file → Create new file", escribiendo `carpeta/archivo.md`):

```
/diagramas        → capturas o archivos .mwb de tus diagramas E-R
/scripts          → tus archivos .sql (DDL, datos de prueba, consultas, vistas)
/documentacion    → propuesta, avances semanales, entrega final
README.md         → descripción general del proyecto
```

## 4. Formas de subir tus avances
Elige la opción con la que te sientas más cómodo; **ambas son válidas**.

### Opción A — Solo desde el navegador (más simple, recomendada si vas iniciando)
1. Entra a tu repositorio en github.com.
2. Ve a la carpeta correspondiente (o créala) y da clic en **Add file → Upload files**.
3. Arrastra tu archivo (script `.sql`, imagen del diagrama, documento).
4. Abajo, en **Commit changes**, escribe un mensaje descriptivo (ver sección 5).
5. Clic en **Commit changes**.

### Opción B — Con Git instalado (recomendada si usarás GitHub también en otras materias)
1. Instala Git: **https://git-scm.com/downloads**.
2. Clona tu repositorio una sola vez:
   ```bash
   git clone https://github.com/tu-usuario/bases-datos-relacionales-tu-nombre.git
   cd bases-datos-relacionales-tu-nombre
   ```
3. Cada semana, copia tus archivos nuevos/actualizados dentro de la carpeta correspondiente y ejecuta:
   ```bash
   git add .
   git commit -m "Avance 3: llaves primarias y foráneas definidas"
   git push
   ```

## 5. Buenas prácticas de commits
- Un commit por avance semanal (no esperes a acumular varios).
- Mensajes descriptivos, en tiempo presente y específicos:
  - Bien: `"Agrega script DDL con 3 tablas normalizadas"`
  - Mal: `"cambios"`, `"avance"`, `"final"`
- Si corriges algo del avance anterior, indícalo: `"Corrige llave foránea en tabla pedidos"`.

## 6. Checklist antes de cada entrega semanal
- [ ] El archivo/script está dentro de la carpeta correcta.
- [ ] El commit tiene un mensaje claro.
- [ ] El repositorio es público o el docente ya está agregado como colaborador.
- [ ] La liga que pegarás en Classroom corresponde a tu repositorio (no a un fork ni a otro proyecto).

## 7. Entrega final del proyecto
En la entrega final (06-ene) tu repositorio debe reflejar el historial completo del semestre:
- Diagrama E-R final.
- Script SQL completo (tablas normalizadas, datos de prueba, vistas, consultas relevantes).
- Documento breve de descripción del proyecto.
- El historial de commits debe mostrar avance progresivo real (no todo subido el mismo día), ya que forma parte de la evaluación de "Control de versiones" en la rúbrica del proyecto.
