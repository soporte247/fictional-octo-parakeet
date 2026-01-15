# DVWA Pentesting Lab: From Zero to Exploit

Este repositorio contiene la configuración y documentación de un laboratorio de ciberseguridad basado en **Damn Vulnerable Web Application (DVWA)**, desplegado sobre **Vagrant** y **Docker**.

## Infraestructura y Despliegue
- **Virtualización**: Ubuntu Server vía Vagrant.
- **Contenedores**: Docker (Image: `vulnerables/web-dvwa`).
- **Networking**: Se configuró un túnel de puerto (`forwarded_port`) en el puerto **8080** para saltar bloqueos de red locales.

##  Hallazgos de Pentesting (Write-ups)

### 1. SQL Injection (Error Based)
- **Vulnerabilidad**: Falta de sanitización en el campo `User ID`.
- **Exploit**: Usando el payload `' OR '1'='1`, se logró extraer la base de datos completa de usuarios.
![Evidencia SQLi](./evidencias/sqli_exploit.png)

### 2. Remote Command Injection
- **Vulnerabilidad**: Ejecución de comandos del sistema a través de un campo de entrada de IP.
- **Impacto**: Acceso a archivos sensibles (`/etc/passwd`) y lectura del código fuente del servidor (`index.php`).
![Evidencia RCE](./evidencias/command_injection.png)
![Evidencia RCE 2](./evidencias/command_injection_2.png)
![Detalles SQLi](./evidencias/sqli_details.png)
![Vista completa RCE](./evidencias/rce_full_view.png)

### 3. Brute Force Attack
- **Vulnerabilidad**: Ausencia de políticas de bloqueo de intentos y contraseñas débiles.
- **Resultado**: Acceso exitoso a la cuenta del usuario `pablo` mediante el password `letmein`.
![Evidencia Brute Force](./evidencias/brute_force_win.png)

## Cómo ejecutar
1. `vagrant up`
2. `vagrant ssh`
3. `sudo docker run --rm -it -p 80:80 vulnerables/web-dvwa`
4. Acceder a `http://localhost:8080`