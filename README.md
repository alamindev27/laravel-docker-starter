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
```

# 🛠️ Step-by-Step Commands & Workflow

### Step 1: Build and Run Docker Containers
Open your terminal in the project root directory and run the following command to build and start all services in the background:

```bash
sudo docker compose up -d --build
```

### Step 2: Check Docker Status (Running or Not?)
To check whether your containers are currently running and healthy, execute:

```bash
sudo docker compose ps
```

### Step 3. Restart Docker Containers
If you need to restart all your services at any time, run:

```bash
sudo docker compose restart
```

(আর যদি সম্পূর্ণ বন্ধ করে আবার চালু করতে চান, তবে `sudo docker compose down` দিয়ে আবার `sudo docker compose up -d` দিতে পারেন).

### Step 4. Accessing the Application Container (To Run Laravel Commands)
To enter inside the running application container (`laravel_app`) and run Laravel artisan or composer commands, execute:

```bash
sudo docker exec -it laravel_app bash
```

(Once you enter the container, your terminal path will be `/var/www`. From there, you can run the commands below.)

To exit the container, simply type:

```bash
exit
```

### Step 5. Running Laravel Commands Inside Container
Once you are inside the container (`laravel_app`), run your necessary Laravel commands:

```php
composer install
php artisan key:generate
php artisan migrate
```

## 🌐 Accessing Your Services

- Laravel Web Application: [`http://localhost:8080`](http://localhost:8080)
- phpMyAdmin (Database GUI): [`http://localhost:8081`](http://localhost:8081)

(Login using the database credentials defined in your `docker-compose.yml` or `.env`)

## ⚙️ Customization & Configuration

### How to Change Database Name, Username, or Password?
If you want to change your database credentials:

Step 1. Open docker-compose.yml and modify the environment variables under the db service:

```yml
environment:
  MYSQL_DATABASE: your_custom_db
  MYSQL_USER: your_custom_user
  MYSQL_PASSWORD: your_custom_password
  ```

 Step 2. Update the exact same credentials in your Laravel `.env` file (`DB_DATABASE`, `DB_USERNAME`, `DB_PASSWORD`).

 Step 3. Re-apply the changes by restarting Docker with a fresh build:

 ```bash
sudo docker compose down
sudo docker compose up -d --build
```

## 🔄 Upgrading PHP Version & Latest Laravel Support
If a newer Laravel version (e.g., Laravel 13) requires a newer PHP version (like PHP 8.3 or 8.4):

Step 1. Open your `Dockerfile`.

Step 2. Change the first line to your desired PHP version:

```dockefile
FROM php:8.3-fpm
```

Step 3. Rebuild and restart your containers:

```bash
sudo docker compose up -d --build
```

## 💡 Pro-Tips & Troubleshooting

### 1. Fix Storage & Cache Permission Errors
If you ever face permission denied issues with Laravel storage or cache folders, run this command in your project root:

```bash
sudo chmod -R 777 storage bootstrap/cache
```

### 2. Port Conflicts Issue
If port `8080` or `3306` is already occupied by another local service on your PC, you can change the left-side port mapping in your `docker-compose.yml` file (e.g., change `"8080:80"` to `"9000:80"`).



### 3. Permission start.sh file
```bash
chmod +x start.sh start.sh
```
