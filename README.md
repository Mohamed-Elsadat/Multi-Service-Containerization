# Project Title: Multi-Service Containerization

## Overview

This project demonstrates the containerization of multiple services for a seamless and efficient deployment. The services include:

1. **NGINX**: Used as a web service.
2. **Tomcat**: Runs a web application built using Maven.
3. **Git Repository**: Source code repository.
4. **MySQL**: Database service.
5. **Memcached**: Caching layer.
6. **RabbitMQ**: Message broker.

The setup leverages Docker to containerize these services and provides an environment for easy orchestration.

------

## Features

- **Modular Architecture**: Each service runs in its own container for isolation and scalability.
- **Automated Builds**: Maven is used to build the Tomcat application.
- **Persistent Storage**: MySQL data is stored persistently.
- **Efficient Caching**: Memcached reduces database load.
- **Messaging**: RabbitMQ handles asynchronous communication.

------

## Prerequisites

1. Docker and Docker Compose installed on your machine.
   - [Install Docker](https://docs.docker.com/get-docker/)
   - [Install Docker Compose](https://docs.docker.com/compose/install/)
2. At least **2 CPUs** and **4GB RAM** available for the containers.

------

## Setup Instructions

### Clone the Repository

```bash
git clone <repository_url>
cd <repository_directory>
```

### Build and Run Containers

1. **Build the Maven Project:**

   ```bash
   docker build -t maven-app ./maven-app
   ```

2. **Start All Services:**

   ```bash
   docker-compose up -d
   ```

------

## Configuration

### Environment Variables

- **MYSQL_ROOT_PASSWORD**: Set the MySQL root password.
- **RABBITMQ_DEFAULT_USER**: Set the RabbitMQ username.
- **RABBITMQ_DEFAULT_PASS**: Set the RabbitMQ password.

These can be configured in the `.env` file:

```env
MYSQL_ROOT_PASSWORD=yourpassword
RABBITMQ_DEFAULT_USER=guest
RABBITMQ_DEFAULT_PASS=guest
```

### Docker Compose File Structure

```yaml
version: '3.8'
services:
  nginx:
    image: nginx
    ports:
      - "8080:80"
    volumes:
      - ./nginx:/etc/nginx/conf.d

  tomcat:
    build:
      context: ./maven-app
    ports:
      - "8081:8080"

  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
    volumes:
      - mysql_data:/var/lib/mysql

  memcached:
    image: memcached
    ports:
      - "11211:11211"

  rabbitmq:
    image: rabbitmq:management
    ports:
      - "15672:15672"
      - "5672:5672"
    environment:
      RABBITMQ_DEFAULT_USER: ${RABBITMQ_DEFAULT_USER}
      RABBITMQ_DEFAULT_PASS: ${RABBITMQ_DEFAULT_PASS}

volumes:
  mysql_data:
```

------

## Accessing the Services

- **NGINX**: [http://localhost:8080](http://localhost:8080/)
- **Tomcat**: [http://localhost:8081](http://localhost:8081/)
- **RabbitMQ Management Console**: [http://localhost:15672](http://localhost:15672/)

------

## Notes

- Ensure that the `docker-compose.yml` file is correctly configured before running the services.

- Use the logs to debug any issues:

  ```bash
  docker-compose logs
  ```

------

## License

This project is licensed under the MIT License. See the LICENSE file for more details.

------

## Contributions

Contributions are welcome! Please fork the repository and submit a pull request for any enhancements or fixes.

------

## Author

[Your Name]
