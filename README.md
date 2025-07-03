# Webhook Receiver Application

This repo contains the Spring Boot backend (and optional UI) to handle incoming webhook events.

## Features

- Receives GitHub webhooks (Push, PR, etc.)
- Parses JSON payload
- Logs or stores webhook event data
- (Optional) Displays status via a simple UI

## Running the App

```bash
mvn spring-boot:run
# or
./gradlew bootRun
