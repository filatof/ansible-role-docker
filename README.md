# Ansible Role: Docker / Podman

Ansible роль для установки и настройки Docker или Podman в зависимости от семейства операционной системы.

- **Debian/Ubuntu**: устанавливается Docker
- **RedHat/CentOS/Rocky/AlmaLinux**: устанавливается Podman

## Требования

- Ansible >= 2.9
- Поддерживаемые ОС:
  - Ubuntu 20.04, 22.04, 24.04
  - Debian 10, 11, 12
  - CentOS 8, 9
  - Rocky Linux 8, 9
  - AlmaLinux 8, 9
  - RHEL 8, 9

## Переменные роли

Доступные переменные и их значения по умолчанию (см. `defaults/main.yml`):

```yaml
# Версия Docker для установки (для Debian/Ubuntu)
docker_version: "latest"

# Добавлять ли пользователей в группу docker
docker_users: []
# docker_users:
#   - username1
#   - username2

# Установить Docker Compose (для Debian/Ubuntu)
docker_install_compose: true
docker_compose_version: "latest"

# Версия Podman (для RedHat-based систем)
podman_version: "latest"

# Настройки Podman
podman_registries:
  - docker.io
  - quay.io
```

## Зависимости

Роль не имеет зависимостей от других ролей.

## Примеры использования

### Базовая установка

```yaml
- hosts: all
  become: yes
  roles:
    - ansible-role-docker
```

### С пользовательскими настройками

```yaml
- hosts: docker_servers
  become: yes
  roles:
    - role: ansible-role-docker
      vars:
        docker_users:
          - deploy
          - developer
```

### Установка конкретной версии

```yaml
- hosts: production
  become: yes
  roles:
    - role: ansible-role-docker
      vars:
        docker_version: "24.0.7"
        docker_compose_version: "2.23.0"
```

### Настройка для RedHat с Podman

```yaml
- hosts: rhel_servers
  become: yes
  roles:
    - role: ansible-role-docker
      vars:
        podman_registries:
          - docker.io
          - registry.redhat.io
          - quay.io
```

## Лицензия

MIT

## Автор

Эта роль создана и поддерживается [filatof](https://github.com/filatof).
