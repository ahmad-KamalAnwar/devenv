# News Aggregator devenv

The purpose of this repo is to have a single place dev environment to build and deploy applications locally. It contains a docker-compose file which combines all relevant apps as services.

## Prerequisites

Make sure you have the following utilities installed locally on your machine.

- Docker

## Setup

Please follow the steps below to setup news_aggregator application locally.

1. Clone devenv repo.
2. Goto devenv directory `cd devenv`.
3. Clone the repositories inside the devenv directory.
    1. [news-aggregator-backend](https://github.com/ahmad-KamalAnwar/news-aggregator-backend)
    2. [news-aggregator-frontend](https://github.com/ahmad-KamalAnwar/news-aggregator)
4. For frontend app copy the .env file and rename to .env.local.
5. For backend app copy the .env.example file, rename to .env and adjust the environment variables if needed otherwise use the default values.
6. Create localhost aliases (in /etc/hosts file) as per API endpoints given in the .env files of frontend apps. Copy the below line and paste it to your /etc/hosts file.
    1. 127.0.0.1	aggregator.local
7. Copy docker-compose.yml.dist file from the root of devenv directory and rename it to docker-compose.yml.
8. Open up docker-compose.yml file apply the following changes if not done already.
    1. Change the ports section to 3309:3306 under `db` services in case of port conflict, you can choose any other port.
    2. Similarly, as mentioned in above points if you change any port in docker-compose.yml then accordingly adjust it in .env.local files of all frontend apps too.
9. Now from the root of devenv directory run this command `docker-compose build`, it will build all services and might take some time depending on the internet speed.
10. Once the build is successful, you can either run `docker-compose up` for running frontend/backend applications at once or run individual services using following commands as per your need
    1. `docker-compose up db` this is mandatory to run admin, connect and scheduling
    2. `docker-compose up api_news_aggregator` for running backend
    3. `docker-compose up news_aggregator` for running connect backend, should already be running with `api_news_aggregator`
11. Once the relevant front/backend services are up & running, you can accesss the apps in the browser using following URLs
    1. http://localhost:3005 for frontend
    2. http://localhost:7005 for backend application

## Notes

- You can use the following command to ssh into any relevant container for package install/update/remove or exploring files.
    - `docker-compose exec [container-name] sh`
- Whenever there is a change in .env file either front or backend you would need to restart the relevant service container.
- To import data contact me for API Keys, put them in your env and run the following commands:
  1. `docker-compose up api_news_aggregator` to ssh in the backend's container
  2. Now run this in container, `php artisan import:articles`
