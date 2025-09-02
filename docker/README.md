# Docker Setup Documentation

This document explains how to set up and run the Laravel application using Docker.

## Prerequisites

Before you begin, ensure you have the following installed on your machine:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/thedevdojo/genesis
   ```

2. **Navigate to the project directory:**

   ```bash
   cd genesis
   ```

3. **Build and start the Docker containers:**

   ```bash
   docker-compose up -d --build
   ```

## Usage

- **Access the application:**

  Once the containers are running, you can access the application in your web browser at [http://localhost:8000](http://localhost:8000).

- **Running Artisan Commands:**

  You can run any `php artisan` command by executing it inside the `app` container. For example, to run migrations:

  ```bash
  docker-compose exec app php artisan migrate
  ```

## Services

The Docker Compose setup consists of the following services:

- **`app`**: This service runs the Laravel application using PHP-FPM.
- **`db`**: This service runs a MySQL 8.0 database.
- **`nginx`**: This service acts as a web server and proxies requests to the `app` service.

## Troubleshooting

### Vite Manifest Not Found Error

If you encounter a "Vite manifest not found" error, it means the frontend assets have not been built. You can resolve this by running the following commands inside your `app` container:

```bash
docker-compose exec app npm install
docker-compose exec app npm run build
```

### File Permission Issues

If you experience file permission errors, especially with the `public/build` directory or other generated files, ensure that commands like `npm install` and `npm run build` are executed with the correct user permissions within the Docker container. You can run them as the `www-data` user:

```bash
docker-compose exec app sudo -u www-data npm install
docker-compose exec app sudo -u www-data npm run build
```

You might also need to adjust file ownership if issues persist:

```bash
docker-compose exec app chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache
```

### Strange Output in Views (Folio/Volt)

Sometimes, due to issues with Laravel Folio or Volt, you might see unusual line numbers or strange output directly in your browser views. This can often be resolved by clearing the compiled views:

```bash
docker-compose exec app php artisan view:clear
```