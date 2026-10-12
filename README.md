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
- **PostgreSQL:** Relational database used to store verification records.
- **Docker and Docker Compose:** Containerization and environment setup.
- **VirusTotal API v3:** External service used for URL security analysis.
- **IPInfo API:** External service used to retrieve information about IP addresses.

## Project Structure

The project uses Django as its web framework and includes application code, configuration files, dependency definitions, and supporting documentation.

- **`manage.py`:** Django's command-line entry point for administrative tasks, including running the development server and applying database migrations.
- **`Projeto/`:** Django project package containing project-level configuration. This package includes settings and URL configuration used to define how the application is configured and routed.
- **`app/`:** Application package containing the functionality implemented for SecureDash, including the code responsible for handling verification requests and interacting with the database and external services.
- **`requirements.txt`:** Lists the Python dependencies needed to install the application environment.
- **`dockerfile`:** Defines instructions for building the application's Docker image.
- **`docker-compose.yml`:** Defines the services and configuration used to run the application with Docker Compose.
- **`docs/`:** Contains screenshots documenting the application's interface.

The exact responsibilities of individual Python modules depend on their implementation. The principal components work together to receive user input, process requests, communicate with external APIs, and present results through the web interface.

## API Integration

SecureDash relies on two external APIs to provide its main features.

**VirusTotal API v3** is used to retrieve URL analysis information. The application submits or looks up URL information through the service and uses the available response to present the analysis to the user.

Website: https://www.virustotal.com/

**IPInfo API** is used to retrieve information associated with an IP address, including geographic and network-related details provided by the service.

Website: https://ipinfo.io/

Because these integrations depend on external services, API availability, rate limits, authentication, and response formats can affect the application's behavior.

## Database Design

PostgreSQL provides persistent storage for the application's verification history. Separating URL and IP records into related entities allows the application to organize different types of queries while maintaining a relational structure.

Database migrations are used to create and update the database schema. This approach makes database changes easier to manage during development.

## Installation and Execution

### Requirements

- Python 3.11
- PostgreSQL, if running without Docker
- Docker and Docker Compose, if using containers
- Valid API credentials for VirusTotal and IPInfo

### 1. Clone the repository

```bash
git clone https://github.com/Jonathan-atlas0/wsBackend-Fabrica26.1.git
cd wsBackend-Fabrica26.1
```

### 2. Create and activate a virtual environment

On Windows:

```bash
python -m venv venv
venv\Scripts\activate
```

On Linux or macOS:

```bash
python -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Configure the credentials required by the VirusTotal and IPInfo integrations using environment variables or an appropriate local configuration mechanism supported by the application.

Do not publish real API keys, tokens, database passwords, or other secrets in the source code or repository.

### 5. Configure PostgreSQL

Create a PostgreSQL database named `securedash` and configure the database connection in the Django settings according to your local environment.

When using Docker Compose, use the database service name and connection settings defined in the Compose configuration.

### 6. Apply migrations

```bash
python manage.py migrate
```

### 7. Start the development server

```bash
python manage.py runserver
```

Open the following address in your browser:

http://127.0.0.1:8000/

## Running with Docker

If the Docker Compose configuration is complete and properly configured, start the application with:

```bash
docker-compose up --build
```

Then access:

http://localhost:8000/

To stop the containers, press `Ctrl+C`. If you started them in detached mode, use:

```bash
docker-compose down
```

## Example Inputs for Testing

The following values can be used to explore the application's functionality. API results may vary depending on the service's current data and policies.

| Type | Example | Purpose |
|---|---|---|
| IP address | `1.178.29.0` | Explore IPInfo results |
| IP address | `1.1.1.1` | Explore information associated with Cloudflare |
| IP address | `177.66.0.1` | Test another IP address |
| URL | `https://www.google.com` | Check a commonly used website |
| URL | `http://testsafebrowsing.appspot.com/s/phishing.html` | Use a test URL intended for phishing-related checks |
| URL | `http://testsafebrowsing.appspot.com/s/malware.html` | Use a test URL intended for malware-related checks |

Use test URLs cautiously and follow the external service's usage policies.

## Application Endpoints

The following endpoints are documented for the application:

| Method | Endpoint | Description |
|---|---|---|
| GET/POST | `/` | Main page and URL verification |
| POST | `/ip/` | IP address lookup |
| POST | `/limpar/` | Clears verification history |
| GET/POST | `/editar/<id>/` | Edits a history record |

The available HTTP methods and exact behavior should match the application's URL configuration and view implementations.

## Design Decisions and Learning Outcomes

Django was selected as the foundation for the application because it provides a structured way to organize server-side logic, handle HTTP requests, integrate with relational databases, and render web pages.

Using external APIs allowed the project to provide IP information and URL security analysis without implementing those data sources from scratch. This introduced practical considerations involving API authentication, external dependencies, response handling, and service availability.

PostgreSQL was used to persist application data, while a relational model helped separate different categories of verification records. Docker was included to simplify environment setup and make the project easier to run consistently.

The project provided practical experience with backend development, API integration, relational databases, database migrations, containerization, and the coordination of different components in a web application.

## Use of Artificial Intelligence

Artificial intelligence tools were used as development assistants during the project. Their assistance included suggesting Django code organization practices, helping troubleshoot Docker and Docker Compose configuration, reviewing HTML and CSS, and improving project documentation.

The tools were used to support development rather than replace the author's responsibility for the project. The implementation and its behavior should be reviewed and understood by the author.

Relevant AI assistance should also be acknowledged in code comments, as required by the CS50x Final Project instructions.

## Author

**Jonathan Santos**

Developed as an academic project for Fábrica de Software 2026.1.
