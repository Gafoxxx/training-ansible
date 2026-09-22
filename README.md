# training-ansible

## Pasos

### 1. Levantamiento de la VM con Terraform
Ejecuté primero el levantamiento de la VM por medio de Terraform, usando el repositorio que ya tenía creado previamente: https://github.com/Gafoxxx/BuildAVMwithTerraform-JFG

<img width="962" height="332" alt="image" src="https://github.com/user-attachments/assets/157deeef-e60d-467f-9998-3c254791a1be" />

Verifiqué que estoy dentro de la VM por medio de una conexión SSH.

### 2. Configuración del inventario de Ansible
Con ayuda del Ansible que envió el profesor y de un dork, edité el archivo `host.ini`.

<img width="962" height="332" alt="image" src="https://github.com/user-attachments/assets/d8db36c1-f351-42a7-afed-9d4f371b7d7e" />

### 3. Ejecución de los playbooks
Con ayuda de los siguientes comandos:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/install_docker.yml
ansible-playbook -i inventory/hosts.ini playbooks/run_container.yml
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/76473f41-597d-47ab-8d0f-4c842a4be335" />

Levantamos el contenedor que trae el videojuego y así lo desplegamos en la VM, quedando disponible en: http://20.25.68.113:8787/

### 4. Apertura de puertos
Al realizar esto tuve errores porque los puertos estaban cerrados, solo estaba abierto el 22. Así que tuve que ejecutar el siguiente comando para habilitar el puerto 8787:

```bash
az network nsg rule create -g juanfelipegt-rg --nsg-name juanfelipegt-nsg \
  -n PermitirMario8787 --priority 110 --direction Inbound --access Allow \
  --protocol Tcp --destination-port-ranges 8787 --source-address-prefixes '*'
```

### 5. Resultado final
Después de esto logré desplegar el videojuego correctamente:

<img width="1920" height="1017" alt="image" src="https://github.com/user-attachments/assets/6b9c74f2-a0f1-4e79-8b3c-b314953b25a3" />
