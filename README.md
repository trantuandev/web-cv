# Web_CV_Group_4 - Recruitment & Job Search Platform

> A modern full-stack recruitment and job search web platform inspired by TopCV, connecting job seekers and recruiters seamlessly, securely, and efficiently.

---

## 📌 Overview

**Web_CV_Group_4** is a full-featured recruitment web portal developed as a mock project:
- **For Candidates:** Explore career opportunities filtered by industry/category, build and manage profiles, upload CVs, submit online job applications, and follow preferred companies.
- **For Recruiters:** Manage company profiles, publish and manage job postings, review applications, and evaluate submitted CVs.
- **For the System:** Secure authentication with Email OTP verification, JWT session handling, Role-Based Access Control (RBAC), and interactive Swagger API documentation.

---

## ✨ Key Features

### 👤 For Candidates (Job Seekers)
- **Secure Authentication:** Register and log in with Email OTP verification; password reset via email confirmation.
- **Profile & CV Management:** Create and update personal profiles, work experience, and upload/manage online CV files.
- **Job Discovery & Filtering:** Search job vacancies by keywords, categories, locations, and salary ranges.
- **Online Job Applications:** Apply directly to recruitments with attached CVs and track application history.
- **Follow & Bookmarking:** Follow favorite companies to receive updates and bookmark jobs for future reference.

### 🏢 For Recruiters & Companies
- **Company Profile Management:** Maintain company identity, including branding, logo, company overview, scale, and address.
- **Job Post Management:** Create, update, publish, and close job postings with detailed job descriptions, requirements, and benefits.
- **Applicant Tracking:** View candidates who applied to each posting, review submitted CVs, and update application statuses.

### ⚙️ System & Administration
- **Role-Based Access Control (RBAC):** Distinct permissions and workflows for `Candidate`, `Recruiter`, and `Admin` roles.
- **Automated Email Notifications:** Integrated SMTP service (powered by MailKit) for sending OTP codes, application notifications, and confirmations.
- **Interactive API Documentation:** Embedded Swagger UI for testing, exploring, and verifying backend endpoints.

---

## 🛠️ Technology Stack

### Frontend (Client)
- **Framework:** [Angular 19](https://angular.dev/) (Standalone Components, Reactive Architecture)
- **UI Components & Styling:** Angular Material, Angular CDK, Bootstrap / CSS
- **Rich Text Editor:** TinyMCE (`@tinymce/tinymce-angular`)
- **State & Networking:** RxJS, Angular HttpClient, JWT Decode, ngx-cookie-service

### Backend (Server)
- **Framework:** [ASP.NET Core 8 Web API](https://dotnet.microsoft.com/en-us/apps/aspnet) (.NET 8.0)
- **ORM:** Entity Framework Core 8.0 (Code-First Migration & Seed Data)
- **Authentication & Security:** JWT (JSON Web Token) Bearer Authentication, Password Hashing
- **Mailing Service:** MailKit & MimeKit (Gmail SMTP)
- **API Documentation:** Swagger / OpenAPI (Swashbuckle)

### Database
- **Database Engine:** Microsoft SQL Server

---

## 🚀 Installation & Local Development

### Prerequisites
1. **Node.js** (v18, v20 or newer) & **npm**
2. **.NET 8.0 SDK** or **Visual Studio 2022** (with *ASP.NET and web development* workload)
3. **Microsoft SQL Server** & **SQL Server Management Studio (SSMS)**

---

### Step 1: Clone Repository
```bash
git clone https://github.com/your-username/Web_CV_Group_4.git
cd Web_CV_Group_4
```

---

### Step 2: Database Configuration & Migration
1. Open [`Web_Sever/Web_Server/appsettings.json`](Web_Sever/Web_Server/appsettings.json) and verify/update your SQL Server connection string:
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=(local); Database=TopCVWeb; Uid=sa; Pwd=123; TrustServerCertificate=True;"
   }
   ```
   *(If using Windows Authentication, replace with: `Server=localhost; Database=TopCVWeb; Trusted_Connection=True; TrustServerCertificate=True;`)*

2. Apply Entity Framework migrations and seed initial data:
   - **Option A: Using .NET CLI**
     ```bash
     cd Web_Sever/Web_Server
     dotnet ef database update
     ```
   - **Option B: Using Visual Studio Package Manager Console**
     - Open solution `Web_Sever.sln`.
     - Go to: **Tools** > **NuGet Package Manager** > **Package Manager Console**.
     - Run:
       ```powershell
       Update-Database
       ```

---

### Step 3: Run the Backend (.NET 8 Web API)
- **Option A: Using Terminal**
  ```bash
  cd Web_Sever/Web_Server
  dotnet run --launch-profile https
  ```
- **Option B: Using Visual Studio 2022**
  - Open [`Web_Sever/Web_Sever.sln`](Web_Sever/Web_Sever.sln).
  - Set `Web_Server` as the startup project.
  - Select the `https` profile and press **F5** or **Ctrl + F5**.

Once running:
- **Swagger UI:** [https://localhost:7247/swagger](https://localhost:7247/swagger)
- **API Base URL:** `https://localhost:7247/api`

---

### Step 4: Run the Frontend (Angular 19)
1. Open a new terminal window and navigate to the `Web_Client` directory:
   ```bash
   cd Web_Client
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the Angular development server:
   ```bash
   npm start
   # or: npx ng serve
   ```

4. Open your browser and navigate to:
   - **Web Application:** [http://localhost:4200](http://localhost:4200)

---

## 📂 Project Structure

```text
Web_CV_Group_4/
├── Web_Client/                      # Frontend Application (Angular 19)
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/         # Shared & reusable UI components (Header, Footer, Navbar...)
│   │   │   ├── feature/            # Feature modules / application pages
│   │   │   │   ├── homepage/       # Landing page & featured recruitments
│   │   │   │   ├── loginpage/      # User authentication & OTP verification
│   │   │   │   ├── signuppage/     # Account registration
│   │   │   │   ├── profile/        # User profile & information management
│   │   │   │   ├── recruitment/    # Job listing, filtering & job detail view
│   │   │   │   ├── recruiter/      # Recruiter portal & job management
│   │   │   │   ├── company/        # Company list & company details
│   │   │   │   └── upload-cv/      # CV upload & management
│   │   │   ├── interceptors/       # HTTP Interceptors (JWT Bearer Token injection)
│   │   │   ├── models/             # TypeScript data models & interfaces
│   │   │   └── services/           # Angular Services for API communication
│   │   ├── assets/                 # Static assets (images, icons, etc.)
│   │   └── styles.css              # Global styles
│   ├── angular.json                # Angular CLI configuration
│   └── package.json                # Frontend package dependencies & scripts
│
├── Web_Sever/                       # Backend Solution (.NET 8 Web API)
│   ├── Web_Sever.sln               # Visual Studio Solution File
│   ├── TopCVWeb_Test/              # Test Project (Unit & Integration Tests)
│   └── Web_Server/                 # Main ASP.NET Core Project
│       ├── Controllers/            # API Controllers (Authentication, Recruitment, Company, CV...)
│       ├── Data/                   # DbContext & Database Seeding logic (SeedData)
│       ├── Interfaces/             # Contracts for Repositories & Services
│       ├── Migrations/             # EF Core database migration files
│       ├── Models/                 # Database entity models
│       ├── Repositories/           # Data Access Layer (Repository pattern)
│       ├── Services/               # Business logic services (Email, Auth, Recruitment...)
│       ├── ViewModels/             # Data Transfer Objects (DTOs / Request & Response models)
│       ├── appsettings.json        # Configuration file (Connection string, JWT, SMTP)
│       └── Program.cs              # Application setup, Dependency Injection & Middleware pipeline
│
└── README.md                       # Project documentation
```
