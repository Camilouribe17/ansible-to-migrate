Building a simple LAMP stack and deploying Application using Ansible Playbooks.
-------------------------------------------

Estos Playbooks requieren Ansible 1.2.

Estos Playbooks están destinados a ser una guía de referencia y de inicio para la creación de Playbooks Ansible. Estos manuales se probaron en CentOS 6.x por lo que recomendamos que utilice CentOS o RHEL para probar estos módulos.

Esta pila LAMP puede estar en un solo nodo o en varios nodos. El archivo de inventario 'hosts' define los nodos en los que se deben configurar las pilas.

        [webservers]
        localhost

        [dbservers]
        bensible
     
Aquí el servidor web sería configurado en el host local y el dbserver en un servidor llamado "bensible". La pila se puede implementar mediante el siguiente comando:

        ansible-playbook -i hosts site.yml
     
Una vez hecho esto, puede comprobar los resultados consultando http: //localhost/index.php. Debería ver una página de prueba simple y una lista de bases de datos recuperadas del servidor de bases de datos.

<h1>Pasos:</h1>
1. Debes construir un docker personalizado que incluye el servidor openssh
- Creación de la imagen en la que se basará el contenedor.
Se ejecuta el siguiente comando :
$ (sudo) docker build -t {{ nombre imagen }}.

----------------------------------------------------------------------------------

2. Ahora debes crear un conjunto de maquinas para el despliegue, se creará un servidor web (apache) y uno de bases de datos (mysql).

Nombre del contenedor web = web
Nombre del contenedor mysql = db

----------------------------------------------------------------------------------

3. Opción 1: edita el archivo /etc/hosts y adiciona 3 alias a localhost
127.0.0.1 web_server mysql_server

Opción 2: adición automática en el archivo de hosts del sistema
echo "127.0.0.1 web_server mysql_server" | sudo tee -a /etc/hosts

----------------------------------------------------------------------------------

4. Para realizar nuestra conexion nuestra llave privada debe contar con los permisos de esta forma [-xw-------] lo que equivale a 0600.

chmod 0600 ../authorized_keys

----------------------------------------------------------------------------------
5
. Realiza una prueba de conexión a las maquinas que se crearon recientemente, en el paso anterior se crearon 2 maquinas con el puerto 2221 y 2222 abiertos para conexión:

ssh root@web_server -p 2221 -i ../key.private ssh root@mysql_server -p 2222 -i ../authorized_keys

Si la conexión se establece, ya está listo para seguir con ansible.
