# Ajarly Backend 🏠

[![Java](https://img.shields.io/badge/Java-17-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.0-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue.svg)](https://www.mysql.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A comprehensive backend system for rental and vacation home platforms built with Java Spring Boot. Ajarly provides a robust, scalable solution for property management, booking workflows, payment processing, and administrative controls.

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [API Documentation](#-api-documentation)
- [Configuration](#-configuration)
- [Database Schema](#-database-schema)
- [Security](#-security)
- [Deployment](#-deployment)
- [Testing](#-testing)
- [Contributing](#-contributing)
- [Authors](#-authors)
- [License](#-license)

## ✨ Features

### Core Features
- 🔐 **Authentication System** - JWT-based secure authentication with role-based access control
- 🏘️ **Property Management** - Complete CRUD operations with advanced search and filtering
- 📸 **Image Management** - Cloudinary integration for property photos
- 📅 **Booking System** - Real-time availability checking and calendar management
- ⭐ **Reviews & Ratings** - User feedback system with owner responses
- ❤️ **Favorites/Wishlist** - Save and manage favorite properties

### Advanced Features
- 👤 **User Profile Management** - Profile updates, avatar upload, phone verification
- 💳 **Payment Integration** - Fawry payment gateway integration
- 💎 **Premium Subscriptions** - Subscription plans for property owners
- 📊 **Analytics & Insights** - Comprehensive performance metrics
- 🛡️ **Admin Dashboard** - Platform management and moderation tools
- 🚨 **Reports & Moderation** - Content reporting and dispute resolution

## 🛠️ Tech Stack

### Backend Framework
- **Java 17** - Programming language
- **Spring Boot 3.2.0** - Application framework
- **Spring Data JPA** - Data persistence
- **Spring Security 6.2.0** - Security framework
- **JWT (JJWT 0.12.3)** - Token-based authentication

### Database
- **MySQL 8.0** - Primary database
- **H2 Database** - In-memory database for testing

### Cloud Services
- **Cloudinary** - Image storage and CDN
- **Fawry** - Payment gateway

### Build Tools
- **Maven** - Dependency management
- **Lombok** - Code generation
- **dotenv-java** - Environment variable management

## 🚀 Getting Started

### Prerequisites

- Java 17 or higher
- Maven 3.6+
- MySQL 8.0+
- Git

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/ajarly-backend.git
cd ajarly-backend
```

2. **Create MySQL database**
```sql
CREATE DATABASE ajarly_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

3. **Configure environment variables**

Create a `.env` file in the root directory:

```env
# Database
DB_URL=jdbc:mysql://localhost:3306/ajarly_db
DB_USERNAME=your_db_username
DB_PASSWORD=your_db_password

# JWT
JWT_SECRET=your_super_secret_jwt_key_min_256_bits
JWT_EXPIRATION=86400000

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Fawry Payment Gateway
FAWRY_MERCHANT_CODE=your_merchant_code
FAWRY_SECURITY_KEY=your_security_key
FAWRY_BASE_URL=https://atfawry.fawrystaging.com
```

4. **Build the project**
```bash
mvn clean install
```

5. **Run the application**
```bash
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

### Quick Start with Docker

```bash
# Build and run with Docker Compose
docker-compose up -d

# View logs
docker-compose logs -f backend
```

## 📁 Project Structure

```
ajarly-backend/
├── src/
│   ├── main/
│   │   ├── java/com/ajarly/backend/
│   │   │   ├── config/          # Configuration classes
│   │   │   ├── controller/      # REST API controllers
│   │   │   ├── dto/             # Data Transfer Objects
│   │   │   ├── model/           # Entity models
│   │   │   ├── repository/      # JPA repositories
│   │   │   ├── service/         # Business logic
│   │   │   ├── security/        # Security configuration
│   │   │   └── util/            # Utility classes
│   │   └── resources/
│   │       ├── application.properties
│   │       └── .env.example
│   └── test/                    # Test files
├── pom.xml                      # Maven configuration
├── Dockerfile                   # Docker configuration
├── docker-compose.yml           # Docker Compose setup
└── README.md
```

## 📚 API Documentation

### Base URL
```
http://localhost:8080/api/v1
```

### Authentication Endpoints

#### Register User
```http
POST /api/v1/auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePass123!",
  "firstName": "John",
  "lastName": "Doe",
  "phoneNumber": "+201234567890",
  "role": "USER"
}
```

#### Login
```http
POST /api/v1/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePass123!"
}
```

### Property Endpoints

#### Get All Properties
```http
GET /api/v1/properties?city=Cairo&minPrice=100&maxPrice=300&page=0&size=20
Authorization: Bearer {token}
```

#### Create Property
```http
POST /api/v1/properties
Authorization: Bearer {token}
Content-Type: application/json

{
  "title": "Modern Apartment in Downtown",
  "description": "Spacious 2-bedroom apartment...",
  "propertyType": "APARTMENT",
  "city": "Cairo",
  "bedrooms": 2,
  "bathrooms": 1,
  "maxGuests": 4,
  "pricePerNight": 150.00
}
```

### Booking Endpoints

#### Create Booking
```http
POST /api/v1/bookings
Authorization: Bearer {token}
Content-Type: application/json

{
  "propertyId": 1,
  "checkInDate": "2025-02-01",
  "checkOutDate": "2025-02-05",
  "numberOfGuests": 2
}
```

For complete API documentation, see [API_DOCUMENTATION.md](docs/API_DOCUMENTATION.md)

## ⚙️ Configuration

### Application Properties

Key configuration options in `application.properties`:

```properties
# Server
server.port=8080
server.servlet.context-path=/api/v1

# Database
spring.datasource.url=${DB_URL}
spring.jpa.hibernate.ddl-auto=validate
spring.jpa.show-sql=false

# JWT
jwt.secret=${JWT_SECRET}
jwt.expiration=${JWT_EXPIRATION}

# File Upload
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB
```

### Security Configuration

- **JWT Token Expiration**: 24 hours (configurable)
- **Password Encryption**: BCrypt (strength: 12)
- **CORS**: Configurable allowed origins
- **Rate Limiting**: Implemented for API endpoints

## 🗄️ Database Schema

### Core Tables

- **users** - User accounts and profiles
- **properties** - Property listings
- **bookings** - Booking records
- **reviews** - User reviews and ratings
- **transactions** - Payment records
- **property_images** - Property photographs
- **amenities** - Available amenities
- **favorites** - User wishlists

### Entity Relationships

```
User (1) -------- (N) Property
User (1) -------- (N) Booking
Property (1) ---- (N) Booking
Booking (1) ----- (1) Transaction
Booking (1) ----- (1) Review
Property (N) ---- (N) Amenity
```

For complete database schema, see [DATABASE_SCHEMA.md](docs/DATABASE_SCHEMA.md)

## 🔒 Security

### Authentication Flow
1. User registers/logs in with credentials
2. Server validates credentials
3. JWT token generated and returned
4. Client includes token in Authorization header
5. Server validates token on each request

### Authorization Levels
- **USER**: Basic access, can book properties
- **LANDLORD**: Can create and manage properties
- **ADMIN**: Full platform access and moderation

### Security Best Practices
- Passwords hashed with BCrypt
- JWT tokens for stateless authentication
- Role-based access control (RBAC)
- Input validation and sanitization
- CORS configuration
- SQL injection prevention via JPA

## 🐳 Deployment

### Docker Deployment

```bash
# Build image
docker build -t ajarly-backend .

# Run container
docker run -p 8080:8080 \
  -e DB_URL=jdbc:mysql://host.docker.internal:3306/ajarly_db \
  -e DB_USERNAME=root \
  -e DB_PASSWORD=password \
  -e JWT_SECRET=your_secret \
  ajarly-backend
```

### Production Deployment

1. Set `spring.jpa.hibernate.ddl-auto=validate`
2. Configure production database connection
3. Set secure JWT secret (256+ bits)
4. Enable HTTPS/TLS
5. Configure proper CORS origins
6. Set up database backups
7. Implement logging and monitoring
8. Configure rate limiting

## 🧪 Testing

### Run All Tests
```bash
mvn test
```

### Run Specific Test Class
```bash
mvn test -Dtest=PropertyServiceTest
```

### Integration Tests
```bash
mvn verify
```

### Test Coverage
```bash
mvn jacoco:report
```

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Coding Standards
- Follow Java naming conventions
- Write meaningful commit messages
- Add unit tests for new features
- Update documentation as needed
- Follow existing code style

## 👥 Authors

- **Tarek Mohamed** - Backend Developer
- **Malak Kamal** - Backend Developer
- **Ayman Mohamed** - Backend Developer

## 📞 Contact

For questions or support, please contact:
- Email: support@ajarly.com
- Issues: [GitHub Issues](https://github.com/yourusername/ajarly-backend/issues)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Spring Boot team for the excellent framework
- Cloudinary for image hosting services
- Fawry for payment gateway integration
- All contributors and supporters

---

**⭐ If you find this project helpful, please give it a star!**

Made with ❤️ by the Ajarly Team
