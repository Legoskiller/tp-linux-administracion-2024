# tp-linux-administracion-2024
# Trabajo Práctico Final – Administración de Sistemas GNU/Linux  
## Universidad de Palermo – Facultad de Ingeniería

---

## 🧑‍💻 Integrantes del Grupo
- Ezequiel Beck  

---

## 📘 Descripción General del Trabajo

Este repositorio contiene los archivos solicitados como entregable del Trabajo Práctico Final correspondiente a la materia **Administración de Sistemas GNU/Linux**.  
El trabajo consistió en la instalación, configuración, administración y documentación de un servidor GNU/Linux Debian dentro de una máquina virtual proporcionada por la Universidad.

Se configuraron servicios, almacenamiento, scripts automatizados, tareas programadas, red y mecanismos de acceso remoto a través de claves SSH.

---

# 🖥️ **Infraestructura Implementada**

## **Servidor Virtual**
- **Sistema operativo:** Debian (versión provista por la cátedra)  
- **Hostname:** `TPServer`  
- **Acceso root:** mediante clave pública SSH  
- **Servicios instalados y configurados:**
  - OpenSSH Server  
  - Apache2 + PHP 7.3 o superior  
  - MariaDB  
  - Cron para automatización de backups  

## **Red**
- Configuración manual mediante archivo `/etc/network/interfaces`
- IP Estática asignada en el mismo rango que la máquina física

---

# 💾 **Almacenamiento**

Se agregó un disco virtual adicional de **10 GB**, del cual se crearon dos particiones:

| Partición | Punto de Montaje | Tamaño | Descripción |
|----------|------------------|--------|-------------|
| `/dev/sdb1` | `/www_dir` | 3 GB | Contenido del sitio web (index.php / logo.png) |
| `/dev/sdb2` | `/backup_dir` | 6 GB | Destino de backups automáticos |

Ambas particiones fueron configuradas en `/etc/fstab` para montarse automáticamente al inicio del sistema.

---

# 🔐 **Backup**

Se desarrolló un script de backup ubicado en:  
`/opt/scripts/backup_full.sh`

Funciones del script:
- Permitir backups parametrizados con `-origen` y `-destino`
- Validar la existencia de sistemas de archivos
- Generar archivos `.tar.gz` con fecha en formato ANSI (YYYYMMDD)
- Incluir opción de ayuda `-help`

## **Automatización mediante cron**
- **Diario a las 00:00:** Backup de `/var/log`
- **Lunes, miércoles y viernes a las 23:00:** Backup de `/www_dir`

---

# 📂 **Contenido del Repositorio**

Los siguientes directorios solicitados fueron exportados desde la máquina virtual en formato `.tar.gz`:

| Directorio original | Archivo en este repositorio |
|---------------------|-----------------------------|
| `/root` | `root.tar.gz` |
| `/etc` | `etc.tar.gz` |
| `/opt` | `opt.tar.gz` |
| `/www_dir` | `www_dir.tar.gz` |
| `/backup_dir` | `backup_dir.tar.gz` |

El directorio `/var` fue comprimido y dividido debido a su tamaño:

| Archivo dividido | Descripción |
|------------------|-------------|
| `var_part_aa` | Parte 1 |
| `var_part_ab` | Parte 2 |
| `var_part_ac` | Parte 3 |
| `var_part_ad` | Parte 4 |
| `var_part_ae` | Parte 5 (última, tamaño menor) |

---

# 🌐 **Diagrama Topológico**

A continuación se incluye el diagrama topológico de la infraestructura implementada:
                       ┌───────────────────────────────┐
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
                       │  /dev/sdb1 → /www_dir (3GB)     │
                       │  /dev/sdb2 → /backup_dir (6GB)  │
                       ├─────────────────────────────────┤
                       │ Respaldos automáticos (cron):   │
                       │  • /var/log → diario 00:00      │
                       │  • /www_dir → L, M, V 23:00     │
                       └──────────────────────────────────┘



