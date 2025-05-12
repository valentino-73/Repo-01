import speech_recognition as sr

def convertir_audio_a_texto_mic():
    # Inicializamos el reconocedor y el micrófono
    recognizer = sr.Recognizer()
    micrófono = sr.Microphone()

    with micrófono as source:
        print("Ajustando niveles del micrófono...")
        recognizer.adjust_for_ambient_noise(source)  # Ajusta los niveles de ruido ambiente
        print("Escuchando... por favor hable.")
        audio_data = recognizer.listen(source)

        try:
            print("Reconociendo texto...")
            texto = recognizer.recognize_google(audio_data, language="es-ES")
            return texto
        except sr.UnknownValueError:
            return "No se pudo entender el audio."
        except sr.RequestError as e:
            return f"Error en la solicitud al servicio de reconocimiento: {e}"

# Ejemplo de uso
resultado = convertir_audio_a_texto_mic()
print("Texto transcripto:\n", resultado)
with open("C:\\Users\\Valentino\\Desktop\\programacion\\VALENTINO\\Nueva carpeta\\texto.txt", "w", encoding="utf-8") as archivo:
    archivo.write(resultado)
archivo.close()
