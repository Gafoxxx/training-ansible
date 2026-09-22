# training-ansible
# Pasos:
1. Ejecuté primero el levantamiento de la vm por medio de terraform y el repositorio que ya tenía creado previamente https://github.com/Gafoxxx/BuildAVMwithTerraform-JFG.
   <img width="962" height="332" alt="image" src="https://github.com/user-attachments/assets/157deeef-e60d-467f-9998-3c254791a1be" />
Verifico que estoy dentro de la vm por medio de una conexión SSH.
2. Posteriormente con ayuda del ansible que envió el profesor y con ayuda de un dork. Edité el archivo host.ini
   <img width="962" height="332" alt="image" src="https://github.com/user-attachments/assets/d8db36c1-f351-42a7-afed-9d4f371b7d7e" />

4.Con ayuda de los comandos:
ansible-playbook -i inventory/hosts.ini playbooks/install_docker.yml
ansible-playbook -i inventory/hosts.ini playbooks/run_container.yml
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/76473f41-597d-47ab-8d0f-4c842a4be335" />

Levantamos el contenedor que trae el videojuego y así mismo lo desplegamos en la vm para posteriormente quedar desplegado en:http://20.25.68.113:8787/

4.Al realizar esto tuve errores porque los puertos estaban cerrados solo en el 22. Así que tuve que ejecutar los siguientes comandos para poder habilitar el puerto 8787:
az network nsg rule create -g juanfelipegt-rg --nsg-name juanfelipegt-nsg \
  -n PermitirMario8787 --priority 110 --direction Inbound --access Allow \
  --protocol Tcp --destination-port-ranges 8787 --source-address-prefixes '*'

 5.  Después de esto logré desplegar el videojuego:
 6.  <img width="1920" height="1017" alt="image" src="https://github.com/user-attachments/assets/6b9c74f2-a0f1-4e79-8b3c-b314953b25a3" />
