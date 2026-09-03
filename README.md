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