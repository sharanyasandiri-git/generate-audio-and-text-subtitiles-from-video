# generate-audio-and-text-subtitiles-from-video
Ever wondered how YouTube automatically generates subtitles? I tried building a simple version of that — by extracting audio and text directly from video files using Python libraries like MoviePy and SpeechRecognition. Here’s what I learned and how it works 

"""#Install below libraries
-----------------------
pip install moviepy==1.0.3
pip install SpeechRecognition

pip install moviepy==1.0.3 SpeechRecognition

#Run below file
--------------
#py extract_text_from_video.py"""



print("Step 1: Importing the libraries")

import os
import glob
import moviepy.editor as mp 
import speech_recognition as sr 




print("Step 2: Loading the video/mp4 file")

def load_video(folder):
    files = os.path.join(folder, "*.mp4")
    mp4_files = glob.glob(files)
    return mp4_files


f = "./videos"
mp4_file_list = load_video(f)

print(mp4_file_list)





print("Step 3: Extract audio from video/mp4 file")


def audio_from_video(file_list):
    video = mp.VideoFileClip(file_list[0]) 
    audio_file = video.audio 
    audio_file.write_audiofile("./audio/sample.wav") 


audio_from_video(mp4_file_list)

print("Step 4: Loading audio file")

r = sr.Recognizer() 
with sr.AudioFile("./audio/sample.wav") as source: 
	data = r.record(source) 

print("Step 5: Extract text from audio/mp3 file")

text = r.recognize_google(data) 

print("\nThe TEXT from VIDEO is: \n") 
print(text) 

