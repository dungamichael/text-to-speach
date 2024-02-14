# text-to-speach
import pyttsx3
import os

engine = pyttsx3.init()  # Object creation



def save_file_if_unique(text_to_speak, file_name, save_folder):
    """
    Saves a file to a folder only if it doesn't already exist.

    Args:
        file_name (str): The name of the file to save.
        save_folder (str): The path to the folder where to save the file.
    """
    full_path = os.path.join(save_folder, file_name)
    if not os.path.exists(full_path):
        os.makedirs(save_folder, exist_ok=True)  # Create folder if needed
        try:
            engine.save_to_file(text_to_speak, full_path)  # Use descriptive variable
            engine.runAndWait()
            print(f"Saved file: {file_name} to {save_folder}")
        except Exception as e:  # Add error handling
            print(f"Error saving file: {e}")
    else:
        print(f"File already exists: {file_name}. Skipping.")

#############################################################
#############################################################

def formater(text):
  old = text.split("\n\n")
  new = []
  for line in old:
    line = line.replace("\n", " ")
    if line.find(" ") != -1:
      line = line.replace(" ", ":\t", 1)
    if line.find(":") != -1:
      line = line.replace(":", " ", 1)
    new.append(line)
  return "\n\n".join(new)  

#############################################################
#############################################################

""" RATE"""
rate = engine.getProperty('rate')   # getting details of current speaking rate
#print (rate)                        #printing current voice rate
engine.setProperty('rate', 150)    # setting up new voice rate
#print (rate)                        #printing current voice rate

"""VOLUME"""
volume = engine.getProperty('volume')   #getting to know current volume level (min=0 and max=1)
#print (volume)                          #printing current volume level
engine.setProperty('volume',1.0)    # setting up volume level  between 0 and 1

"""VOICE"""
voices = engine.getProperty('voices')       #getting details of current voice
#engine.setProperty('voice', voices[0].id)  #changing index, changes voices. o for male
engine.setProperty('voice', voices[0].id)   #changing index, changes voices. 1 for female

#############################################################
#############################################################

text_to_speak = """PROVERBS CHAPTER 31

31 1:   The words of king Lemuel, the prophecy that his mother taught him.

31 2:   What, my son? and what, the son of my womb? and what, the son of my vows?

31 3:   Give not thy strength unto women, nor thy ways to that which destroyeth kings.
"""

#############################################################
#############################################################
# Format text_to_speak or remove the function if unnecessary
# text_to_speak = formater(text_to_speak)

save_folder = "proverbs"
file_name = "proverbs31.mp3"  # Use consistent naming

# Check for Linux dependencies if you use them
if os.name == "posix":  # Consider more specific check
    print("Ensure 'espeak' and 'ffmpeg' are installed on Linux.")

save_file_if_unique(text_to_speak, file_name, save_folder)




