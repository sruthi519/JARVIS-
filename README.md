import pyttsx3
import speech_recognition as sr
import datetime
import webbrowser
import os

engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voices', voices[0].id)  

def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wish_me():
    hour = int(datetime.datetime.now().hour)
    if 0 <= hour < 12:
        speak("Good Morning!")
    elif 12 <= hour < 18:
        speak("Good Afternoon!")
    else:
        speak("Good Evening!")
    speak("I am chiki. How can I help you?")

def take_command():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        speak("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        speak("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"You said: {query}")
    except Exception as e:
        print("Say that again please...")
        speak("Say that again please...")
        return "None"
    return query.lower()

if __name__ == "__main__":
    wish_me()
    while True:
        query = take_command()


        if "open youtube" in query:
            webbrowser.open("https://www.youtube.com")
            speak("chiki is opening YouTube")

        elif "open google" in query:
            webbrowser.open("https://www.google.com")
            speak("chiki is opening Google")

        elif "what is the time and date" in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"The time is {strTime}")
            Today=datetime.date.today()  
            speak(f"Today's date is {Today.strftime('%B %d,%Y')}")  

        elif "open weather update" in query:
            webbrowser.open("https://developer.accuweather.com/weather/now")
            speak("chiki is opening weather update")

        elif "open news" in query:
            webbrowser.open("https://indianexpress.com//news/")
            speak("chiki is opening news update")

        elif "open calculator" in query:
            os.system("start calc")
            speak("chiki is opening calculator")

        elif "open spotify" in query:
            webbrowser.open("https://open.spotify.com/")
            speak("chiki is opening Spotify")

        elif "open whatsapp" in query:
            os.system(r"C:\Users\Admin\Desktop\WhatsApp.lnk")
            speak("chiki is opening WhatsApp")

        elif "open chat" in query:
            webbrowser.open("https://chat.openai.com/")
            speak("chiki is opening chat")

        elif "open map" in query:
            webbrowser.open("https://www.google.co.in/maps")
            speak("chiki is opening Google Maps")

        elif "open translator" in query:
            webbrowser.open("https://translate.google.com/")
            speak("chiki is opening Google Translator")

        elif "open camera" in query:
            os.system("start microsoft.windows.camera:")
            speak("chiki is opening camera")
        elif"open notepad" in query:
            os.system("notepad")
            speak("chiki is opening notepad")

        elif "exit" in query:
            speak("Goodbye!,have a nice day!")
