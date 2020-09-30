!pip install youtube-dl   # youtubeの動画をダウンロードするためのもの
!pip install ffmpeg   # 動画の録画・再生するためのもの
!pip install SpeechRecognition  # 音声ファイルをテキストに変換するためのもの
!pip install pydub  # mp3をwavに変換するためのもの


import youtube_dl
import pydub
from pydub import AudioSegment
import speech_recognition as sr
import os

# youtubeの動画のurlからダウンロード
ydl_opts = {
    'format': 'bestaudio/best',
    'outtmpl':  "sample_music" + '.%(ext)s',
    'postprocessors': [
        {'key': 'FFmpegExtractAudio',
        'preferredcodec': 'mp3',
         'preferredquality': '192'},
        {'key': 'FFmpegMetadata'},
    ],
}
#　sample_music.mp3として保存される
ydl = youtube_dl.YoutubeDL(ydl_opts)
info_dict = ydl.extract_info("音声をテキストに変換したいyoutubeの動画URL", download=True)


sound = AudioSegment.from_file("sample_music.mp3", format="mp3")

# 音声ファイルの動画時間が長すぎると文字起こしできない（google colabが対応していない？）
sound1 = sound[0:240000] # 30秒ごとに試したところ4分30秒からエラーが出た

# 抽出した部分を出力
sound1.export("output1.mp3", format="mp3")


# 文字起こしは wav 形式にしか対応していないため mp3 から wav に変換
sound = pydub.AudioSegment.from_mp3("output1.mp3")
sound.export("output.wav", format="wav")

AUDIO_FILE = "output.wav"


# ここから文字起こし
r = sr.Recognizer()
with sr.AudioFile(AUDIO_FILE) as source:
  audio = r.record(source)

print("音声データの文字起こし結果：\n\n", r.recognize_google(audio,language = "ja"))

audio_text = r.recognize_google(audio, language = "ja")

with open('audio_text.txt', 'w') as f:
  print(audio_text, file=f)

print(len(audio_text))

# 文字数が多すぎると音声にできなかったため文字数を制限
if len(audio_text) > 100:
  audio_text = audio_text[0:99]

# ここからテキストから音声にするもの。最初のものたちをインストールしないと動かない
input_text = audio_text

with torch.no_grad():
    start = time.time()
    x = frontend(input_text)
    c, _, _ = model.inference(x, inference_args)
    y = vocoder.inference(c)
rtf = (time.time() - start) / (len(y) / fs)
print(f"RTF = {rtf:5f}")

from IPython.display import display, Audio
display(Audio(y.view(-1).cpu().numpy(), rate=fs))
