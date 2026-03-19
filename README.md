# 📓 Journal App (Spring Boot)

A full‑stack backend project built with **Spring Boot**, designed to manage personal journal entries and provide advanced features like sentiment analysis, scheduled email notifications, Kafka messaging, and Redis caching.

---

## 🚀 Features

- **User Management**
  - Register and manage users
  - Secure authentication and authorization with Spring Security

- **Journal Entries**
  - Create, update, delete, and view personal journal entries
  - Store metadata like date, sentiment, and user association

- **Sentiment Analysis**
  - Automatic sentiment tagging of journal entries
  - Weekly aggregation of user sentiment
  - Kafka producer publishes weekly sentiment summaries
  - Kafka consumer triggers email notifications

- **Email Notifications**
  - Integrated with Gmail SMTP
  - Sends weekly sentiment summaries to users
  - Uses Google App Password for secure authentication

- **Caching**
  - Redis integration for fast lookups and reduced DB load
  - Scheduled cache clearing every hour

- **Scheduler**
  - Weekly scheduled task to analyze user journals and send sentiment summaries
  - Hourly scheduled task to refresh Redis cache

- **Cloud Integrations**
  - Kafka cluster hosted on Confluent Cloud
  - Redis hosted on Redis Cloud
  - MongoDB Atlas for persistent storage

---

## 🛠️ Tech Stack

- **Backend Framework**: Spring Boot
- **Database**: MongoDB Atlas
- **Cache**: Redis Cloud
- **Messaging**: Apache Kafka (Confluent Cloud)
- **Email**: Gmail SMTP
- **Build Tool**: Maven

---

## ⚙️ Configuration

Set up your `application.yml` with the following:

```yaml
spring:
  mail:
    host: smtp.gmail.com
    port: 587
    username: <your-email>
    password: <your-16-char-app-password>
    properties:
      mail.smtp.auth: true
      mail.smtp.starttls.enable: true

  redis:
    host: <redis-host>
    port: <redis-port>
    password: <redis-password>

  kafka:
    bootstrap-servers: <confluent-bootstrap-server>
    producer:
      key-serializer: org.apache.kafka.common.serialization.StringSerializer
      value-serializer: org.springframework.kafka.support.serializer.JsonSerializer
    consumer:
      group-id: weekly-sentiment-group
      key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
      value-deserializer: org.springframework.kafka.support.serializer.JsonDeserializer
      properties:
        spring.json.trusted.packages: net.engineeringdigest.journalApp.model
    properties:
      security.protocol: SASL_SSL
      sasl.mechanism: PLAIN
      sasl.jaas.config: org.apache.kafka.common.security.plain.PlainLoginModule required username='<api-key>' password='<api-secret>';
      session.timeout.ms: 45000
📅 Scheduled Jobs
Weekly Sentiment Analysis  
Runs every Sunday at 9 AM, aggregates journal entries, publishes sentiment data to Kafka, and sends email notifications.

Hourly Cache Refresh  
Clears and reinitializes Redis cache every hour.

▶️ Running the Project
Clone the repo:

bash
git clone https://github.com/IMashokkadayat/Journal.git
cd Journal
Configure application.yml with your credentials.

Build and run:

bash
mvn clean install
mvn spring-boot:run
📬 Future Enhancements
REST API endpoints for external integrations

Frontend UI for journal management

Dockerization and Kubernetes deployment

Enhanced analytics dashboards

👨‍💻 Author
Developed by Ashok Kadayat  
B.Tech Computer Science, Maharishi University of Information Technology

Code

---

This README gives a professional overview of your project, highlights all the integrations (Kafka, Redis, MongoDB, Email), and provides setup instructions.  

Do you want me to also add **example API endpoints** (like `/journal/add`, `/journal/list`, `/user/register`) so anyone cloning your repo can immediately see how to interact with it?
