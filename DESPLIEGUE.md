# DESPLIEGUE — Evidencias y respuestas

Este documento recopila todas las evidencias y respuestas de la practica.

**NOTA**: Para la práctica he utiliza nginx y sftp como nombres de los contenedores.

---

## Parte 1 — Evidencias minimas

### Fase 1: Instalacion y configuracion


1) Servicio Nginx activo
 - Que demuestra: Muestra que el servicio Nginx está en ejecución dentro del entorno Docker.
 - Comando: docker compose ps
 - Evidencia: ![Evidencia 1](evidencias/requisito1.png)

2) Configuracion cargada
 - Que demuestra: El archivo de configuración cargado.
 - Comando: "ls -l /etc/nginx/conf.d/" dentro del contenedor de nginx
 - Evidencia: ![Evidencia 2](evidencias/requisito2.png)

3) Resolucion de nombres
 - Que demuestra: Demuestra que la web usa ese nombre.
 - Comando: En este caso no he utilizado comando, lo he verificado directamente en el navegador.
 - Evidencia: ![Evidencia 3](evidencias/requisito3.png)

4) Contenido Web
 - Que demuestra: El contenido importado de Cloud Academy se muestra correctamente en la web.
 - Comando: En este caso no he utilizado comando, lo he verificado directamente en el navegador.
 - Evidencia: ![Evidencia 4](evidencias/requisito4.png)

### Fase 2: Transferencia SFTP (Filezilla)

5) Conexion SFTP exitosa
 - Que demuestra: Conexión SFTP exitosa al servidor con FileZilla.
 - Comando: En este caso no he utilizado comando, lo he verificado con FileZilla.
 - Evidencia: ![Evidencia 5](evidencias/requisito5.png)

6) Permisos de escritura
 - Que demuestra: Archivos subidos por SFTP sin problema de permisos.
 - Comando: En este caso no he utilizado comando, lo he verificado con FileZilla.
 - Evidencia: ![Evidencia 6](evidencias/requisito6.png)

### Fase 3: Infraestructura Docker

7) Contenedores activos
 - Que demuestra: Los contenedores están arrancados.
 - Comando: docker compose ps
 - Evidencia: ![Evidencia 7](evidencias/requisito7.png)

8) Persistencia (Volumen compartido)
 - Que demuestra: Los ficheros subidos via SFTP se sirven desde Nginx.
 - Comando: En este caso no he utilizado comando, lo he verificado directamente en el navegador y los ficheros con FileZilla.`
 - Evidencia: ![Evidencia 8](evidencias/requisito8.png)

9) Despliegue multi-sitio
 - Que demuestra: La ruta "/reloj" está servida correctamente como sitio secundario.
 - Comando: En este caso no he utilizado comando, lo he verificado en el navegador.
 - Evidencia: ![Evidencia 9](evidencias/requisito9.png)

### Fase 4: Seguridad HTTPS

10) Cifrado SSL
 - Que demuestra: HTTPS está activo, el puerto 8433 configurado y que el certificado está autofirmado.
 - Comando: En este caso no he utilizado comando, lo he verificado en el navegador.
 - Evidencia: ![Evidencia 10](evidencias/requisito10.png)

11) Redireccion forzada
 - Que demuestra: Las peticiones HTTP son redirigidas a HTTPS con un 301 Moved Permanently.
 - Comando: En este caso no he utilizado comando, lo he verificado en el navegador en la pestaña network.
 - Evidencia: ![Evidencia 11](evidencias/requisito11.png)

---

## Parte 2 — Evaluacion RA2 (a–j)

### a) Parametros de administracion
- Respuesta:

**1.** Evidencia de los fragmentos de los parametros de administración pedidos:
![Evidencia A-1](evidencias/a-01-grep-nginxconf.png)

**2.** Directivas:

**worker_processes**
- Controla: Define el número de procesos de trabajo.
- Configuración realista incorrecta: Poniendo un valor negativo (ej -1).
- Lo comprobaría mediante el comando "docker compose exec nginx nginx -t" que valida la configuración, la evidencia se encuentra al final de este punto.

**worker_connections**
- Controla: Establece el número máximo de conexiones simultáneas que puede ser abierto por un proceso de trabajo.
- Configuración realista incorrecta: Poniendo un valor negativo (ej -1).
- Lo comprobaría mediante el comando "docker compose exec nginx nginx -t" que valida la configuración, la evidencia se encuentra al final de este punto.

**access_log**
- Controla: Define archivos de log de acceso específicos para el sitio.
- Configuración realista incorrecta: Da error si se pone ningun valor.
- Lo comprobaría mediante el comando "docker compose exec nginx nginx -t" que valida la configuración, la evidencia se encuentra al final de este punto.

**error_log**
- Controla: Define archivos de log de error específicos para el sitio.
- Configuración realista incorrecta: Da error si no se pone ningún valor.
- Lo comprobaría mediante el comando "docker compose exec nginx nginx -t" que valida la configuración, la evidencia se encuentra al final de este punto.

**keepalive_timeout**
- Controla: establece un tiempo de espera durante el cual una conexión del cliente viva permanecerá abierta en el lado del servidor.
- Configuración realista incorrecta: Poniendo un valor negativo (ej -35)
- Lo comprobaría mediante el comando "docker compose exec nginx nginx -t" que valida la configuración, la evidencia se encuentra al final de este punto.

**include**
- Controla: Para incluir configuraciones adicionales
- Configuración realista incorrecta: Da error si no se incluye ningún valor.
- Lo comprobaría mediante el comando "docker compose exec nginx nginx -t" que valida la configuración, la evidencia se encuentra al final de este punto.

**gzip**
- Controla: Permite la compresión.
- Configuración realista incorrecta: Cualquier valor que no sea on y off.
- Lo comprobaría mediante el comando "docker compose exec nginx nginx -t" que valida la configuración, la evidencia se encuentra al final de este punto.

Para comprobar si la configuración es correcta utilizaría este comando "docker compose exec nginx nginx -t" que valida la configuración.

Evidencia de la validación de la configuración incorrecta:
![Evidencia A-2](evidencias/a-02-nginx-t.png)

**3.** Cambio seguro y reload:

He ajustado keepalive_timeout de 65 a 35 editando el nginx.conf local. Y he recargado la configuración de nginx mediante el comando "docker compose exec nginx nginx -s reload"

Evidencia del cambio y la recarga:

![Evidencia A-3](evidencias/a-03-reload.png)
- Evidencias:
  - evidencias/a-01-grep-nginxconf.png
  - evidencias/a-02-nginx-t.png
  - evidencias/a-03-reload.png

### b) Ampliacion de funcionalidad + modulo investigado
- Opcion elegida (B1 o B2):
- Respuesta: B1
- Evidencias (B1 o B2):
  - evidencias/b1-01-gzipconf.png
  ![Evidencia B1-1](evidencias/b1-01-gzipconf.png)
  - evidencias/b1-02-compose-volume-gzip.png
  ![Evidencia B1-2](evidencias/b1-02-compose-volume-gzip.png)
  - evidencias/b1-03-nginx-t.png
  ![Evidencia B1-3](evidencias/b1-03-nginx-t.png)
  - evidencias/b1-04-curl-gzip.png
  ![Evidencia B1-4](evidencias/b1-04-curl-gzip.png)
  - evidencias/b2-01-defaultconf-headers.png
  - evidencias/b2-02-nginx-t.png
  - evidencias/b2-03-curl-https-headers.png

#### Modulo investigado: <NOMBRE>
- Para que sirve:
- Como se instala/carga:
- Fuente(s):

### c) Sitios virtuales / multi-sitio
- Respuesta:
- Evidencias:
  - evidencias/c-01-root.png
![Evidencia C-1](evidencias/c-01-root.png)
  - evidencias/c-02-reloj.png
![Evidencia C-2](evidencias/c-02-reloj.png)
  - evidencias/c-03-defaultconf-inside.png
![Evidencia C-3](evidencias/c-03-defaultconf-inside.png)

### d) Autenticacion y control de acceso
- Respuesta:
- Evidencias:
  - evidencias/d-01-admin-html.png
![Evidencia D-1](evidencias/d-01-admin-html.png)
  - evidencias/d-02-defaultconf-auth.png
![Evidencia D-2](evidencias/d-02-defaultconf-auth.png)
  - evidencias/d-03-curl-401.png
![Evidencia D-3](evidencias/d-03-curl-401.png)
  - evidencias/d-04-curl-200.png
![Evidencia D-4](evidencias/d-04-curl-200.png)

### e) Certificados digitales
- Respuesta:
- Evidencias:
  - evidencias/e-01-ls-certs.png
![Evidencia E-1](evidencias/e-01-ls-certs.png)
  - evidencias/e-02-compose-certs.png
![Evidencia E-2](evidencias/e-02-compose-certs.png)
  - evidencias/e-03-defaultconf-ssl.png
![Evidencia E-3](evidencias/e-03-defaultconf-ssl.png)

### f) Comunicaciones seguras
- Respuesta:
- Evidencias:
  - evidencias/f-01-https.png
![Evidencia F-1](evidencias/c-03-defaultconf-inside.png)
  - evidencias/f-02-301-network.png
![Evidencia F-2](evidencias/f-02-301-network.png)

### g) Documentacion
- Respuesta:
- Evidencias: enlaces a todas las capturas

### h) Ajustes para implantacion de apps
- Respuesta:
- Evidencias:
  - evidencias/h-01-root.png
![Evidencia H-1](evidencias/h-01-root.png)
  - evidencias/h-02-reloj.png
![Evidencia H-2](evidencias/h-02-reloj.png)

### i) Virtualizacion en despliegue
- Respuesta:
- Evidencias:
  - evidencias/i-01-compose-ps.png
![Evidencia I-1](evidencias/i-01-compose-ps.png)

### j) Logs: monitorizacion y analisis
- Respuesta:
- Evidencias:
  - evidencias/j-01-logs-follow.png
![Evidencia J-1](evidencias/j-01-logs-follow.png)
  - evidencias/j-02-metricas.png
![Evidencia J-2](evidencias/j-02-metricas.png)
```
docker compose exec web sh -c "awk '{print \$7}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head"
docker compose exec web sh -c "awk '{print \$9}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head"
docker compose exec web sh -c "awk '\$9==404 {print \$7}' /var/log/nginx/access.log | sort | uniq -c | sort -nr | head"
```

---

## Checklist final

### Parte 1
- [✔️] 1) Servicio Nginx activo
- [✔️] 2) Configuracion cargada
- [✔️] 3) Resolucion de nombres
- [✔️] 4) Contenido Web (Cloud Academy)
- [✔️] 5) Conexion SFTP exitosa
- [✔️] 6) Permisos de escritura
- [✔️] 7) Contenedores activos
- [✔️] 8) Persistencia (Volumen compartido)
- [✔️] 9) Despliegue multi-sitio (/reloj)
- [✔️] 10) Cifrado SSL
- [✔️] 11) Redireccion forzada (301)

### Parte 2 (RA2)
- [✔️] a) Parametros de administracion
- [ ] b) Ampliacion de funcionalidad + modulo investigado
- [ ] c) Sitios virtuales / multi-sitio
- [✔️] d) Autenticacion y control de acceso
- [✔️] e) Certificados digitales
- [✔️] f) Comunicaciones seguras
- [ ] g) Documentacion
- [✔️] h) Ajustes para implantacion de apps
- [ ] i) Virtualizacion en despliegue
- [ ] j) Logs: monitorizacion y analisis
