# moodle-docker-setup
**Introduction**

This guide provides step-by-step instructions for setting up Moodle on localhost using Docker. The installation uses Bitnami's Moodle and MariaDB images, with Docker networking for container communication.

**Prerequisites**

Ensure you have the following installed on your system:

[Docker](https://knowledgebase.aridhia.io/workspaces/analysing-data/virtual-machines/installing-software-on-virtual-machines/installing-docker-on-your-virtual-machine)

Docker Compose (optional)


**Step 1: Create a Docker Network**
Create a custom Docker network to enable communication between Moodle and MariaDB containers.

```docker network create moodle_network```

**Step 2: Deploy MariaDB Container**

Run the following command to start a MariaDB container with necessary environment variables:

```
docker run -d \
  --name mariadb \
  -e MARIADB_ROOT_PASSWORD=admin \
  -e MARIADB_USER=bn_moodle \
  -e MARIADB_PASSWORD=admin \
  -e MARIADB_DATABASE=bitnami_moodle \
  -e MARIADB_CHARACTER_SET=utf8mb4 \
  -e MARIADB_COLLATE=utf8mb4_unicode_ci \
  -v mariadb_data:/bitnami/mariadb \
  -p 3306:3306 \
  --network moodle_network \
  docker.io/bitnami/mariadb:latest
```
**Step 3: Deploy Moodle Container**

Run the following command to start a Moodle container and connect it to the MariaDB database:

```
docker run -d \
  --name moodle \
  --network moodle_network \
  -e MOODLE_DATABASE_HOST=mariadb \
  -e MOODLE_DATABASE_PORT_NUMBER=3306 \
  -e MOODLE_DATABASE_USER=bn_moodle \
  -e MOODLE_DATABASE_PASSWORD=admin \
  -e MOODLE_DATABASE_NAME=bitnami_moodle \
  -e ALLOW_EMPTY_PASSWORD=yes \
  -p 80:8080 \
  -p 443:8443 \
  -v moodle_data:/bitnami/moodle \
  -v moodledata_data:/bitnami/moodledata \
  docker.io/bitnami/moodle:4.5
```

**Step 4: Access Moodle**

Once the containers are running, access Moodle via your web browser:

```
http://0.0.0.0/
```

For HTTPS:
```
https://0.0.0.0/
```

User Id : user

Password : bitnami

**Conclusion**

You have successfully installed Moodle on localhost using Docker. You can now proceed with Moodle configuration and customization as needed.


