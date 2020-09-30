# youtubeから動画を取ってきて音声をテキストと合成音声に変換するもの

音声合成に関しては
https://colab.research.google.com/github/espnet/notebook/blob/master/tts_realtime_demo.ipynb#scrollTo=69vGlN12DqB2
こちらの内容を使用させていただきました。
以下コピペ手順
Install → Japanese demo → Tacotron 2 → Setup

google colab上で動作させました。
google colabの仕様上（おそらく）長すぎる動画ファイルは対応していないため4分までにカット
メモリ不足により長すぎるテキストは合成音声にできなかったため100文字までにカット
