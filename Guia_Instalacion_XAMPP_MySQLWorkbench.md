# Guía de instalación — XAMPP y MySQL Workbench
**Bases de Datos Relacionales (IS0737) · UPEM · Sesión 1 (09-sep)**

## Objetivo
Dejar listo el entorno de trabajo del semestre: un servidor MySQL local (vía XAMPP) y una herramienta gráfica para administrarlo (MySQL Workbench).

## Requisitos previos
- Laptop con Windows 10/11, macOS o Linux.
- Al menos 2 GB libres en disco.
- Permisos de administrador en el equipo (la instalación los requiere).
- Conexión a internet solo para la descarga inicial.

---

## Parte A — Instalar XAMPP

1. Descarga el instalador desde el sitio oficial: **https://www.apachefriends.org** (elige la versión de tu sistema operativo).
2. Ejecuta el instalador.
   - **Windows:** si tu antivirus o el Control de Cuentas de Usuario muestran una alerta, permite la instalación (es normal en XAMPP).
   - **Mac:** abre el `.dmg` y sigue el asistente.
3. En la selección de componentes, asegúrate de marcar al menos: **Apache**, **MySQL** y **phpMyAdmin**.
4. Instala en la ruta por defecto (`C:\xampp` en Windows, `/Applications/XAMPP` en Mac).
5. Al finalizar, abre el **Panel de Control de XAMPP**.
6. Da clic en **Start** en el módulo **Apache** y en el módulo **MySQL**. Ambos deben ponerse en verde ("Running").
7. Verifica que funciona: abre tu navegador y entra a `http://localhost/`. Debe aparecer la página de bienvenida de XAMPP.
8. Verifica MySQL: entra a `http://localhost/phpmyadmin/`. Debe abrir el panel de administración de la base de datos (sin pedir contraseña la primera vez).

### Problemas comunes en XAMPP
| Problema | Causa probable | Solución |
|---|---|---|
| El puerto 80 de Apache no arranca | Skype, IIS o algún otro programa ya usa ese puerto | En XAMPP, botón **Config** del módulo Apache → cambiar el puerto a 8080, o cerrar el programa que lo ocupa |
| El puerto 3306 de MySQL no arranca | Ya tienes un MySQL/MariaDB instalado previamente en el equipo | Detén el servicio de MySQL existente desde el administrador de servicios del sistema operativo, o cambia el puerto de XAMPP |
| MySQL se pone rojo al iniciar | Cierre incorrecto anterior (archivo de bloqueo) | Cierra XAMPP, borra el archivo `mysql/data/*.pid` dentro de la carpeta de XAMPP, reinicia |

---

## Parte B — Instalar MySQL Workbench

1. Descarga el instalador desde: **https://dev.mysql.com/downloads/workbench/**.
2. Instálalo con las opciones por defecto.
3. Abre MySQL Workbench. En la pantalla principal, da clic en el botón **+** junto a "MySQL Connections" para crear una nueva conexión.
4. Configura la conexión con estos datos (los valores por defecto de XAMPP):
   - **Connection Name:** `BasesDatosRelacionales`
   - **Hostname:** `127.0.0.1`
   - **Port:** `3306`
   - **Username:** `root`
   - **Password:** deja vacío (XAMPP no pone contraseña por defecto). Si más adelante configuras una, guárdala en el "Store in Vault".
5. Da clic en **Test Connection**. Debe aparecer "Successfully made the MySQL connection".
6. Guarda la conexión y ábrela con doble clic.

### Problemas comunes en MySQL Workbench
| Problema | Causa probable | Solución |
|---|---|---|
| "Can't connect to MySQL server" | El módulo MySQL de XAMPP no está corriendo | Regresa al panel de XAMPP y da clic en **Start** en MySQL |
| Pide contraseña y no la tienes | Se configuró una contraseña de root previamente | Prueba dejarla vacía o revisa con tu equipo/compañeros qué contraseña se usó al instalar |
| Conexión muy lenta o "tiempo de espera agotado" | Firewall bloqueando el puerto 3306 | Permite la conexión en el firewall de Windows/Mac cuando aparezca la alerta |

---

## Parte C — Verificación final (entregable de la sesión)

1. En MySQL Workbench, con tu conexión abierta, ejecuta:
   ```sql
   CREATE DATABASE prueba_instalacion;
   USE prueba_instalacion;
   CREATE TABLE alumno (
       id INT PRIMARY KEY AUTO_INCREMENT,
       nombre VARCHAR(100)
   );
   INSERT INTO alumno (nombre) VALUES ('Prueba exitosa');
   SELECT * FROM alumno;
   ```
2. Debes ver una fila con el texto "Prueba exitosa" en el resultado.
3. Toma una captura de pantalla mostrando: el panel de XAMPP con Apache y MySQL en verde, y el resultado de la consulta `SELECT` en Workbench.
4. Sube la captura en la tarea "Crear cuenta y repositorio en GitHub" de Classroom (o donde se indique), como evidencia de instalación completada.

> Conserva XAMPP corriendo cada vez que trabajes en el laboratorio: todas las prácticas del semestre dependen de que Apache y MySQL estén en verde.
