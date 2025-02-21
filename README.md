# AI-Powered WhatsApp Reminder System

## Introduction
The **AI-Powered WhatsApp Reminder System** is a conversational AI application that allows users to set, update, delete, and receive reminders via WhatsApp. The system uses **Cohere's NLP model** to extract task details from natural language inputs and **Twilio's WhatsApp API** to send and receive messages. It is designed to be user-friendly, efficient, and scalable.

---

## Key Features
1. **Natural Language Processing (NLP)**:
   - Users can type reminders in natural language (e.g., "Remind me every month on the 3rd to pay the TV loan").
   - The system extracts task, frequency, date, and time using **Cohere's AI model**.
2. **Conversational Interface**:
   - Users can interact with the system via WhatsApp messages.
   - The system handles greetings, thank-you messages, and error responses.
3. **Reminder Management**:
   - Users can create, update, delete, and list reminders.
4. **Notifications**:
   - The system sends human-like reminder notifications via WhatsApp when the reminder time arrives.
5. **Relative Date Handling**:
   - The system supports relative dates like "today," "2 years," "this year," etc.

---

## Technical Stack
1. **Backend**:
   - **Flask**: A lightweight Python web framework for handling HTTP requests.
   - **SQLite**: A lightweight database for storing reminders.
2. **AI/NLP**:
   - **Cohere**: For extracting task details from natural language inputs.
3. **Messaging**:
   - **Twilio WhatsApp API**: For sending and receiving WhatsApp messages.
4. **Utilities**:
   - **Python-dateutil**: For handling relative dates.
   - **Threading**: For running background tasks (e.g., checking reminders).

---

## System Architecture
The system consists of the following components:

1. **Frontend**:
   - WhatsApp (user interface for interaction).
2. **Backend**:
   - Flask server (handles HTTP requests and business logic).
   - SQLite database (stores reminders).
3. **AI/NLP**:
   - Cohere API (extracts task details from user messages).
4. **Messaging**:
   - Twilio WhatsApp API (sends and receives WhatsApp messages).

---

## Workflow

### 1. User Interaction
- Users send WhatsApp messages to the Twilio Sandbox number.
- The Flask backend receives the message via a webhook.

### 2. Message Processing
- The backend processes the message based on its content:
  - **Greetings**: Responds with a welcome message.
  - **Thank You**: Responds with a thank-you message.
  - **Reminder Creation**: Extracts task details using Cohere and saves the reminder to the database.
  - **Reminder Deletion**: Deletes the specified reminder from the database.
  - **Reminder Update**: Updates the specified reminder with new details.
  - **List Reminders**: Sends a list of all reminders to the user.

### 3. Notification
- The backend checks reminders every minute.
- If a reminder's time matches the current time, the system sends a notification via WhatsApp.
- The notification message is generated using Cohere to make it human-like.

---

## Flow Diagram
![Alt text describing the image](https://github.com/Adhi-Git-hub/WhatsApp-Based-AI-Reminder-System/blob/main/whatsapp%20reminder.png)


---

## Detailed Flow

### 1. User Sends a Message
- The user sends a message to the Twilio Sandbox number (e.g., "Remind me every month on the 3rd to pay the TV loan").
- Twilio forwards the message to the Flask backend via a webhook.

### 2. Backend Processes the Message
- The backend identifies the type of message (greeting, reminder creation, deletion, etc.).
- For reminder creation:
  - The backend sends the message to Cohere for entity extraction.
  - Cohere returns the extracted task, frequency, date, and time.
  - The backend saves the reminder to the SQLite database.
- For reminder deletion:
  - The backend deletes the specified reminder from the database.
- For listing reminders:
  - The backend retrieves all reminders for the user and sends them via WhatsApp.

### 3. Notification
- The backend runs a background thread to check reminders every minute.
- If a reminder's time matches the current time:
  - The backend generates a human-like notification message using Cohere.
  - The notification is sent to the user via WhatsApp.

---

## Code Explanation

### 1. Flask Backend
- The Flask app handles incoming WhatsApp messages via the `/webhook` endpoint.
- It processes the message and performs the appropriate action (create, delete, update, or list reminders).

### 2. Cohere Integration
- The `extract_entities` function sends the user's message to Cohere and extracts task details.
- The `send_whatsapp_notification` function uses Cohere to generate a human-like reminder message.

### 3. Twilio Integration
- The `send_whatsapp_message` function sends messages to the user via Twilio's WhatsApp API.

### 4. Database
- The SQLite database stores reminders with the following fields:
  - `id`: Unique identifier for the reminder.
  - `task`: The task to be reminded.
  - `frequency`: The frequency of the reminder (e.g., daily, monthly).
  - `start_date`: The start date of the reminder.
  - `end_date`: The end date of the reminder.
  - `time`: The time of the reminder.
  - `user_number`: The user's WhatsApp number.

---

## Example Use Cases

### 1. Create Reminder
- **User**: "Remind me every day for 2 years to affix bio metric in hostel at 19:40."
- **Bot**: "Reminder set: affix bio metric in hostel at 19:40 on 2023-10-03."

### 2. Delete Reminder
- **User**: "Delete affix bio metric in hostel reminder."
- **Bot**: "Reminder for 'affix bio metric in hostel' has been deleted."

### 3. List Reminders
- **User**: "List all reminders."
- **Bot**: "Your reminders:\naffix bio metric in hostel at 19:40 on 2023-10-03."

### 4. Notification
- **Bot**: "Hey, don’t forget to affix your bio metric in hostel today at 19:40!"

---

## Challenges and Solutions
1. **Challenge**: Handling relative dates like "today," "2 years," etc.
   - **Solution**: Include the current date and time in the Cohere prompt and explicitly ask Cohere to handle relative dates.
2. **Challenge**: Generating human-like reminder messages.
   - **Solution**: Use Cohere to generate reminder messages based on the task details.
3. **Challenge**: Ensuring reminders are deleted correctly.
   - **Solution**: Use a precise SQL query to delete reminders based on the task name and user number.

---

## Future Enhancements
1. **Multi-Language Support**:
   - Add support for multiple languages using Cohere's multilingual capabilities.
2. **Advanced NLP**:
   - Use more advanced NLP models for better entity extraction.
3. **User Authentication**:
   - Add user authentication to support multiple users.
4. **Web Interface**:
   - Develop a web interface for managing reminders.

---

## Conclusion
The **AI-Powered WhatsApp Reminder System** is a powerful and user-friendly application that leverages AI and messaging APIs to simplify reminder management. It is designed to be scalable, efficient, and easy to use, making it ideal for personal and professional use cases.

---

## How to Run the Project
1. Install dependencies:
   ```bash
   pip install flask flask-cors twilio cohere python-dateutil
   python app.py
   ngrok http 5000
Update the Twilio Sandbox Webhook URL to point to your ngrok URL (e.g., https://your-ngrok-url.ngrok.io/webhook).
