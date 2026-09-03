# 🚀 Laravel Docker Boilerplate (Plug & Play)

A production-ready, reusable, and lightweight Docker environment designed for Laravel developers. Spin up any new Laravel project instantly with a pre-configured multi-container architecture.

---

## 🌟 What's Included Inside? (Tech Stack)
This boilerplate integrates the following services via Docker Compose:
- **Application Server (`app`)**: PHP 8.2-FPM (with custom extensions: `pdo_mysql`, `mbstring`, `exif`, `pcntl`, `bcmath`, `gd`)
- **Web Server (`webserver`)**: Nginx (Alpine-based, pre-configured routing for Laravel)
- **Database (`db`)**: MySQL 8.0 (persistent data storage)
- **Database Management (`phpmyadmin`)**: phpMyAdmin GUI for easy database navigation

---

## 📂 Project Integration Guide (For New Projects)

### Step 1: Copy Docker Files
Copy the following items from this repository into the root directory of your new (or existing) Laravel project:
- `Dockerfile`
- `docker-compose.yml`
- `docker/` (folder containing Nginx configurations)

### Step 2: Configure Environment (`.env`)
Open your Laravel project's `.env` file and update your database credentials to match the Docker MySQL service:
```env
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel_db
DB_USERNAME=laravel_user
DB_PASSWORD=laravel_password

🛠️ Step-by-Step Commands & Workflow
1. Build and Run Docker Containers
Open your terminal in the project root directory and run the following command to build and start all services in the background:

Bash
sudo docker compose up -d --build
2. Check Docker Container Status
To verify whether all your Docker services are running properly and check their status, execute:

Bash
sudo docker compose ps
3. Accessing the Application Container
To run Laravel artisan commands, composer commands, or view files inside the container (laravel_app), run:

Bash
sudo docker exec -it laravel_app bash
(Once inside, your terminal path changes to root inside /var/www where you can run any command).

To exit the container terminal, simply type: exit.

4. Setting up Laravel Inside Container
Once you are inside the container (laravel_app), run these initial commands for a fresh project:

Bash
composer install
php artisan key:generate
php artisan migrate
🌐 Accessing Your Services
Laravel Web Application: http://localhost:8080

phpMyAdmin (Database GUI): http://localhost:8081

(Login using the database credentials defined in your docker-compose.yml or .env)

⚙️ Customization & Configuration
How to Change Database Name, Username, or Password?
If you want to change your database credentials:

Open docker-compose.yml and modify the environment variables under the db service:

YAML
environment:
  MYSQL_DATABASE: your_custom_db
  MYSQL_USER: your_custom_user
  MYSQL_PASSWORD: your_custom_password
Update the exact same credentials in your Laravel .env file (DB_DATABASE, DB_USERNAME, DB_PASSWORD).

Re-apply the changes by restarting Docker with a fresh build:

Bash
sudo docker compose down
sudo docker compose up -d --build
🔄 Upgrading PHP Version & Latest Laravel Support
If a newer Laravel version (e.g., Laravel 13) requires a newer PHP version (like PHP 8.3 or 8.4):

Open your Dockerfile.

Change the first line to your desired PHP version:

Dockerfile
FROM php:8.3-fpm
Rebuild and restart your containers:

Bash
sudo docker compose up -d --build
💡 Pro-Tips & Troubleshooting
File Permissions: If you ever face permission issues with storage or cache, run:

Bash
sudo chmod -R 777 storage bootstrap/cache
Port Conflicts: If port 8080 or 3306 is already occupied by another local service on your PC, you can change the left-side port mapping in docker-compose.yml (e.g., change "8080:80" to "9000:80").
