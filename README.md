# moodle-docker-setup
**Introduction**

This guide provides step-by-step instructions for setting up Moodle on localhost using Docker. The installation uses Bitnami's Moodle and MariaDB images, with Docker networking for container communication.

**Prerequisites**

Ensure you have the following installed on your system:

Docker

Docker Compose (optional)


**Step 1: Create a Docker Network**
Create a custom Docker network to enable communication between Moodle and MariaDB containers.

```docker network create moodle_network```
