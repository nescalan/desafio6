# Desafío 6: Implementación de Ansible Playbooks y Roles

## Descripción

Este proyecto consiste en la creación y modularización de un sistema de _Configuration Management_ utilizando **Ansible**. La meta es instalar y desplegar un sitio web de **WordPress** en un host EC2 de AWS, incluyendo la configuración de **PHP** (con sus componentes) y **MySQL**.

El proyecto es parte del Desafío No. 6 del bootcamp de **EducaciónIT** y tiene como objetivo entregar un entorno funcional que pueda ser usado para demostraciones.

---

## Objetivos del Proyecto

1. Configurar un host EC2 en AWS para instalar WordPress.
2. Crear **playbooks** y **roles** para PHP y MySQL.
3. Modularizar el código mediante el uso de variables reutilizables.
4. Proveer documentación clara y detallada para facilitar la replicación del entorno.

---

## Requisitos Previos

Antes de iniciar, asegúrate de cumplir con los siguientes requisitos:

1. Acceso a AWS Academy para provisionar un bastión y una instancia EC2 con Ubuntu.
2. Archivo `.pem` para acceder al servidor.
3. Tener instalado:
   - **Ansible** >= 2.9
   - **Python** >= 3.6
4. Clonar este repositorio en tu máquina local:
   ```bash
   git clone <URL del repositorio>
   cd desafio-6
   ```
