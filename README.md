## Text-To-Speech-openai
The idea of this project is to create a Text-to-Speech (TTS) system that allows users to convert written text into spoken audio. The system uses the OpenAI API to generate the audio files.
### Some potential use cases for this project include:

* Creating audio versions of written content, such as blog posts or articles.
* Generating audio files for educational or training materials.
* Converting written scripts into spoken audio for videos or podcasts.
* Assisting individuals with reading difficulties or disabilities.
### Setup:
1. OpenAI API Key:
   * Create an account on the OpenAI website (www.openai.com).
   * Apply for an API key, which will be used to authenticate your requests to the OpenAI API. 
   * Once you receive your API key, store it in a .env file in your project folder.
2. Project setup:
   * The programming language used in this project is python for that you need to start by setting up Python on your device by following these steps:

     - Install Python
     - Install the OpenAI Python library
     - Set up a virtual environment (optional)
     - Set up your API key
     - Sending your API request
     - All the detailes about gettin up and running with the OpenAI API for different operaing systems and different languages are provided here: https://platform.openai.com/docs/quickstart
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### Learn more about Text To Speech here: https://platform.openai.com/docs/guides/text-to-speech/overview
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### The Text To Speech Model used in this Project is called TTS-1 which is the latest text to speech model, optimized for speed, learn more about it here: https://platform.openai.com/docs/models/tts
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
### python T-T-S convertor:
This code askes the user if they want to type a text to be converted into audio or if they want to use a text file instead of writing,

then using tts-1 the text will be converted to a human like voice then saved as .mp3 file that can be played for listeners.
```
from openai import OpenAI

client = OpenAI()

while True:
    # Ask the user if they want to write a text or read from a file
    choice = input("Do you want to write a text or read from a file? (type 'text' or 'file', 'quit' to exit): ")
    if choice.lower() == 'quit':
        break

    if choice.lower() == 'text':
        # Get the text from the user
        text_input = input("Enter your text or '-1' to exit: ")

        if text_input == '-1':
            break

        # Use the OpenAI API to create a speech audio file from the user's text
        response = client.audio.speech.create(
            model='tts-1',
            input=text_input,
            voice='alloy'
        )

        # Save the audio as mp3
        filename = input("Enter the filename (e.g. test.mp3): ")
        response.write_to_file(filename)

        print("Speech saved to", filename)
        print("\n")

    elif choice.lower() == 'file':
        # Prompt the user to enter the filename of the text file
        filename_text = input("Enter the filename of the text file (e.g. text.txt): ")

        try:
            with open(filename_text, 'r') as file:
                text_input = file.read()
        except FileNotFoundError:
            print("File not found. Try again.")
            continue

        # Use the OpenAI API to create a speech audio file from the text file
        response = client.audio.speech.create(
            model='tts-1',
            input=text_input,
            voice='alloy'
        )

        # Prompt the user to enter the filename for the audio file
        filename_audio = input("Enter the filename for the audio file (e.g. test.mp3): ")

        # Save the audio file to disk
        response.write_to_file(filename_audio)

        print("Speech saved to", filename_audio)
        print("\n")

    else:
        print("Invalid choice. Please try again.")
```
### Demo
#### Code output:
<img width="583" alt="write-read-tts" src="https://github.com/user-attachments/assets/90f81b9b-fb95-4493-9478-7a9478da0cf1">

------------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------------------
#### The writen text is now converted into a voice:
 

https://github.com/user-attachments/assets/22d79fb2-d3e2-4a00-8ced-4f29d54e03f1

------------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------------------
#### The text file used was:
  ![test-file](https://github.com/user-attachments/assets/8f4f6fbf-fa05-44b2-8821-d4dd80bc39ed)

#### Text file converted into a voice:


https://github.com/user-attachments/assets/c796383e-eb59-49bb-8bcc-cbafebbdd575

-------------------------------------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------------------------------------
#### TTS supports many languages including Arabic language also have many different voices, here is a mixed english and arabic language audio:


https://github.com/user-attachments/assets/6fd8bc77-5836-4154-8df7-82d9683267ea

