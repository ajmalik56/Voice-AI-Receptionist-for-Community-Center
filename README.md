# community-center-receptionist
This Node.js application demonstrates how to build a voice AI receptionist for a fictional community center.

The application uses Ultravox Realtime and Twilio. It handles both incoming and outgoing calls, with a specific focus on managing student lesson reminders and appointments. There are accompanying videos that go into detail about building the application:


## Highlights
The application includes:

1. Automated lesson reminder calls using voice AI
2. Calendar management integration with Cal.com
3. Student information database integration
4. Dynamic call routing and transfer capabilities
5. Multi-stage conversation management

## Prerequisites

- Node.js (v20 or higher)
- An Ultravox API key
- A Twilio account with:
  - Account SID
  - Auth Token
  - A phone number
- A Cal.com account with:
  - API key
  - Existing event type
- SQLite database (for student information)
- A way to expose your local server to the internet (e.g., ngrok)



```


4. Set up your database:
   - Place your students.csv file in the `data/` directory
   - The CSV should contain columns for: first_name, last_name, email, phone, emergency_contact, emergency_contact_phone

5. Start your server:
```bash
pnpm start
```

This application uses nodemon to provide automatic reloading if files are updated.

6. Expose your local server:
```bash
ngrok http 3000
```

7. Update your Twilio webhook:
   - Go to your Twilio phone number settings
   - Set the webhook URL for incoming calls to:
     `https://your-ngrok-url/twilio/incoming`
   - Set HTTP method to POST

## Key Features

### Incoming Call Handling
- Automatic connection to AI agent
- Natural language understanding
- Dynamic tool selection based on conversation context
- Call transfer capabilities to human agents

### Automated Reminder System
- Scheduled lesson reminders
- Integration with Cal.com calendar
- Student database lookup
- Emergency contact management
- Rescheduling capabilities
- Provides a GitHub Action (dailyreminders.yml) that will run daily to send reminders

### Call Management Tools
- Call transfer functionality
- Calendar availability checking
- Appointment booking/rescheduling
- Active call tracking

## Project Structure

```
├── index.js               # Main application entry point
├── db.js                  # Database configuration and operations
├── ultravox-config.js     # AI configuration and system prompts
├── ultravox-utils.js      # Utility functions for Ultravox API
├── .github/
│   ├── dailyreminders.yml # Daily job to send reminders
├── routes/
│   ├── twilio.js          # Call handling and Twilio integration
│   ├── cal.js             # Calendar operations and reminders
│   └── rag.js             # Knowledge base integration
└── data/
    └── students.csv       # Student information database
```

## API Endpoints

### Twilio Routes (/twilio)
- POST `/incoming` - Handle incoming calls
- POST `/transferCall` - Transfer active call
- GET `/active-calls` - List current active calls
- POST `/makeOutboundCall` - Initiate outbound call

### Calendar Routes (/cal)
- POST `/checkAvailability` - Check calendar availability
- POST `/createBooking` - Create new appointment
- GET `/upcomingBookings` - List upcoming appointments
- POST `/sendLessonReminders` - Process and send reminder calls

## Testing

### Manual Testing
1. Start the server and expose it via ngrok
2. Call your Twilio number to test incoming call handling
3. Use the `/cal/sendLessonReminders` endpoint to test reminder calls

### Expected Console Output
```
Server running on port 3000
Successfully imported X students
Incoming call received
Creating Ultravox call...
Got joinUrl: [URL]
Call initiated: [CallSID]
```



