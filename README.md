# FoodRescue: Bridging the Gap Between Food Surplus and Need

<div style="display: flex; justify-content: center; align-items: center;">
    <img src="https://github.com/user-attachments/assets/b09cd7d7-3d50-4099-bc54-c81fa0296b88" alt="Project Logo" width="400" height="400" style="margin-right: 10px;"/>
    <img src="https://github.com/user-attachments/assets/4047a52a-de75-4592-affe-60a4aeb5a3d4" alt="Project Logo" width="400" height="600"/>
</div>

FoodRescue is an innovative mobile application designed to address the critical challenge of food waste while combating food insecurity through efficient resource redistribution and community engagement.

## Table of Contents

- [Overview](#overview)
- [Software Architecture](#software-architecture)
- [Technical Stack](#technical-stack)
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
## Docker Image
```
version: '3.8'

services:
  app:
    container_name: chek-app-1
    build:
      context: .
    ports:
      - "8090:8090"
    depends_on:
      - db
    environment:
      SPRING_DATASOURCE_URL: jdbc:mysql://mysql-container:3306/df
      SPRING_DATASOURCE_USERNAME: root
      SPRING_DATASOURCE_PASSWORD: password
    networks:
      - chek_app-network

  db:
    image: mysql:5.7
    container_name: mysql-container
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: df
    ports:
      - "3307:3306"
    networks:
      - chek_app-network

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: phpmyadmin-container
    environment:
      PMA_HOST: mysql-container
      MYSQL_ROOT_PASSWORD: password
    ports:
      - "8081:80"
    networks:
      - chek_app-network

networks:
  chek_app-network:
    driver: bridge  # Retiré 'external: true' pour permettre la création du réseau

```
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
## Features

- User Authentication with JWT
- Food Offer Management
- Geolocation Services
- Real-time Updates
- Offer Matching

## Getting Started

Certainly! Here are step-by-step instructions to set up and run your project locally:

### Prerequisites:

1. *Git:*
   - Make sure you have Git installed. If not, download and install it from [git-scm.com](https://git-scm.com/).

2. *XAMPP:*
   - Install XAMPP from [apachefriends.org](https://www.apachefriends.org/).
   - Start the Apache and MySQL servers in XAMPP.
   - Ensure MySQL is using port 3306.


### Backend Setup:

1. *Clone the Project:*
   bash
   git clone <repository_url>
   cd <project_folder>
   

2. *Install Backend Dependencies:*
   - Open a terminal in the backend project folder.
   - Run the following commands:
     bash
     mvn clean install
     

3. *Run Backend:*
   - Start your XAMPP Apache and MySQL servers.
   - Run the Spring Boot application. The database and entities will be created automatically.
   - Verify that the backend is running by visiting [http://localhost:8090](http://localhost:8090) in your browser.


## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Team

- Mohamed Lachgar ([Researchgate](https://www.researchgate.net/profile/Mohamed-Lachgar))
- Mohamed Amine EL MASKYNE ([Email](mailto:mohamedamine.elmaskyne@gmail.com))
- Abdellah EL GHARBI ([Email](mailto:abdellah.elgharbi2002@gmail.com))
