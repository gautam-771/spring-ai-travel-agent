# AI Travel Agent & Customer Support using Spring AI

An interactive AI agent application built with **Java, Spring Boot, Spring AI, Ollama, and Thymeleaf**. This project demonstrates AI-powered travel assistance and e-commerce customer support using tool calling and conversational memory.

> **Learning project:** Based on [AI Agents using Spring AI & Thymeleaf](https://github.com/LearnCodeWithDurgesh/ai-agents-using-spring-ai) by LearnCodeWithDurgesh. I configured and tested the application with a locally running Ollama model as part of my Spring AI learning.

## Features

- **Travel Assistant:** Searches sample flights and hotels and accesses weather-related functionality through registered tools.
- **Customer Support:** Checks order status, cancels eligible orders, and checks product inventory.
- **AI Tool Calling:** Exposes Java methods to the language model using Spring AI's `@Tool` annotations.
- **Conversation Memory:** Uses `MessageWindowChatMemory` and a `Conversation-Id` header to maintain conversational context.
- **Interactive Chat Interface:** Uses Thymeleaf with Markdown rendering, suggested prompts, and chat-history functionality.
- **Local LLM:** Runs chat requests using Ollama and Qwen2.5 3B.

## Tech Stack

- Java 21
- Spring Boot 4.1.0
- Spring AI 2.0.0
- Ollama
- Qwen2.5 3B
- Thymeleaf
- Tailwind CSS
- Marked.js
- Maven
- Lombok

## Architecture

1. The user submits a message through the chat interface.
2. Spring Boot receives the request through the chat controller.
3. The chat service sends the prompt to Spring AI's `ChatClient`.
4. The model determines whether an available Java tool is needed.
5. Spring AI executes the selected tool when requested.
6. The response is returned to the user, with conversation memory maintained across requests.

## Project Structure

```text
ai-agents-using-spring-ai/
├── README.md
├── .gitignore
├── docs/
│   ├── prompt.md
│   └── understand.excalidraw
└── ai-agent-backend/
    ├── pom.xml
    ├── mvnw
    ├── mvnw.cmd
    └── src/
        └── main/
            ├── java/
            │   └── com/substring/agent/backend/
            │       ├── config/
            │       ├── controller/
            │       ├── service/
            │       ├── model/
            │       └── tools/
            └── resources/
                ├── templates/
                │   └── chat.html
                ├── application.yml
                └── application.properties
```

## Prerequisites

- Java 21
- Ollama installed and running
- Internet access for downloading the model initially
- Maven Wrapper included with the project

## Setup and Configuration

### 1. Download the model

```powershell
ollama pull qwen2.5:3b
```

### 2. Start Ollama

Ensure Ollama is running locally at `http://localhost:11434`.

### 3. Configure the application

In `ai-agent-backend/src/main/resources/application.yml`, configure the local model:

```yaml
server:
  port: 8081

spring:
  application:
    name: ai-agent-backend
  ai:
    ollama:
      base-url: http://localhost:11434
      chat:
        options:
          model: qwen2.5:3b
```

Retain any additional settings required by your local application.

### 4. Run the application

Open a terminal in the `ai-agent-backend` directory and execute:

```powershell
.\mvnw.cmd spring-boot:run
```

Alternatively, run the main application class from IntelliJ IDEA.

### 5. Open the chat interface

Visit [http://localhost:8081](http://localhost:8081).

## Registered Agent Tools

| Tool class | Method | Purpose |
|---|---|---|
| `FlightTools` | `searchFlight` | Searches predefined flights by route and date |
| `HotelTools` | `searchHotel` | Searches hotels by city and budget |
| `WeatherTools` | `getForecast` | Provides weather-related information |
| `OrderTools` | `getOrderStatus` | Checks an order's status |
| `OrderTools` | `cancelOrder` | Cancels an eligible order |
| `OrderTools` | `getOrderCount` | Returns the sample order count |
| `InventoryTools` | `checkStock` | Checks product availability |
| `InventoryTools` | `getAllProductsInStock` | Lists products in stock |

## Example Prompts

- "Plan a trip from Delhi to Goa and suggest a hotel within my budget."
- "Find flights from Delhi to Goa on 2026-08-21."
- "Check the weather information for Goa."
- "Can you check the status of order 1042?"
- "Check whether a product is available in inventory."

## Limitations

- Flight search uses predefined sample data and does not provide live airline availability or real-time ticket prices.
- Sample flight records include the date `2026-08-21`; this date is in the past.
- Results from other tools depend on their implementations and configured data sources.
- Tool-based workflows require a model that supports tool calling.

## Key Learning Outcomes

- Configuring a local LLM with Ollama in Spring AI
- Understanding `ChatClient` and AI tool calling
- Registering Java methods as AI tools
- Maintaining conversation history using `MessageWindowChatMemory`
- Integrating an AI model with a Spring Boot application
- Running and testing a Thymeleaf-based chat interface

## Acknowledgements

Thanks to [LearnCodeWithDurgesh](https://github.com/LearnCodeWithDurgesh/ai-agents-using-spring-ai) for the original project and tutorial.

This repository is maintained as a learning and experimentation project, including local Ollama configuration and testing.
