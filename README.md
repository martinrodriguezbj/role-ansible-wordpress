# ansible-role-wordpress

[![Molecule Test](https://github.com/martinrodriguezbj/ansible-role-wordpress/actions/workflows/molecule-ci.yml/badge.svg)](https://github.com/martinrodriguezbj/ansible-role-wordpress/actions)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-martinrodriguezbj.wordpress-blue.svg)](https://galaxy.ansible.com/martinrodriguezbj/wordpress)

Este role de Ansible instala y configura **WordPress** en servidores basados en Debian/Ubuntu o RedHat.  
Incluye instalación de dependencias PHP y Apache/Httpd, descarga del paquete WordPress y configuración automática del archivo `wp-config.php`.

---

## Requisitos

- Ansible >= 2.12
- Acceso SSH con privilegios `sudo`
- Servidor soportado: Debian 11, Ubuntu 22.04, Rocky Linux 9 (o compatibles)
- Base de datos MySQL/MariaDB ya configurada y accesible

---

## Variables

Las variables configurables están en `defaults/main.yml` y se pueden sobreescribir en tu playbook o `group_vars`.

### Variables principales

| Variable                    | Descripción                                       | Valor por defecto              |
|-----------------------------|---------------------------------------------------|--------------------------------|
| `wordpress_db_name`         | Nombre de la base de datos                        | `wordpress`                    |
| `wordpress_db_user`         | Usuario de la base de datos                       | `wp_user`                      |
| `wordpress_db_password`     | Contraseña del usuario de base de datos           | `wp_pass`                      |
| `wordpress_db_host`         | Host de la base de datos                          | `localhost`                    |
| `wordpress_site_url`        | URL del sitio WordPress                           | `http://localhost`             |
| `wordpress_site_title`      | Título del sitio WordPress                        | `Mi Sitio WordPress`           |
| `wordpress_admin_user`      | Usuario administrador del sitio                   | `admin`                        |
| `wordpress_admin_password`  | Contraseña del usuario administrador              | `admin123`                      |
| `wordpress_admin_email`     | Email del administrador                           | `admin@example.com`            |
| `wordpress_install_dir`     | Ruta de instalación de WordPress                  | `/var/www/html/wordpress`      |
| `wordpress_archive_url`     | URL para descargar la última versión de WordPress | `https://wordpress.org/latest.tar.gz` |
| `wordpress_web_user`        | Usuario del servidor web (apache/httpd)           | Detectado según el SO          |

### Claves de seguridad (`wp-config.php`)

Estas claves son utilizadas para mejorar la seguridad de las cookies y sesiones de WordPress.  
Defínelas en `defaults/main.yml` o sobreescríbelas en producción:

- `auth_key`
- `secure_auth_key`
- `logged_in_key`
- `nonce_key`
- `auth_salt`
- `secure_auth_salt`
- `logged_in_salt`
- `nonce_salt`

> **Recomendación:** Para entornos productivos, genera claves únicas y protégelas con `ansible-vault`.

---

## Ejemplo de uso

Ejemplo de playbook mínimo para usar este role:

```yaml
- hosts: wordpress
  become: true
  roles:
    - role: martinrodriguezbj.wordpress
      vars:
        wordpress_db_name: mysite
        wordpress_db_user: myuser
        wordpress_db_password: supersecret
        wordpress_site_title: "Blog Personal"
        wordpress_admin_password: "contraseñaSegura!"
```
# Test con Molecule

Este role incluye escenario de pruebas con Molecule. Para ejecutarlo:

```
Instalar dependencias
pip install molecule[docker] ansible-lint

Ejecutar pruebas completas
molecule test

O correr solo converge para verificar la instalación
molecule converge
```

Compatibilidad
Probado en:

Debian 11 (Bullseye)
Ubuntu 22.04 (Jammy)
Rocky Linux 9

Licencia
MIT

Autor
Role desarrollado por Martin Rodriguez
Disponible en [Ansible Galaxy](https://galaxy.ansible.com/martinrodriguezbj/wordpress)
