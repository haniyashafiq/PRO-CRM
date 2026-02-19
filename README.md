# PRO-CRM: Professional Rehabilitation & Outreach CRM System

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Flask](https://img.shields.io/badge/Flask-2.0+-green.svg)](https://flask.palletsprojects.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-brightgreen.svg)](https://www.mongodb.com/cloud/atlas)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A comprehensive Customer Relationship Management (CRM) system designed specifically for healthcare facilities, rehabilitation centers, and outreach programs. The system provides robust patient management, financial tracking, canteen operations, and administrative oversight capabilities.

---

## 📋 Table of Contents

- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Documentation](#-api-documentation)
- [Deployment](#-deployment)
- [Database Schema](#-database-schema)
- [Security](#-security)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### 🔐 Authentication & User Management

- Secure user authentication with encrypted passwords
- Role-based access control (Admin, Staff, etc.)
- Password reset functionality via email
- Session management with expiration
- Initial admin user auto-creation

### 👥 Patient Management

- Complete patient record keeping (demographics, contact info, admission details)
- Session notes and medical records tracking
- Patient history and timeline tracking
- Patient status management (Active, Discharged)
- Advanced search and filtering capabilities

### 💰 Financial Management

- Automated monthly fee calculation with prorated billing
- Comprehensive payment tracking and history
- Balance calculation (Outstanding dues)
- Expense tracking (Incoming & Outgoing)
- Multiple payment categories support
- Financial dashboard with real-time analytics

### 🍽️ Canteen Operations

- Daily canteen sales tracking per patient
- Monthly canteen reports and summaries
- Sales history and breakdown
- Daily canteen sheet generation
- Old balance management
- Automated canteen-overhead synchronization

### 📊 Overhead Management

- Daily overhead expense tracking
- Monthly overhead summaries
- Annual overhead reports
- Kitchen, canteen, and miscellaneous expense categories
- Profit/loss calculations
- Staff advance tracking

### 📈 Dashboard & Analytics

- Real-time statistics and KPIs
- Patient admission trends
- Financial overview (Expected balance, collections)
- Active patient count
- Monthly admission charts
- Customizable date range filtering

### 📄 Reporting & Export

- Export patient data to Excel
- Payment records export
- Discharge bill generation
- Canteen sales reports
- Custom financial reports

---

## 🛠️ Technology Stack

### Backend

- **Framework:** Flask 2.0+
- **Database:** MongoDB Atlas (Cloud NoSQL Database)
- **ODM:** Flask-PyMongo
- **Authentication:** Werkzeug Security, itsdangerous
- **Email:** SMTP with Gmail integration

### Frontend

- **HTML5/CSS3** with modern responsive design
- **JavaScript (ES6+)** for dynamic interactions
- **Vanilla JS** (No heavy frameworks - lightweight & fast)

### Data Processing

- **Pandas & Openpyxl** for Excel export functionality

### Deployment

- **Platform:** Vercel
- **WSGI:** Gunicorn

---

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.8 or higher**
- **pip** (Python package installer)
- **MongoDB Atlas account** (or local MongoDB instance)
- **Gmail account** with App Password (for email functionality)
- **Git** (for version control)

---

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/PRO-CRM.git
cd PRO-CRM
```

### 2. Create Virtual Environment

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables

Create a `.env` file in the root directory:

```bash
# Windows
copy .env.example .env

# macOS/Linux
cp .env.example .env
```

Edit the `.env` file with your configuration (see [Configuration](#-configuration) section).

### 5. Initial Database Setup

The application will automatically:

- Connect to MongoDB on first run
- Create necessary collections
- Initialize the default admin user: `ImranSaab` / `password123`

---

## ⚙️ Configuration

### Environment Variables

Create a `.env` file in the project root with the following variables:

```env
# MongoDB Configuration
MONGO_URI="mongodb+srv://username:password@cluster.mongodb.net/database_name?retryWrites=true&w=majority"

# Flask Security
SECRET_KEY="your-super-secret-key-change-this-in-production"

# Email Configuration (Gmail)
GMAIL_USER="your-email@gmail.com"
GMAIL_APP_PASSWORD="your-16-digit-app-password"

# Optional Settings
PASSWORD_RESET_EXPIRY_MINUTES=30
ADMIN_EMAIL="admin@example.com"
```

### Gmail App Password Setup

1. Enable 2-Factor Authentication on your Gmail account
2. Go to [Google App Passwords](https://myaccount.google.com/apppasswords)
3. Generate a new app password for "Mail"
4. Copy the 16-digit password to `GMAIL_APP_PASSWORD`

### MongoDB Atlas Setup

1. Create a free account at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster
3. Set up database user credentials
4. Whitelist your IP address (or use `0.0.0.0/0` for all IPs)
5. Copy the connection string to `MONGO_URI`
6. Replace `<password>` with your database user password
7. Replace `<database_name>` with your preferred database name (e.g., `pro_crm`)

---

## 💻 Usage

### Running Locally

1. **Activate Virtual Environment** (if not already activated):

   ```bash
   # Windows
   venv\Scripts\activate

   # macOS/Linux
   source venv/bin/activate
   ```

2. **Start the Application**:

   ```bash
   python app.py
   ```

3. **Access the Application**:
   - Open your browser and navigate to: `http://127.0.0.1:5000`

4. **Default Login Credentials**:

   ```
   Username: ImranSaab
   Password: password123
   ```

   ⚠️ **Important:** Change the default password immediately after first login!

### First-Time Setup Checklist

- [ ] Change default admin password
- [ ] Create additional user accounts
- [ ] Configure email settings
- [ ] Test password reset functionality
- [ ] Add initial patient records
- [ ] Set up monthly fee structures
- [ ] Configure canteen pricing

---

## 📡 API Documentation

### Authentication Endpoints

| Method | Endpoint            | Description               | Authentication |
| ------ | ------------------- | ------------------------- | -------------- |
| POST   | `/api/auth/login`   | User login                | None           |
| POST   | `/api/auth/logout`  | User logout               | Required       |
| POST   | `/api/auth/forgot`  | Request password reset    | None           |
| POST   | `/api/auth/reset`   | Reset password with token | None           |
| GET    | `/api/auth/session` | Get current session info  | Required       |

### Patient Management

| Method | Endpoint                            | Description             | Role Required |
| ------ | ----------------------------------- | ----------------------- | ------------- |
| GET    | `/api/patients`                     | List all patients       | Any           |
| POST   | `/api/patients`                     | Create new patient      | Admin         |
| PUT    | `/api/patients/<id>`                | Update patient          | Admin         |
| DELETE | `/api/patients/<id>`                | Delete patient          | Admin         |
| GET    | `/api/patients/<id>/discharge-bill` | Generate discharge bill | Any           |

### Financial Operations

| Method | Endpoint                | Description           | Role Required |
| ------ | ----------------------- | --------------------- | ------------- |
| GET    | `/api/expenses`         | List expenses         | Any           |
| POST   | `/api/expenses`         | Add expense/payment   | Admin         |
| DELETE | `/api/expenses/<id>`    | Delete expense        | Admin         |
| GET    | `/api/expenses/summary` | Financial summary     | Any           |
| POST   | `/api/export`           | Export financial data | Admin         |

### Canteen Management

| Method | Endpoint                       | Description         | Role Required |
| ------ | ------------------------------ | ------------------- | ------------- |
| POST   | `/api/canteen/sales`           | Record canteen sale | Staff         |
| GET    | `/api/canteen/sales/breakdown` | Sales breakdown     | Any           |
| GET    | `/api/canteen/daily-sheet`     | Daily canteen sheet | Any           |
| GET    | `/api/canteen/monthly-table`   | Monthly summary     | Any           |
| POST   | `/api/canteen/daily-entry`     | Bulk daily entry    | Staff         |

### Dashboard & Analytics

| Method | Endpoint                        | Description          | Role Required |
| ------ | ------------------------------- | -------------------- | ------------- |
| GET    | `/api/dashboard`                | Dashboard statistics | Any           |
| GET    | `/api/dashboard/admissions`     | Admission trends     | Any           |
| GET    | `/api/overheads/<month>/<year>` | Monthly overheads    | Admin         |
| GET    | `/api/overheads/annual/<year>`  | Annual overheads     | Admin         |

For detailed request/response examples, see the [API Reference Documentation](docs/API.md).

---

## 🚀 Deployment

### Deploying to Vercel

This application is configured for Vercel deployment.

1. **Install Vercel CLI**:

   ```bash
   npm install -g vercel
   ```

2. **Login to Vercel**:

   ```bash
   vercel login
   ```

3. **Configure Environment Variables**:
   - Go to your Vercel project settings
   - Add all environment variables from `.env`

4. **Deploy**:

   ```bash
   vercel --prod
   ```

5. **Verify Deployment**:
   - Check the provided URL
   - Test login functionality
   - Verify database connection

### Deploying to Render

Render provides a straightforward deployment process for Python web applications.

1. **Create a Render Account**:
   - Sign up at [render.com](https://render.com)

2. **Connect Your Repository**:
   - Link your GitHub/GitLab repository to Render
   - Or use the Render dashboard to connect

3. **Create a New Web Service**:
   - Click "New +" and select "Web Service"
   - Choose your repository
   - Configure the following settings:

4. **Build Configuration**:

   ```yaml
   Name: pro-crm
   Environment: Python 3
   Build Command: pip install -r requirements.txt
   Start Command: gunicorn app:app
   ```

5. **Configure Environment Variables**:
   - Go to "Environment" tab in your Render service
   - Add all environment variables from `.env`:
     - `MONGO_URI`
     - `SECRET_KEY`
     - `GMAIL_USER`
     - `GMAIL_APP_PASSWORD`
     - `PASSWORD_RESET_EXPIRY_MINUTES`
     - `ADMIN_EMAIL`

6. **Deploy**:
   - Click "Create Web Service"
   - Render will automatically build and deploy your application
   - Deployment typically takes 2-5 minutes

7. **Verify Deployment**:
   - Access your app at `https://your-app-name.onrender.com`
   - Test login functionality
   - Verify database connection

8. **Optional - Custom Domain**:
   - Go to "Settings" → "Custom Domain"
   - Add your domain and configure DNS settings

#### Render-Specific Considerations

- **Free Tier**: Applications on free tier may spin down after inactivity (cold starts)
- **Automatic Deploys**: Enable auto-deploy from your main branch
- **Health Checks**: Render automatically monitors your application health
- **Logs**: Access real-time logs from the Render dashboard
- **Scaling**: Easily scale to paid plans for better performance

### Configuration Files

- **vercel.json**: Vercel deployment configuration
- **requirements.txt**: Python dependencies (used by both Vercel and Render)
- **.env**: Environment variables (not committed to Git)

---

## 🗄️ Database Schema

### Collections

#### `users`

- `username` (String, Unique)
- `password` (String, Hashed)
- `role` (String: Admin, Staff)
- `name` (String)
- `email` (String)
- `created_at` (DateTime)

#### `patients`

- `name` (String)
- `fatherName` (String)
- `cnic` (String)
- `contact` (String)
- `address` (String)
- `monthlyFee` (String/Number)
- `admissionDate` (DateTime)
- `dischargeDate` (DateTime, Optional)
- `status` (String: Active, Discharged)
- `receivedAmount` (Number)
- `laundryStatus` (Boolean)
- `sessionNotes` (Array)
- `medicalRecords` (Array)

#### `canteen_sales`

- `patient_id` (ObjectId)
- `patient_name` (String)
- `amount` (Number)
- `description` (String)
- `date` (DateTime)
- `recorded_by` (String)

#### `expenses`

- `type` (String: incoming, outgoing)
- `category` (String)
- `amount` (Number)
- `description` (String)
- `date` (DateTime)
- `auto` (Boolean)
- `patient_name` (String)

#### `overheads`

- `month` (Number: 1-12)
- `year` (Number)
- `entries` (Array of daily expenses)

---

## 🔒 Security

### Implemented Security Measures

- ✅ **Password Hashing**: Werkzeug's generate_password_hash with salt
- ✅ **Session Management**: Secure Flask sessions with secret key
- ✅ **CSRF Protection**: Built-in Flask CSRF tokens
- ✅ **SQL Injection Prevention**: MongoDB ODM parameterized queries
- ✅ **XSS Prevention**: Input sanitization and output encoding
- ✅ **Role-Based Access Control**: Decorator-based permission system
- ✅ **Secure Password Reset**: Time-limited tokens with email verification
- ✅ **Environment Variables**: Sensitive data stored in .env
- ✅ **HTTPS Ready**: SSL/TLS support for production

### Security Best Practices

1. **Change Default Credentials**: Immediately after installation
2. **Use Strong SECRET_KEY**: Generate cryptographically secure key
3. **Regular Backups**: Schedule MongoDB Atlas automatic backups
4. **Update Dependencies**: Keep all packages up to date
5. **Monitor Logs**: Review application logs regularly
6. **Limit Access**: Use IP whitelisting for administrative functions
7. **Enable 2FA**: For all administrative accounts

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Built with ❤️ for healthcare professionals**
