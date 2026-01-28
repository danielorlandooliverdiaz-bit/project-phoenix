# Proyecto Phoenix

Infraestructura como código para servidor base seguro con Docker.

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
