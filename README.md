# SecureDash — Web Security Dashboard

#### Video Demo: PENDING

#### Description:

SecureDash is a web application developed as an academic project for Fábrica de Software 2026.1. Its main purpose is to provide a centralized interface for performing basic security-related checks on IP addresses and URLs. The application integrates external APIs to retrieve information about IP addresses and analyze URLs for potential malicious activity.

The project was developed using Python and Django, with HTML and CSS for the user interface, PostgreSQL for relational data storage, and Docker for containerization. The application demonstrates the integration of external services, server-side request processing, database operations, and the organization of a web application using the Django framework.

## Features

### 1. IP Finder

The IP Finder allows users to submit an IPv4 address and retrieve information about it through the IPInfo API. This feature helps users inspect information associated with an IP address, such as its approximate geographic location and other details returned by the API.

The application sends the submitted address to the external service and presents the returned information through its interface. The accuracy and availability of the results depend on the external API.

### 2. Link Checker

The Link Checker allows users to submit a URL for security analysis using the VirusTotal API v3. The application communicates with the service to obtain information about the submitted URL and its potential association with malicious content or phishing.

This feature demonstrates how an application can integrate an external security service to support URL analysis. The results depend on the information available through VirusTotal and should not be interpreted as an absolute guarantee that a URL is safe or malicious.

### 3. Verification History

SecureDash stores records of verification requests in its database. Users can review previous checks, edit records, and clear the history through the application's interface.

Keeping a history allows users to revisit previous queries instead of relying exclusively on the results displayed immediately after each request.

### 4. Relational Database

The application uses PostgreSQL to persist verification data. Its data model separates URL-related and IP-related queries into two related entities, helping organize records according to the type of verification performed.

Django's database functionality and migrations are used to manage the application's database structure.

### 5. Containerization

Docker and Docker Compose are provided to facilitate application setup and execution. Containerization helps make the development environment more consistent and reduces differences between machines with different local configurations.

## Technologies Used

- **Python 3.11:** Main programming language.
- **Django 6.0.3:** Web framework used to handle requests, application logic, routing, and database integration.
- **HTML and CSS:** User interface structure and styling.
- **PostgreSQL:** Rel
