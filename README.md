# FoodRescue: Bridging the Gap Between Food Surplus and Need

![Project Logo]()

FoodRescue is an innovative mobile application designed to address the critical challenge of food waste while combating food insecurity through efficient resource redistribution and community engagement.

## Table of Contents

- [Overview](#overview)
- [Software Architecture](#software-architecture)
- [Technical Stack](#technical-stack)
- [Project Structure](#project-structure)
- [Implementation Guide](#implementation-guide)
- [Features](#features)
- [Getting Started](#getting-started)
- [Contributing](#contributing)
- [Team](#team)

## Overview

FoodRescue addresses the global challenge where one-third of food production is wasted while millions face hunger. Our platform creates an efficient digital ecosystem connecting food surplus holders with those in need.

## Software Architecture
![Software Architecture](https://github.com/user-attachments/assets/72415312-164f-4d38-8015-eaec3b2812c3)

Our application follows a modern, layered architecture:

### Backend (Spring Boot)
1. **Security Layer**
   - Security Configuration
   - JWT Authentication
   
2. **REST API Layer**
   - REST Controllers
   - Global Error Handler
   - DTOs (Data Transfer Objects)

3. **Business Logic Layer**
   - Services
   - Domain Models

4. **Persistence Layer**
   - Data Access Layer
   - CRUD Operations
   - Database Management

### Mobile Application
1. **State Management**
   - ViewModels
   - LiveData

2. **UI Layer**
   - Activities & Fragments
   - User Interface Components

3. **Data Layer**
   - LiveData & Repository
   - Local Data Management

4. **Network Layer**
   - API Client
   - HTTP/HTTPS Communication

## Technical Stack

### Backend
```xml
<!-- Spring Boot Dependencies -->
<dependencies>
    <!-- Spring Boot Starter -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
    <!-- Spring Security -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    
    <!-- JWT -->
    <dependency>
        <groupId>io.jsonwebtoken</groupId>
        <artifactId>jjwt</artifactId>
        <version>0.9.1</version>
    </dependency>
    
    <!-- JPA -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    
    <!-- Database -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
    </dependency>
</dependencies>
```

### Mobile Application Structure
```gradle
dependencies {
    // ViewModel and LiveData
    implementation "androidx.lifecycle:lifecycle-viewmodel:2.7.0"
    implementation "androidx.lifecycle:lifecycle-livedata:2.7.0"
    
    // Room for local database
    implementation "androidx.room:room-runtime:2.6.1"
    annotationProcessor "androidx.room:room-compiler:2.6.1"
    
    // Retrofit for API calls
    implementation "com.squareup.retrofit2:retrofit:2.9.0"
    implementation "com.squareup.retrofit2:converter-gson:2.9.0"
    
    // Android UI Components
    implementation "androidx.recyclerview:recyclerview:1.3.2"
    implementation "com.google.android.material:material:1.11.0"
}
```

## Project Structure

### Backend Structure
```
src/main/java/com/foodrescue/
├── config/
│   ├── SecurityConfig.java
│   └── JwtConfig.java
├── controller/
│   ├── AuthController.java
│   ├── FoodOfferController.java
│   └── UserController.java
├── service/
│   ├── UserService.java
│   └── FoodOfferService.java
├── model/
│   ├── User.java
│   ├── FoodOffer.java
│   └── Location.java
├── repository/
│   ├── UserRepository.java
│   └── FoodOfferRepository.java
└── security/
    ├── JwtTokenProvider.java
    └── UserDetailsServiceImpl.java
```

### Mobile App Structure
```
app/src/main/java/com/foodrescue/
├── ui/
│   ├── activities/
│   ├── fragments/
│   └── adapters/
├── viewmodel/
│   ├── UserViewModel.java
│   └── FoodOfferViewModel.java
├── repository/
│   ├── UserRepository.java
│   └── FoodOfferRepository.java
├── data/
│   ├── local/
│   └── remote/
└── network/
    └── ApiClient.java
```

## Implementation Guide

### 1. Backend Security Configuration
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    
    @Autowired
    private JwtTokenProvider jwtTokenProvider;
    
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .cors().and().csrf().disable()
            .authorizeRequests()
            .antMatchers("/api/auth/**").permitAll()
            .anyRequest().authenticated()
            .and()
            .addFilterBefore(new JwtTokenFilter(jwtTokenProvider),
                UsernamePasswordAuthenticationFilter.class);
    }
}
```

### 2. Mobile ViewModel Implementation
```java
public class FoodOfferViewModel extends ViewModel {
    private final MutableLiveData<List<FoodOffer>> foodOffers;
    private final FoodOfferRepository repository;
    
    public FoodOfferViewModel() {
        foodOffers = new MutableLiveData<>();
        repository = new FoodOfferRepository();
    }
    
    public LiveData<List<FoodOffer>> getFoodOffers() {
        return foodOffers;
    }
    
    public void loadFoodOffers() {
        repository.getFoodOffers()
            .subscribe(offers -> foodOffers.setValue(offers));
    }
}
```

## Features

- User Authentication with JWT
- Food Offer Management
- Geolocation Services
- Real-time Updates
- Message System
- Offer Matching

## Getting Started

### Prerequisites
- JDK 11 or later
- MySQL 5.7+
- Android Studio 4.0+
- Maven or Gradle

### Backend Setup
```bash
# Clone the repository
git clone https://github.com/yourusername/foodrescue.git

# Navigate to backend directory
cd foodrescue/backend

# Build the project
mvn clean install

# Run the application
mvn spring-boot:run
```

### Mobile App Setup
```bash
# Navigate to mobile directory
cd foodrescue/mobile

# Build the project
./gradlew build

# Run tests
./gradlew test
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Team

- Mohamed Amine EL MASKYNE ([Email](mailto:mohamedamine.elmaskyne@gmail.com))
- Mohamed LACHGAR
- Abdellah EL GHARBI ([Email](mailto:abdellah.elgharbi2002@gmail.com))
