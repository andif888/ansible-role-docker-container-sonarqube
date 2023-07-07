# ansible-role-docker-container-sonarqube

Role to run sonarqube in a docker container

## Table of content

- [Default Variables](#default-variables)
  - [docker_container_sonarqube_comparisons](#docker_container_sonarqube_comparisons)
  - [docker_container_sonarqube_database_name](#docker_container_sonarqube_database_name)
  - [docker_container_sonarqube_database_password](#docker_container_sonarqube_database_password)
  - [docker_container_sonarqube_database_user](#docker_container_sonarqube_database_user)
  - [docker_container_sonarqube_env](#docker_container_sonarqube_env)
  - [docker_container_sonarqube_image](#docker_container_sonarqube_image)
  - [docker_container_sonarqube_labels](#docker_container_sonarqube_labels)
  - [docker_container_sonarqube_name](#docker_container_sonarqube_name)
  - [docker_container_sonarqube_networks](#docker_container_sonarqube_networks)
  - [docker_container_sonarqube_ports](#docker_container_sonarqube_ports)
  - [docker_container_sonarqube_restic_enable](#docker_container_sonarqube_restic_enable)
  - [docker_container_sonarqube_restic_retention](#docker_container_sonarqube_restic_retention)
  - [docker_container_sonarqube_restic_s3_bucket_name](#docker_container_sonarqube_restic_s3_bucket_name)
  - [docker_container_sonarqube_restic_s3_endpoint](#docker_container_sonarqube_restic_s3_endpoint)
  - [docker_container_sonarqube_restic_s3_repo](#docker_container_sonarqube_restic_s3_repo)
  - [docker_container_sonarqube_restic_s3_repo_access_key](#docker_container_sonarqube_restic_s3_repo_access_key)
  - [docker_container_sonarqube_restic_s3_repo_password](#docker_container_sonarqube_restic_s3_repo_password)
  - [docker_container_sonarqube_restic_s3_repo_secret_key](#docker_container_sonarqube_restic_s3_repo_secret_key)
  - [docker_container_sonarqube_restic_tag](#docker_container_sonarqube_restic_tag)
  - [docker_container_sonarqube_volume_dir](#docker_container_sonarqube_volume_dir)
  - [docker_container_sonarqube_volumes](#docker_container_sonarqube_volumes)
  - [docker_container_sonarqubedb_comparisons](#docker_container_sonarqubedb_comparisons)
  - [docker_container_sonarqubedb_env](#docker_container_sonarqubedb_env)
  - [docker_container_sonarqubedb_image](#docker_container_sonarqubedb_image)
  - [docker_container_sonarqubedb_labels](#docker_container_sonarqubedb_labels)
  - [docker_container_sonarqubedb_name](#docker_container_sonarqubedb_name)
  - [docker_container_sonarqubedb_networks](#docker_container_sonarqubedb_networks)
  - [docker_container_sonarqubedb_ports](#docker_container_sonarqubedb_ports)
  - [docker_container_sonarqubedb_volume_dir](#docker_container_sonarqubedb_volume_dir)
  - [docker_container_sonarqubedb_volumes](#docker_container_sonarqubedb_volumes)
  - [docker_image_sonarqube_name](#docker_image_sonarqube_name)
  - [docker_image_sonarqube_pull](#docker_image_sonarqube_pull)
  - [docker_image_sonarqubedb_name](#docker_image_sonarqubedb_name)
  - [docker_image_sonarqubedb_pull](#docker_image_sonarqubedb_pull)
  - [docker_network_sonarqube_name](#docker_network_sonarqube_name)
  - [docker_network_sonarqubedb_name](#docker_network_sonarqubedb_name)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### docker_container_sonarqube_comparisons

Allows to specify how properties of existing containers are compared with module options to decide whether the container should be recreated / updated or not.

#### Default value

```YAML
docker_container_sonarqube_comparisons:
  image: strict
  env: strict
  volumes: strict
```

### docker_container_sonarqube_database_name

Name of the database.

#### Default value

```YAML
docker_container_sonarqube_database_name: sonarqube
```

### docker_container_sonarqube_database_password

Password of the database user.

#### Default value

```YAML
docker_container_sonarqube_database_password: sonarqubesomethingsecret8888
```

### docker_container_sonarqube_database_user

Name of the database user.

#### Default value

```YAML
docker_container_sonarqube_database_user: sonarqube
```

### docker_container_sonarqube_env

Dictionery of key,value pairs for docker environment variables to configure sonarqube.

#### Default value

```YAML
docker_container_sonarqube_env:
  SONAR_JDBC_URL: jdbc:postgres://database:5432/{{ docker_container_sonarqube_database_name
    }}
  SONAR_JDBC_USERNAME: '{{ docker_container_sonarqube_database_user }}'
  SONAR_JDBC_PASSWORD: '{{ docker_container_sonarqube_database_password }}'
```

### docker_container_sonarqube_image

Repository path and tag used to create the container. If an image is not found or pull is true, the image will be pulled from the registry. If no tag is included, latest will be used.

#### Default value

```YAML
docker_container_sonarqube_image: '{{ docker_image_sonarqube_name }}'
```

### docker_container_sonarqube_labels

Dictionary of key value pairs for container labels.

Example:

```yaml

docker_container_sonarqube_labels:

traefik.enable: "true"

```

#### Default value

```YAML
docker_container_sonarqube_labels: {}
```

### docker_container_sonarqube_name

Name for the container

#### Default value

```YAML
docker_container_sonarqube_name: sonarqube
```

### docker_container_sonarqube_networks

List of networks the container belongs to.

#### Default value

```YAML
docker_container_sonarqube_networks:
  - name: '{{ docker_network_sonarqube_name }}'
    links:
      - '{{ docker_container_sonarqubedb_name }}:database'
```

### docker_container_sonarqube_ports

List of ports to publish from the container to the host.

#### Default value

```YAML
docker_container_sonarqube_ports:
  - 9000:9000
```

### docker_container_sonarqube_restic_enable

Enable restic backup for the container's mounted volumes.

#### Default value

```YAML
docker_container_sonarqube_restic_enable: false
```

### docker_container_sonarqube_restic_retention

Retention settions for `restic forget` after the `restic backup`.

#### Default value

```YAML
docker_container_sonarqube_restic_retention:
  keep_last: 1
  keep_daily: 7
  keep_weekly: 4
```

### docker_container_sonarqube_restic_s3_bucket_name

Minio S3 bucket name for restic backup storage.

#### Default value

```YAML
docker_container_sonarqube_restic_s3_bucket_name: restic-{{ docker_container_sonarqube_name
  }}
```

### docker_container_sonarqube_restic_s3_endpoint

Minio S3 endpoint for restic backup storage.

Example:

```yaml

docker_container__base__restic_s3_endpoint: "https://minio.{{ dns_domain }}"

docker_container_sonarqube_restic_s3_endpoint: "{{ docker_container__base__restic_s3_endpoint }}"

```

#### Default value

```YAML
docker_container_sonarqube_restic_s3_endpoint: '{{ docker_container__base__restic_s3_endpoint
  }}'
```

### docker_container_sonarqube_restic_s3_repo

Minio S3 repo URL for restic backup storage.

#### Default value

```YAML
docker_container_sonarqube_restic_s3_repo: s3:{{ docker_container_sonarqube_restic_s3_endpoint
  }}/{{ docker_container_sonarqube_restic_s3_bucket_name }}
```

### docker_container_sonarqube_restic_s3_repo_access_key

Minio S3 repo access key for restic backup storage.

#### Default value

```YAML
docker_container_sonarqube_restic_s3_repo_access_key: '{{ docker_container__base__restic_s3_repo_access_key
  }}'
```

### docker_container_sonarqube_restic_s3_repo_password

Minio S3 repo password for restic backup storage.

#### Default value

```YAML
docker_container_sonarqube_restic_s3_repo_password: '{{ docker_container__base__restic_s3_repo_password
  }}'
```

### docker_container_sonarqube_restic_s3_repo_secret_key

Minio S3 repo secret key for restic backup storage.

#### Default value

```YAML
docker_container_sonarqube_restic_s3_repo_secret_key: '{{ docker_container__base__restic_s3_repo_secret_key
  }}'
```

### docker_container_sonarqube_restic_tag

Tag for the `restic backup` command

#### Default value

```YAML
docker_container_sonarqube_restic_tag: '{{ docker_container_sonarqube_name }}'
```

### docker_container_sonarqube_volume_dir

Volume mount host directory, where Treafik config files are stored.

#### Default value

```YAML
docker_container_sonarqube_volume_dir: '{{ docker_container__base__volume_dir }}/{{
  docker_container_sonarqube_name }}'
```

### docker_container_sonarqube_volumes

List of volumes to mount within the container.

#### Default value

```YAML
docker_container_sonarqube_volumes:
  - '{{ docker_container_sonarqube_volume_dir }}/data:/opt/sonarqube/data'
  - '{{ docker_container_sonarqube_volume_dir }}/extensions:/opt/sonarqube/extensions'
  - '{{ docker_container_sonarqube_volume_dir }}/logs:/opt/sonarqube/logs'
```

### docker_container_sonarqubedb_comparisons

Allows to specify how properties of existing containers are compared with module options to decide whether the container should be recreated / updated or not.

#### Default value

```YAML
docker_container_sonarqubedb_comparisons:
  image: strict
  env: strict
  volumes: strict
```

### docker_container_sonarqubedb_env

Dictionery of key,value pairs for docker environment variables to configure sonarqubedb.

#### Default value

```YAML
docker_container_sonarqubedb_env:
  POSTGRES_USER: '{{ docker_container_sonarqube_database_user }}'
  POSTGRES_PASSWORD: '{{ docker_container_sonarqube_database_password }}'
  POSTGRES_DB: '{{ docker_container_sonarqube_database_name }}'
```

### docker_container_sonarqubedb_image

Repository path and tag used to create the container. If an image is not found or pull is true, the image will be pulled from the registry. If no tag is included, latest will be used.

#### Default value

```YAML
docker_container_sonarqubedb_image: '{{ docker_image_sonarqubedb_name }}'
```

### docker_container_sonarqubedb_labels

Dictionary of key value pairs for container labels.

Example:

```yaml

docker_container_sonarqubedb_labels:

traefik.enable: "true"

```

#### Default value

```YAML
docker_container_sonarqubedb_labels: {}
```

### docker_container_sonarqubedb_name

Name for the container

#### Default value

```YAML
docker_container_sonarqubedb_name: sonarqubedb
```

### docker_container_sonarqubedb_networks

List of networks the container belongs to.

#### Default value

```YAML
docker_container_sonarqubedb_networks:
  - name: '{{ docker_network_sonarqubedb_name }}'
```

### docker_container_sonarqubedb_ports

List of ports to publish from the container to the host.

#### Default value

```YAML
docker_container_sonarqubedb_ports: []
```

### docker_container_sonarqubedb_volume_dir

Volume mount host directory, where Treafik config files are stored.

#### Default value

```YAML
docker_container_sonarqubedb_volume_dir: '{{ docker_container__base__volume_dir }}/{{
  docker_container_sonarqube_name }}'
```

### docker_container_sonarqubedb_volumes

List of volumes to mount within the container.

#### Default value

```YAML
docker_container_sonarqubedb_volumes:
  - '{{ docker_container_sonarqube_volume_dir }}/postgres:/var/lib/postgresql'
```

### docker_image_sonarqube_name

Repository path and tag for the container image.

#### Default value

```YAML
docker_image_sonarqube_name: sonarqube:10-community
```

### docker_image_sonarqube_pull

Indicate to always pull the docker image.

#### Default value

```YAML
docker_image_sonarqube_pull: false
```

### docker_image_sonarqubedb_name

Repository path and tag for the container image.

#### Default value

```YAML
docker_image_sonarqubedb_name: postgres:12
```

### docker_image_sonarqubedb_pull

Indicate to always pull the docker image.

#### Default value

```YAML
docker_image_sonarqubedb_pull: false
```

### docker_network_sonarqube_name

Name of the docker network created for sonarqube.

#### Default value

```YAML
docker_network_sonarqube_name: '{{ docker_container_sonarqube_name }}_backend'
```

### docker_network_sonarqubedb_name

Name of the docker network created for sonarqubedb.

#### Default value

```YAML
docker_network_sonarqubedb_name: '{{ docker_container_sonarqube_name }}_backend'
```

## Discovered Tags

**_docker-container-backup-all_**\
&emsp;Backup all containers' volume mounts.

**_docker-container-backup-init-all_**\
&emsp;Run init backup task for all container.

**_docker-container-backup-init-sonarqube_**\
&emsp;Run init backup task for sonarqube if restic is enabled.

**_docker-container-backup-list-all_**\
&emsp;List all containers' backups.

**_docker-container-backup-list-sonarqube_**\
&emsp;List sonarqube backups.

**_docker-container-backup-sonarqube_**\
&emsp;Backup sonarqube volume mounts.

**_docker-container-prereq-all_**\
&emsp;Ensure all pre-requisites are installed

**_docker-container-prereq-sonarqube_**\
&emsp;Ensure all pre-requisites for sonarqube are installed

**_docker-container-purge-all_**\
&emsp;Remove all containers and delete volume mounts.

**_docker-container-purge-sonarqube_**\
&emsp;Remove sonarqube and delete volume mounts.

**_docker-container-remove-all_**\
&emsp;Remove all containers.

**_docker-container-remove-sonarqube_**\
&emsp;Remove sonarqube.

**_docker-container-restore-all_**\
&emsp;Run restic restore for all restic enabled containers.

**_docker-container-restore-sonarqube_**\
&emsp;Run restic restore for sonarqube if restic is enabled.

**_docker-container-setup-all_**\
&emsp;Run setup task for all containers.

**_docker-container-setup-sonarqube_**\
&emsp;Run setup task for sonarqube.

**_never_**


## Dependencies

None.

## License

license (GPL-2.0-or-later, MIT, etc)

## Author

andif888
