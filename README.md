# Audiofrom PIL import Image
import pytesseract
from gtts import gTTS
import os

# Path to the Tesseract executable (update this with your own path)
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'

def recognize_text(image_path):
    try:
        # Open the image file
        with Image.open(image_path) as img:
            # Use pytesseract to recognize text
            text = pytesseract.image_to_string(img)
            return text
    except Exception as e:
        print(f"Error: {e}")
        return None

def text_to_speech(text, language='en'):
    try:
        # Create a gTTS object
        tts = gTTS(text=text, lang=language, slow=False)
        
        # Save the audio file
        tts.save("output.mp3")

        # Play the audio file
        os.system("start output.mp3")
    except Exception as e:
        print(f"Error: {e}")

# Example usage
image_path = 'path/to/your/image.png'
recognized_text = recognize_text(image_path)

if recognized_text:
    print(f"Recognized Text: {recognized_text}")
    text_to_speech(recognized_text)
else:
    print("Text recognition failed.")
