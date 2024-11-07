## Redmine and MariaDB Docker Deployment
This Docker Compose configuration sets up a functional deployment of Redmine with a MariaDB database using Bitnami images. The Bitnami images were chosen for their flexibility, particularly for deploying plugins and customizing the environment.

## Prerequisites
Docker and Docker Compose must be installed on your server or local machine.

## Setup Instructions
1. Clone this repository to your desired directory.
2. In the docker-compose.yml file, update all placeholder values to enhance security and customize the environment. These include:
- MARIADB_ROOT_PASSWORD, MARIADB_USER, MARIADB_PASSWORD, and MARIADB_DATABASE for the MariaDB database configuration.
- REDMINE_DATABASE_USER, REDMINE_DATABASE_PASSWORD, and REDMINE_DATABASE_NAME for Redmine’s connection to the database.
- REDMINE_USERNAME, REDMINE_PASSWORD, and REDMINE_EMAIL to configure the initial Redmine admin account.
Note: Make sure to replace default passwords and usernames with secure values before deploying in a production environment.

## Usage
1. Start the services by running:

bash
Copier le code
 ```sh
docker-compose up -d
```

2. Access Redmine: Once the services are running, Redmine will be available at http://localhost or http://<your-server-ip> on port 80.

3. Data Persistence: The volumes specified in the docker-compose.yml file ensure that data persists across container restarts. You can also uncomment the backup volume for MariaDB if needed.

## Configuration Details
Services
- MariaDB: The MariaDB container stores data at mariadb_repos_to-store_data, and it’s configured to be secure by disabling empty passwords.
- Redmine: The Redmine container stores data at redmine_repos_to-store_data, which allows for data persistence and flexibility for plugin management.

## Networks
This setup uses a bridged network called redmine, isolating the services within a Docker network for secure internal communication.

## Install Plugin
Insure the docker Container is stoped

 ```sh
docker compose -f docker-compose.yml down
```
Place plugin folder on  the plugins folder

 ```sh
cp -r plugin_folder ${HOME}/**docker-compose-file-repo**/**redmine_repos_to-store_data**/plugins/
```
Start the docker Container
 ```sh
docker compose -f docker-compose.yml up -d
```


