# LAB-006 — Vulnversity | TryHackMe

## Objetivo
Laboratorio práctico de pentesting para preparación eJPT.

**Plataforma:** TryHackMe  
**Máquina:** Vulnversity  
**Sistema operativo:** Ubuntu Linux  
**Estado:** Completado

## 1. Reconocimiento

Se realizó un escaneo TCP completo con Nmap.

Puertos encontrados:

| Puerto | Servicio |
|--------|----------|
| 21 | FTP |
| 22 | SSH |
| 139 | NetBIOS |
| 445 | SMB |
| 3128 | Squid Proxy 4.10 |
| 3333 | Apache HTTP |

## 2. Enumeración web

Se identificó el directorio:

/internal/

Contenía un formulario de subida de archivos.

## 3. Vulnerabilidad identificada

El formulario restringía archivos PHP convencionales,
pero permitía la extensión .phtml.

Esto permitió demostrar ejecución remota de código
con los permisos del usuario www-data.

## 4. Escalada de privilegios

Durante la enumeración de archivos SUID se identificó:

/bin/systemctl

El ejecutable pertenecía a root y tenía SUID activado.

Se demostró que podía iniciar servicios con privilegios
elevados y ejecutar comandos con EUID 0.

## 5. Resultado

- Acceso inicial: www-data
- Escalada: SUID systemctl
- Privilegios finales: root
- Objetivo del laboratorio: completado

## 6. Recomendaciones

- Validar extensiones y contenido de archivos subidos.
- Almacenar las subidas fuera del directorio web ejecutable.
- Eliminar permisos SUID innecesarios.
- Aplicar el principio de mínimo privilegio.
- Auditar periódicamente los permisos del sistema.

## Aviso legal

Práctica realizada exclusivamente en un entorno
de entrenamiento autorizado de TryHackMe.

Las cargas útiles, credenciales y flags no se publican.
