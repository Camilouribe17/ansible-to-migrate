Building a simple LAMP stack and deploying Application using Ansible Playbooks.
-------------------------------------------

Estos Playbooks requieren Ansible 1.2.

Estos Playbooks están destinados a ser una guía de referencia y de inicio para la creación de Playbooks Ansible. Estos manuales se probaron en CentOS 6.x por lo que recomendamos que utilice CentOS o RHEL para probar estos módulos.

Esta pila LAMP puede estar en un solo nodo o en varios nodos. El archivo de inventario 'hosts' define los nodos en los que se deben configurar las pilas.

     [servidores web]
     localhost

     [dbservers]
     bienesible
     
Aquí el servidor web sería configurado en el host local y el dbserver en un servidor llamado "bensible". La pila se puede implementar mediante el siguiente comando:

     ansible-playbook -i hosts site.yml
     
Una vez hecho esto, puede comprobar los resultados consultando http: //localhost/index.php. Debería ver una página de prueba simple y una lista de bases de datos recuperadas del servidor de bases de datos.

Pasos:
1. Generar DockerFile Ubuntu
2. Generar Dockers
3. Modificar Hosts
4. Modificar Ansibles
