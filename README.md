### README.md

# Desafío No. 6: Automatización de Despliegue de WordPress con Ansible

Hola, bienvenido a mi proyecto del **Desafío No. 6** del bootcamp de EducaciónIT. En este desafío, trabajé en la automatización del despliegue de WordPress en una instancia EC2 de AWS usando Ansible. Mi objetivo fue crear un entorno completamente funcional que incluye la instalación y configuración de Apache, PHP y MariaDB, junto con la configuración de WordPress como el sitio principal.

Quiero compartir los pasos que seguí para implementar este proyecto, los requisitos necesarios, y cómo configurarlo si decides probarlo tú mismo. ¡Espero que te sea útil!

---

## **Requisitos Previos**

Antes de ejecutar este proyecto, asegúrate de cumplir con los siguientes requisitos:

1. **Herramientas Instaladas**:

   - Ansible (versión 2.9 o superior).
   - Python 3 con `pip`.
   - Clave privada (_.pem_) para acceder a tu instancia EC2.

2. **Acceso a AWS**:

   - Una instancia EC2 con Ubuntu.
   - Un grupo de seguridad configurado para permitir tráfico en los puertos 22 (SSH) y 80 (HTTP).

3. **Repositorio Clonado**:
   Clona este repositorio en tu computadora:

   ```bash
   git clone <URL-del-repositorio>
   cd desafio6
   ```

4. **Inventario Configurado**:
   Asegúrate de tener un archivo `inventory.ini` configurado correctamente (ver sección **Configuración del Inventario**).

---

## **Configuración del Inventario**

Para que Ansible pueda acceder a tu instancia EC2, debes configurar un archivo `inventory.ini`. Aquí está un ejemplo:

```ini
[wordpress]
34.222.168.68 ansible_user=ubuntu ansible_ssh_private_key_file=/path/to/your-key.pem
```

- Reemplaza `34.222.168.68` con la IP pública de tu instancia EC2.
- Ajusta la ruta al archivo de clave privada (_.pem_).

---

## **Variables Configurables**

En el archivo `playbook.yaml`, definí estas variables para facilitar la configuración:

```yaml
vars:
  db_name: "wordpress_db" # Nombre de la base de datos
  db_user: "nelson" # Usuario de la base de datos
  db_password: "tu_contraseña_segura" # Contraseña del usuario de la base de datos
```

Puedes cambiarlas según tus necesidades antes de ejecutar el _playbook_.

---

## **Pasos para Ejecutar el Playbook**

1. **Prueba la Conexión con el Servidor**:
   Antes de empezar, asegúrate de que Ansible puede conectarse a tu servidor EC2:

   ```bash
   ansible -i inventory.ini wordpress -m ping
   ```

2. **Ejecuta el Playbook**:
   Una vez verificada la conexión, ejecuta el playbook para instalar y configurar WordPress:

   ```bash
   ansible-playbook -i inventory.ini playbook.yaml
   ```

3. **Accede a WordPress**:
   Cuando termine el proceso, abre un navegador y ve a la IP pública de tu instancia EC2. Deberías ver la página de configuración inicial de WordPress.

---

## **Estructura del Proyecto**

Esta es la estructura del repositorio que desarrollé:

```
desafio6/
├── ansible.cfg
├── inventory.ini
├── playbook.yaml
├── roles/
│   ├── apache/
│   │   ├── tasks/
│   │   │   └── main.yaml
│   │   └── templates/
│   │       └── wordpress.conf.j2
│   ├── mysql/
│   │   ├── tasks/
│   │   │   └── main.yaml
│   ├── php/
│   │   ├── tasks/
│   │   │   └── main.yaml
└── README.md
```

---

## **Resolución de Problemas**

### Error: "Could not find or access..."

Esto pasa cuando Ansible no encuentra un archivo remoto, como `wp-config-sample.php`. Asegúrate de que el archivo existe en el servidor remoto y usa el módulo `command` en lugar de `copy` si es necesario.

### Error: "Access denied for user 'root'@'localhost'"

Esto ocurre si MySQL está configurado con `unix_socket`. Cambié el método de autenticación a contraseña con este comando en MySQL:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'tu_contraseña_segura';
FLUSH PRIVILEGES;
```

---

## **Reflexión**

Este proyecto me ayudó a profundizar en cómo Ansible puede simplificar la configuración de infraestructura en la nube. También aprendí a trabajar con roles, plantillas y variables, lo que hizo que el despliegue fuera más modular y eficiente. Si tienes sugerencias o encuentras algo que pueda mejorar, ¡me encantaría recibir tu retroalimentación! 😊

---

¡Gracias por revisar mi proyecto! 🚀
