Criando um Sistema de Assistência Virtual do Zero

Este projeto tem como objetivo criar um sistema de assistência virtual do zero, utilizando Processamento de Linguagem Natural (PLN), com base nas bibliotecas apresentadas durante o curso. O sistema será capaz de interagir com o usuário de forma intuitiva, com funcionalidades de conversão de texto em áudio, reconhecimento de fala, e execução de comandos automatizados por voz.
Requisitos do Sistema

O sistema de assistência virtual deve atender aos seguintes requisitos:

    Módulo de Transformação de Texto em Áudio (Text-to-Speech):
        O sistema deve ser capaz de converter texto em áudio, permitindo que o assistente fale com o usuário. Isso será realizado utilizando bibliotecas como pyttsx3 ou gTTS.

    Módulo de Transformação de Fala em Texto (Speech-to-Text):
        O sistema deve ser capaz de reconhecer a fala do usuário e convertê-la em texto, utilizando bibliotecas como SpeechRecognition.

    Módulo de Ações Automatizadas por Comando de Voz:
        O sistema deve ser capaz de acionar comandos como:
            Abrir uma pesquisa no Wikipedia.
            Abrir o YouTube.
            Apresentar a localização da farmácia mais próxima.
        Isso será feito através da interpretação de comandos de voz, utilizando o módulo de reconhecimento de fala e integrando APIs para realizar as ações automatizadas.

Bibliotecas Utilizadas

Durante o desenvolvimento deste projeto, serão utilizadas as seguintes bibliotecas:

    SpeechRecognition: Para converter fala em texto.
    pyttsx3 ou gTTS: Para converter texto em fala.
    Wikipedia: Para realizar pesquisas no Wikipedia.
    webbrowser: Para abrir páginas da web (como YouTube).
    geopy: Para localizar a farmácia mais próxima.

Estrutura do Projeto

virtual_assistant/
│
├── assistant.py           # Arquivo principal para execução do assistente
├── text_to_speech.py      # Módulo de conversão de texto em fala
├── speech_to_text.py      # Módulo de conversão de fala em texto
├── actions.py             # Módulo para execução de comandos automatizados
├── requirements.txt       # Dependências do projeto
├── README.md              # Documentação do projeto

assistant.py

Este arquivo será o ponto de entrada para o assistente, integrando todos os módulos. Ele utilizará o reconhecimento de fala para entender os comandos do usuário e acionar as funções apropriadas.
text_to_speech.py

Responsável pela conversão de texto em áudio, utilizando a biblioteca pyttsx3 ou gTTS.
speech_to_text.py

Este módulo será responsável por capturar a fala do usuário e convertê-la em texto, utilizando a biblioteca SpeechRecognition.
actions.py

Aqui serão implementadas as funções automatizadas acionadas por comandos de voz, como abrir o YouTube, buscar no Wikipedia ou encontrar farmácias próximas.
Como Usar

    Instalar as Dependências:

    Primeiramente, instale as bibliotecas necessárias:

pip install -r requirements.txt

Executar o Assistente Virtual:

Após a instalação das dependências, execute o arquivo principal para iniciar o assistente:

    python assistant.py

    Interagir com o Assistente:

    Quando o sistema estiver em execução, você poderá interagir com ele por meio de comandos de voz. Por exemplo:
        "Pesquise sobre inteligência artificial no Wikipedia."
        "Abra o YouTube."
        "Onde está a farmácia mais próxima?"

Exemplo de Execução
Módulo de Conversão de Texto em Áudio (Text-to-Speech)

import pyttsx3

def speak(text):
    engine = pyttsx3.init()
    engine.say(text)
    engine.runAndWait()

speak("Olá, como posso ajudá-lo?")

Módulo de Conversão de Fala em Texto (Speech-to-Text)

import speech_recognition as sr

def listen():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Diga algo:")
        audio = recognizer.listen(source)
    
    try:
        text = recognizer.recognize_google(audio)
        print(f"Você disse: {text}")
        return text
    except sr.UnknownValueError:
        print("Não consegui entender o que você disse.")
        return None
    except sr.RequestError:
        print("Erro ao conectar ao serviço de reconhecimento de fala.")
        return None

Módulo de Ações Automatizadas

import webbrowser
import wikipedia
from geopy.geocoders import Nominatim

def search_wikipedia(query):
    result = wikipedia.summary(query, sentences=2)
    print(result)
    speak(result)

def open_youtube():
    webbrowser.open("https://www.youtube.com")

def find_nearest_pharmacy():
    geolocator = Nominatim(user_agent="virtual_assistant")
    location = geolocator.geocode("farmácia", timeout=10)
    if location:
        print(f"A farmácia mais próxima está em: {location.address}")
        speak(f"A farmácia mais próxima está em: {location.address}")
    else:
        print("Não encontrei farmácias próximas.")
        speak("Não encontrei farmácias próximas.")

Conclusão

Este projeto visa criar um assistente virtual funcional e simples, com a utilização das principais bibliotecas de Processamento de Linguagem Natural (PLN) e reconhecimento de fala. Ao seguir os requisitos propostos, você será capaz de criar um assistente que entende comandos de voz e interage com o usuário de maneira intuitiva.
