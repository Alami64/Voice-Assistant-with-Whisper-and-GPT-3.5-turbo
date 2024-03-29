# Voice Assistant with Whisper and GPT-3.5-turbo-1106

This project is a voice assistant that utilizes the Whisper speech recognition model for transcribing user speech and the OpenAI GPT-3.5-turbo-1106 language model for generating responses. It listens for a wake word, processes the user's speech, and provides a spoken response using text-to-speech.

## Features

- Wake word detection: The assistant listens for a specific wake word to activate.
- Speech recognition: It transcribes the user's speech using the Whisper model.
- Language model integration: It generates responses using the OpenAI GPT-3.5-turbo-1106 model.
- Text-to-speech: The generated responses are converted to speech using gTTS.
- Configurable options: Various parameters can be adjusted, such as the wake word, energy threshold, pause time, and model size.

## Requirements

- Python 3.x
- PyTorch
- OpenAI API key
- Whisper
- SpeechRecognition
- gTTS
- pydub
- python-dotenv

## Installation

1. Clone the repository:
   ```bash
   https://github.com/Alami64/Voice-Assistant-with-Whisper-and-GPT-3.5-turbo.git
   ```
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Set up your OpenAI API key:
    - Create a `.env` file in the project directory.
    - Add your OpenAI API key to the `.env` file: `OPENAI_API_KEY=your_api_key_here`

## Usage

To run the voice assistant, use the following command:
```bash
python main.py [--model MODEL] [--english] [--energy ENERGY] [--pause PAUSE] [--dynamic_energy] [--wake_word WAKE_WORD] [--verbose]
```

- `--model`: Choose the Whisper model size (tiny, base, small, medium, large). Default is "base".
- `--english`: Use the English-only model. Default is False.
- `--energy`: Set the energy level for the microphone to detect speech. Default is 300.
- `--pause`: Set the pause time before considering the speech entry ended. Default is 0.8 seconds.
- `--dynamic_energy`: Enable dynamic energy adjustment. Default is False.
- `--wake_word`: Set the wake word to activate the assistant. Default is "jarvis".
- `--verbose`: Enable verbose output for debugging. Default is False.

## How It Works

1. The `main.py` script initializes the Whisper model, sets up queues for audio and transcription results, and starts three threads:
   - `record_audio`: Continuously records audio from the microphone and puts the audio data into the `audio_queue`.
   - `transcribe_forever`: Retrieves audio data from the `audio_queue`, transcribes it using the Whisper model, and puts the transcribed text into the `result_queue` if the wake word is detected.
   - `reply`: Retrieves the transcribed text from the `result_queue`, generates a response using the OpenAI GPT-3.5-turbo-1106 model, converts the response to speech using gTTS, and plays the audio response.

2. The `replying.py` script handles the generation of responses using the OpenAI API and the playback of the generated speech.
