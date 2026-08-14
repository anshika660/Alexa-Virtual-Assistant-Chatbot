Synthesia — Voice-Controlled Virtual Assistant

A Python-based voice assistant with a Flask web interface, speech recognition, text-to-speech, web automation, Wikipedia search, jokes, and real-time assistant status updates.

Overview

Synthesia is a voice-controlled virtual assistant built with Python. The application listens to spoken commands through the system microphone, converts speech into text, processes the command, and responds using text-to-speech.

The project also includes a Flask web layer with Flask-SocketIO, allowing assistant speaking status to be emitted to the frontend in real time.

Key Features

🎙️ Voice command recognition using Google Speech Recognition

🔊 Text-to-speech responses using pyttsx3

👋 Wake-word activation using "Hey Synthesia"

🎵 YouTube music/video playback using pywhatkit

🕒 Current time information

😂 Random programming jokes

📚 Wikipedia-based person/information lookup

🌤️ Weather lookup using OpenWeatherMap API

🌐 Flask-based web interface

⚡ Real-time speaking-status updates using Flask-SocketIO

🧵 Background assistant execution using Python threading

🎤 Ambient-noise calibration for microphone input

Technology Stack

Backend

Technology

Purpose

Python 3.11

Core programming language

Flask

Web application/backend framework

Flask-SocketIO

Real-time communication between backend and frontend

Threading

Runs the voice assistant alongside the Flask application

SpeechRecognition

Converts spoken audio into text

PyAudio

Captures microphone audio

pyttsx3

Offline text-to-speech engine

Requests

HTTP requests to external APIs

Wikipedia API/library

Retrieves Wikipedia summaries

PyJokes

Generates programming jokes

PyWhatKit

YouTube playback/web automation

datetime

Current date/time functionality

OpenWeatherMap API

Weather information

Frontend

The project contains a templates directory and a static directory, indicating a Flask-served web frontend.

HTML templates

Static frontend assets

Flask-SocketIO client-side communication for assistant status updates

Architecture

                    ┌──────────────────────┐
                    │      User Voice      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      Microphone      │
                    │       PyAudio        │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ SpeechRecognition    │
                    │  Google Recognition  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Command Processing   │
                    │       Python         │
                    └──────────┬───────────┘
                               │
              ┌────────────────┼─────────────────┐
              ▼                ▼                 ▼
        ┌──────────┐    ┌─────────────┐   ┌─────────────┐
        │ Wikipedia│    │ OpenWeather │   │  PyWhatKit  │
        └──────────┘    └─────────────┘   └─────────────┘
              │                │                 │
              └────────────────┼─────────────────┘
                               ▼
                    ┌──────────────────────┐
                    │     pyttsx3 TTS      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Spoken Response   │
                    └──────────────────────┘

             Flask + Flask-SocketIO
                    │
                    ▼
             Web Interface

Supported Voice Commands

Wake Word

Hey Synthesia

Activates the assistant and starts command processing.

Time

What is the time?

Returns the current system time.

Music / Video

Play some music
Play [song/video name]

Uses PyWhatKit to open/play the requested content on YouTube.

Jokes

Tell me a joke

Returns a programming joke using PyJokes.

Information Search

Who is Albert Einstein?

Uses Wikipedia to retrieve a short summary.

Weather

What is the weather?

The assistant asks for a city name and retrieves the current temperature using the OpenWeatherMap API.

Stop

Stop

Stops the assistant loop.

Project Structure

Alexa-FlaskAPI/
│
├── flask-alexa 1.py       # Main assistant application
├── flask-alexa.py         # Alternate/previous application version
├── README.md              # Project documentation
│
├── templates/             # Flask HTML templates
│   └── alexa.html
│
├── static/                # Static frontend assets
│
├── venv/                  # Python virtual environment
│
└── alexa-flask-env/       # Older project environment

Installation

1. Clone the repository

git clone <YOUR_GITHUB_REPOSITORY_URL>
cd Alexa-FlaskAPI

2. Create a virtual environment

python -m venv venv

3. Activate the environment

Windows CMD:

venv\Scripts\activate

Windows PowerShell:

.\venv\Scripts\Activate.ps1

4. Install dependencies

pip install flask flask-socketio SpeechRecognition PyAudio pyttsx3 pywhatkit pyjokes wikipedia requests

Configuration

The weather functionality requires an OpenWeatherMap API key.

Do not commit API keys directly to GitHub.

A production-ready implementation should store secrets in environment variables:

import os

api_key = os.getenv("OPENWEATHER_API_KEY")

Then configure the environment variable before running the application.

Running the Application

Activate the virtual environment:

venv\Scripts\activate

Run the assistant:

python "flask-alexa 1.py"

The voice assistant will initialize the microphone and wait for the wake word.

If the Flask server is enabled successfully, the web interface can be accessed through the local Flask address shown in the terminal, typically:

http://127.0.0.1:5000

How It Works

The application initializes the Flask and SocketIO backend.

A background thread starts the voice assistant.

The microphone captures audio using PyAudio.

SpeechRecognition sends the captured speech to Google Speech Recognition.

The recognized text is converted to lowercase and matched against supported commands.

The corresponding Python functionality is executed.

pyttsx3 converts the generated response into speech.

Flask-SocketIO emits speaking-status information to the web frontend.

Example Flow

User:
"Hey Synthesia"

        ↓

Speech Recognition

        ↓

Wake Word Detected

        ↓

Synthesia:
"I am listening now. How can I help you today?"

        ↓

User:
"What is the weather?"

        ↓

Synthesia:
"Please tell me the city name."

        ↓

User:
"Delhi"

        ↓

OpenWeatherMap API

        ↓

Synthesia:
"The temperature in Delhi is XX degrees Celsius."

Requirements

Python 3.11+

Working microphone

Internet connection for Google Speech Recognition

Internet connection for Wikipedia/weather/web services

OpenWeatherMap API key for weather functionality

Windows/macOS/Linux with compatible audio dependencies

Security Notes

Never upload API keys, passwords, tokens, or other secrets to GitHub.

Use environment variables or a .env file for credentials.

Add .env and local virtual environments to .gitignore.

Avoid committing generated cache files such as __pycache__.

Example .gitignore:

venv/
alexa-flask-env/
__pycache__/
*.pyc
.env

Future Improvements

Add Natural Language Processing for more flexible command understanding

Replace keyword-based command matching with an intent-classification system

Add conversational memory

Add authentication for the web interface

Improve error handling and logging

Move API keys to environment variables

Add a database for user preferences and command history

Add a modern responsive frontend

Add support for multiple languages

Add an LLM-based conversational mode

Add automated testing and CI/CD

Deploy the Flask application to a cloud platform

Learning Outcomes

This project demonstrates practical experience with:

Python application development

Flask web development

REST API integration

Speech recognition

Text-to-speech systems

Microphone/audio handling

Multithreading

Real-time WebSocket communication

Third-party Python libraries

API-based weather services

Web automation

Git/GitHub project organization

License

This project is intended for educational and portfolio purposes. Add a suitable open-source license before redistributing the project publicly.
