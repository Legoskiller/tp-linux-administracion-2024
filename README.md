# tp-linux-administracion-2024
# Trabajo Práctico — Administración de Sistemas GNU/Linux  
Universidad de Palermo

## Integrantes del grupo
- Ezequiel Beck     

## Contenido del repositorio
Este repositorio contiene los archivos solicitados en el Trabajo Práctico:

- `/root` (comprimido en root.tar.gz)
- `/etc` (comprimido en etc.tar.gz)
- `/opt` (comprimido en opt.tar.gz)
- `/www_dir` (comprimido en www_dir.tar.gz)
- `/backup_dir` (comprimido en backup_dir.tar.gz)
- `/var` dividido en partes (var_part_aa, var_part_ab, etc.)
- Diagrama topológico de la infraestructura (topologia.png)

## Descripción General
En este trabajo se configuraron:
- Servicios SSH, Apache + PHP 7.3+, MariaDB
- Red estática
- Particiones adicionales (/www_dir y /backup_dir)
- Script de backup con tareas programadas
- Pruebas de conectividad y servicio

-                          ┌───────────────────────────────┐
                           │    Máquina Física / Host       │
                           │  (Windows / Linux / Mac)       │
                           └───────────────┬───────────────┘
                                           │
                           Red en modo Bridge / NAT en VirtualBox
                                           │
                           ┌───────────────┴───────────────┐
                           │         VM Debian 11           │
                           │         Hostname: TPServer     │
                           ├─────────────────────────────────┤
                           │ IP Estática (ejemplo):          │
                           │   192.168.0.50                  │
                           ├─────────────────────────────────┤
                           │ Servicios instalados:           │
                           │  • SSH (root por clave pública) │
                           │  • Apache + PHP 7.3+            │
                           │  • MariaDB                      │
                           ├─────────────────────────────────┤
                           │ Almacenamiento:                 │
                           │  Disco principal (SO)           │
                           │  Disco extra 10GB:              │
                           │    /dev/sdb1 → /www_dir (3GB)   │
                           │    /dev/sdb2 → /backup_dir (6GB)│
                           ├─────────────────────────────────┤
                           │ Respaldos automáticos (cron):   │
                           │  • /var/log → diario 00:00      │
                           │  • /www_dir → L, M, V 23:00     │
                           └──────────────────────────────────┘
