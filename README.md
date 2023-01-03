# adminer

[![Source Code](https://img.shields.io/badge/github-source%20code-blue?logo=github&logoColor=white)](https://github.com/rolehippie/adminer) [![General Workflow](https://github.com/rolehippie/adminer/actions/workflows/general.yml/badge.svg)](https://github.com/rolehippie/adminer/actions/workflows/general.yml) [![Readme Workflow](https://github.com/rolehippie/adminer/actions/workflows/readme.yml/badge.svg)](https://github.com/rolehippie/adminer/actions/workflows/readme.yml) [![Galaxy Workflow](https://github.com/rolehippie/adminer/actions/workflows/galaxy.yml/badge.svg)](https://github.com/rolehippie/adminer/actions/workflows/galaxy.yml) [![License: Apache-2.0](https://img.shields.io/github/license/rolehippie/adminer)](https://github.com/rolehippie/adminer/blob/master/LICENSE)
Ansible role to install Adminer database management.

## Sponsor

Building and improving this Ansible role have been sponsored by my current and previous employers like **[Cloudpunks GmbH](https://cloudpunks.de)** and **[Proact Deutschland GmbH](https://www.proact.eu)**.

## Table of content

- [adminer](#adminer)
  - [Sponsor](#sponsor)
  - [Table of content](#table-of-content)
  - [Default Variables](#default-variables)
    - [adminer\_base\_plugins](#adminer_base_plugins)
      - [Default value](#default-value)
      - [Example usage](#example-usage)
    - [adminer\_destination](#adminer_destination)
      - [Default value](#default-value-1)
    - [adminer\_download](#adminer_download)
      - [Default value](#default-value-2)
    - [adminer\_extra\_packages](#adminer_extra_packages)
      - [Default value](#default-value-3)
    - [adminer\_general\_packages](#adminer_general_packages)
      - [Default value](#default-value-4)
    - [adminer\_general\_plugins](#adminer_general_plugins)
      - [Default value](#default-value-5)
      - [Example usage](#example-usage-1)
    - [adminer\_group](#adminer_group)
      - [Default value](#default-value-6)
    - [adminer\_language](#adminer_language)
      - [Default value](#default-value-7)
    - [adminer\_max\_upload\_size](#adminer_max_upload_size)
      - [Default value](#default-value-8)
    - [adminer\_memory\_limit](#adminer_memory_limit)
      - [Default value](#default-value-9)
    - [adminer\_mysql](#adminer_mysql)
      - [Default value](#default-value-10)
    - [adminer\_mysql\_packages](#adminer_mysql_packages)
      - [Default value](#default-value-11)
    - [adminer\_owner](#adminer_owner)
      - [Default value](#default-value-12)
    - [adminer\_php\_paths](#adminer_php_paths)
      - [Default value](#default-value-13)
    - [adminer\_php\_versions](#adminer_php_versions)
      - [Default value](#default-value-14)
    - [adminer\_version](#adminer_version)
      - [Default value](#default-value-15)
  - [Discovered Tags](#discovered-tags)
  - [Dependencies](#dependencies)
  - [License](#license)
  - [Author](#author)

---

## Default Variables

### adminer_base_plugins

List of required base plugins

#### Default value

```YAML
adminer_base_plugins:
  - name: plugin
    url: https://raw.githubusercontent.com/vrana/adminer/v{{ adminer_version }}/plugins/plugin.php
    class: AdminerPlugin
```

#### Example usage

```YAML
adminer_base_plugins:
  - name: login-servers
    url: https://raw.githubusercontent.com/pematon/adminer-plugins/master/AdminerLoginServers.php
    class: AdminerLoginServers
    config: |
      [
        'mysql://database-01:3306' => 'Database 01',
        'mysql://database-02:3306' => 'Database 02',
      ]
```

### adminer_destination

Destination path where to install

#### Default value

```YAML
adminer_destination: /var/www/html/index.php
```

### adminer_download

URL to download the release from

#### Default value

```YAML
adminer_download: https://github.com/vrana/adminer/releases/download/v{{ adminer_version
  }}/adminer-{{ adminer_version }}{{ '-mysql' if adminer_mysql else '' }}{{ '-' +
  adminer_language if adminer_language | default(False) else '' }}.php
```

### adminer_extra_packages

List of extra packages to install

#### Default value

```YAML
adminer_extra_packages: []
```

### adminer_general_packages

List of packages for general databases

#### Default value

```YAML
adminer_general_packages:
  - php
  - php-mysql
  - php-sqlite3
  - php-pgsql
  - php-mongodb
```

### adminer_general_plugins

List of plugins to install

#### Default value

```YAML
adminer_general_plugins: []
```

#### Example usage

```YAML
adminer_general_plugins:
  - name: login-servers
    url: https://raw.githubusercontent.com/pematon/adminer-plugins/master/AdminerLoginServers.php
    class: AdminerLoginServers
    config: |
      [
        'mysql://database-01:3306' => 'Database 01',
        'mysql://database-02:3306' => 'Database 02',
      ]
```

### adminer_group

Group of the destination path

#### Default value

```YAML
adminer_group: www-data
```

### adminer_language

Install with single translation

#### Default value

```YAML
adminer_language:
```

### adminer_max_upload_size

Max allowed size for uploads/imports/dumps

#### Default value

```YAML
adminer_max_upload_size: 256M
```

### adminer_memory_limit

Max allowed memory to allocate by PHP

#### Default value

```YAML
adminer_memory_limit: 256M
```

### adminer_mysql

Install with mysql support only

#### Default value

```YAML
adminer_mysql: false
```

### adminer_mysql_packages

List of packages for mysql databases

#### Default value

```YAML
adminer_mysql_packages:
  - php
  - php-mysql
```

### adminer_owner

Owner of the destination path

#### Default value

```YAML
adminer_owner: www-data
```

### adminer_php_paths

Paths to write the custom PHP config to

#### Default value

```YAML
adminer_php_paths:
  - /etc/php/{{ adminer_php_versions[ansible_distribution_version] }}/apache2/conf.d/99-adminer.ini
  - /etc/php/{{ adminer_php_versions[ansible_distribution_version] }}/cli/conf.d/99-adminer.ini
  - /etc/php/{{ adminer_php_versions[ansible_distribution_version] }}/mods-available/adminer.ini
```

### adminer_php_versions

Mapping of the available PHP versions on Ubuntu

#### Default value

```YAML
adminer_php_versions:
  '18.04': 7.2
  '20.04': 7.4
  '22.04': 8.1
```

### adminer_version

Version of the release to install

#### Default value

```YAML
adminer_version: 4.8.1
```

## Discovered Tags

**_adminer_**


## Dependencies

- [rolehippie.apache](https://github.com/rolehippie/apache)

## License

Apache-2.0

## Author

[Thomas Boerger](https://github.com/tboerger)
