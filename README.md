# 🔥 Proyecto Phoenix: Infraestructura como Código

Repositorio de automatización con **Ansible** para desplegar servidores de producción seguros y listos para contenedores, partiendo de una instalación mínima de Ubuntu Server.

## 📋 Arquitectura

* **Nodo de Control:** Pop!_OS (Ansible + Git).
* **Nodo Objetivo:** Ubuntu Server 22.04 LTS (Ejecutándose en **Incus Container**).
* **Filosofía:** Idempotencia, Seguridad por Diseño y Modularidad.

## 🛠️ Estructura del Proyecto

El proyecto utiliza "Ansible Roles" para separar responsabilidades y `group_vars` para la configuración centralizada:

| Directorio | Propósito |
| :--- | :--- |
| `roles/common` | Actualización del sistema y paquetería base (vim, htop, git, tree, ufw). |
| `roles/security` | **Hardening**: Configuración de Firewall (UFW) y blindaje de SSH (Solo llaves, no root). |
| `roles/docker` | Instalación de Docker CE (Repo oficial) y configuración de usuarios sin sudo. |
| `group_vars/` | **[Refactor]** Variables globales (puertos abiertos, listas de paquetes) para fácil edición. |

## 🚀 Uso Rápido

### 1. Requisitos Previos
* Tener acceso SSH sin contraseña al servidor objetivo (`ssh-copy-id`).
* Configurar la IP y la ruta de la llave privada en `inventory/hosts.ini`.

### 2. Verificar Conectividad
```bash
ansible all -m ping
















## Arquitectura
- **Controlador:** Pop!_OS (Ansible)
- **Objetivo:** Ubuntu Server 22.04 (Incus Container)

## Uso Rápido
1. Verificar conectividad: `ansible all -m ping`
2. Desplegar: `ansible-playbook site.yml`

## Roles
- **Common:** Paquetes base (htop, git, ufw).
- **Security:** Hardening de SSH y Firewall UFW.
- **Docker:** Instalación oficial de Docker CE.



# set up contenedor
incus launch images:ubuntu/22.04 phoenix-vm



# Crear usuario, home directory (-m), shell bash (-s) y grupo sudo (-G)
incus exec phoenix-vm -- useradd -m -s /bin/bash -G sudo sysadmin

# (OPCIONAL PERO RECOMENDADO) Instalar SSH server si no viene
incus exec phoenix-vm -- apt update
incus exec phoenix-vm -- apt install -y openssh-server




# configurar una contraseña temporal.
incus exec phoenix-vm -- passwd sysadmin


# obtenr la IP 
incus list phoenix-vm

#Establecer la confianza (SSH Copy ID)
ssh-copy-id sysadmin@<IP_DEL_CONTENEDOR>



#prueba de fuego
ssh sysadmin@<IP_DEL_CONTENEDOR>


#Habilitar "Passwordless Sudo"
incus exec phoenix-vm -- bash -c "echo 'sysadmin ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/sysadmin"


# set up 
ansible-playbook site.yml
