# Project Overview

This project, named "Genesis," is a Laravel starter kit built on the **TALL Stack** (TailwindCSS, AlpineJS, Livewire, Laravel), along with **Volt** and **Folio**. It provides a robust foundation for building modern web applications with a focus on rapid development and a rich user experience.

Key features and technologies include:
*   **Laravel:** The core PHP framework for backend logic, routing, and more.
*   **TailwindCSS:** A utility-first CSS framework for rapid UI development.
*   **AlpineJS:** A rugged, minimal JavaScript framework for adding interactivity directly in your markup.
*   **Livewire:** A full-stack framework for Laravel that makes building dynamic interfaces simple, without leaving the comfort of PHP.
*   **Folio:** A page-based routing solution for Laravel, simplifying route definitions for views.
*   **Volt:** A Livewire extension that allows writing Livewire components as single-file components.
*   **Vite:** A fast frontend build tool for asset compilation (CSS and JavaScript).
*   **Docker:** Provides a containerized development environment for the application, database (MySQL), and web server (Nginx).

The project includes pre-built authentication pages, a dashboard, and profile management, leveraging Laravel's built-in features and the TALL stack components.

# Building and Running

## Prerequisites

Before running the project, ensure you have the following installed:

*   **PHP** (version 8.2 or higher)
*   **Composer**
*   **Node.js** and **npm** (or Yarn)
*   **Docker** and **Docker Compose** (if using the Docker-based setup)

## Local Development (without Docker)

1.  **Install PHP Dependencies:**
    ```bash
    composer install
    ```

2.  **Install Node.js Dependencies:**
    ```bash
    npm install
    ```

3.  **Build Frontend Assets:**
    ```bash
    npm run build
    ```

4.  **Copy Environment File:**
    ```bash
    cp .env.example .env
    ```

5.  **Generate Application Key:**
    ```bash
    php artisan key:generate
    ```

6.  **Create Database (if not already created) and Run Migrations:**
    Configure your database connection in the `.env` file, then run:
    ```bash
    php artisan migrate
    ```

7.  **Start Development Servers:**
    To run the Laravel backend and the Vite asset watcher concurrently:
    ```bash
    npm run dev
    ```
    Alternatively, you can run them separately:
    ```bash
    php artisan serve
    npm run dev
    ```

## Local Development (with Docker)

1.  **Build and Start Docker Containers:**
    ```bash
    docker-compose up -d --build
    ```

2.  **Install PHP Dependencies (inside app container):**
    ```bash
    docker-compose exec app composer install
    ```

3.  **Install Node.js Dependencies (inside app container):**
    ```bash
    docker-compose exec app npm install
    ```

4.  **Copy Environment File (inside app container):**
    ```bash
    docker-compose exec app cp .env.example .env
    ```

5.  **Generate Application Key (inside app container):**
    ```bash
    docker-compose exec app php artisan key:generate
    ```

6.  **Run Database Migrations (inside app container):**
    ```bash
    docker-compose exec app php artisan migrate
    ```

7.  **Access the Application:**
    The application should be accessible via your browser at `http://localhost:8000`.

## Testing

The project uses PHPUnit for testing.

1.  **Run all tests:**
    ```bash
    php artisan test
    ```
    or
    ```bash
    ./vendor/bin/phpunit
    ```

2.  **Run specific test suites:**
    *   Unit tests: `./vendor/bin/phpunit tests/Unit`
    *   Feature tests: `./vendor/bin/phpunit tests/Feature`

# Development Conventions

*   **TALL Stack:** The project heavily relies on TailwindCSS for styling, AlpineJS for frontend interactivity, Livewire for dynamic components, and Laravel for the backend.
*   **Page-based Routing (Folio):** Most of the application's routes are defined implicitly by the `.blade.php` files within the `resources/views/pages` directory.
*   **Single-File Livewire Components (Volt):** Livewire components are often written using Volt, allowing the PHP logic and Blade template to reside in a single file.
*   **Blade Components:** Reusable UI elements are implemented as Blade components, located in `resources/views/components`.
*   **Middleware:** Middleware is used to control access and behavior for routes and pages (e.g., `redirect-to-dashboard`, `auth`, `verified`).
*   **Asset Compilation (Vite):** Frontend assets (CSS and JavaScript) are managed and compiled using Vite.
*   **Dockerized Environment:** The `docker-compose.yml` file defines the recommended development environment, promoting consistency across development machines.
