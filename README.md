# OMS 
A multi-user Order Management System starter: React/Vite + Java 21/Spring Boot + MySQL 8.

**Live demo:** https://order-management-system-pi-sable.vercel.app

> The backend runs on a free server that sleeps when idle, so the first load can take up to a minute.

## Requirements
Java 21, Maven 3.9+, Node 20+, MySQL 8.

## Database
```sql
CREATE DATABASE oms_db;
CREATE USER 'oms_user'@'localhost' IDENTIFIED BY 'choose-a-strong-private-password';
GRANT ALL PRIVILEGES ON oms_db.* TO 'oms_user'@'localhost';
```

## Start backend (PowerShell)
```powershell
cd backend
$env:DB_URL="jdbc:mysql://localhost:3306/oms_db"
$env:DB_USERNAME="oms_user"
$env:DB_PASSWORD="your-private-password"
$env:JWT_SECRET="replace-with-a-random-secret-at-least-32-characters-long"
mvn spring-boot:run
```
Backend: http://localhost:8080

## Start frontend (second terminal)
```powershell
cd frontend
npm install
npm run dev
```
Open the Local URL printed by Vite (usually http://localhost:5173).

The first account registered becomes ADMIN; subsequent accounts are EMPLOYEE. Employees see only orders they created; admins see all orders. This first-user bootstrap is convenient for local setup, but public deployment needs an invitation/approval process and careful admin provisioning.

## Included
- Signup/login with BCrypt password hashing and JWT bearer tokens
- ADMIN and EMPLOYEE roles
- Order creation/list/update/delete API (delete is admin-only)
- Modern responsive dashboard and AI assistant page
- Rule-based order assistant that answers questions about order counts, pending and delivered orders, and total sales from the database

## Before public deployment
This is a development starter, not a security-audited production system. Add email verification, password reset, rate limiting, audit logging, backups, monitoring, tests, database migrations, HTTPS, secure secret storage, and a reviewed registration/admin policy. Never commit secrets or expose the backend/database directly to the public internet.
