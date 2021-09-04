# コンサーティーナ 自作 MIDIキーボード の実現方法
ohayuta さんが Corne Cherry を使ってコンサーティーナ のMIDIキーボード を実現されるということで、QMK Firmware のコードを少し変更して、VIA （REMAP）で MIDIの音階キーを割り当てた後、MIDI出力できるようにしました。  
### 注意点： 2021/9/4 現在、押し引きで音が変わるダイアトニック式コンサーティーナ（＝アングロ・コンサーティーナ、＝蛇腹を開いた時と閉じた時で異なる音が出るタイプ）の再現のためにはレイヤー切り替え作戦をイメージしておりました。しかし、この作戦はうまく行かないようです。レイヤーの切り替えだけでは、押しっぱなしにしている音階キーが押され直さないようです。もともとQMK Firmware はタイピングキーボード用に設計されているので、そういう仕様なのだと思います。 ###

参考：ohayuta さんのブログ  
https://itmlearner.blogspot.com/2021/07/midi.html

# キーボードキット
foostan さんの Corne キーボード  
https://github.com/foostan/crkbd  

# ファームウェア
github にUPされているコードに一部変更を加えて、MIDI機能を有効にしました。
ただ、そのままではファームウェアの容量オーバーだったため、config.h にて  
'#define RGBLIGHT_ANIMATIONS'
はコメントアウトして無効にしています。もしもLEDを使われる場合は、別の不要な機能を削減するなど対応が必要になると思います。  

コンパイル済のものを[こちら](https://github.com/3araht/crkbd2ConcertinaMIDI/blob/main/crkbd_rev1_via_concertinaMIDI_hex.zip)にUPしています。  

# 変更箇所
変更内容：　　
- rules.mk で 'MIDI_ENABLE = yes' にする。
- config.h で 'MIDI_ADVANCED' を define する。
-  (ファームウェアの容量の都合で 'RGBLIGHT_ANIMATIONS' をコメントアウト)
- keymap.c で MIDI の初期音量の指定とオクターブ位置の調整

をしています。  

詳細の変更点は  [diff 出力](https://github.com/3araht/crkbd2ConcertinaMIDI/blob/main/crkbd_ConcertinaMIDI.diff)
をご覧ください。  

# コンタクト先:
***このVIAファームウェアの変更案は 3araht の勝手なカスタマイズですので、MIDIに関するお問い合わせなどを Corne キーボード作者の foostan さんにしないよう、ご注意ください。***  

Twitter, YouTube, Instagram はじめました。  
http://twitter.com/3araht  
https://www.youtube.com/channel/UC0zYtYMoxb0P7S8DPAkl0zA/  
https://www.instagram.com/3araht/  

# A proposal to convert Corne keyboard into Concertina MIDI keyboard
ohayuta had an Excellent idea using Corne keyboard emulating a MIDI keyboard of Concertina.
I helped him a little to preape a VIA firmware which has MIDI features enabled.  

### Warning: As of 2021/9/4, layer transition was the idea to emulate the different notes played when bellows are pressed or pulled (Diatonic Concertina = Anglo style Concertina, which each button plays a different note depending on whether the bellows are pressed or pulled). However, this doesn't work well since QMK Firmware is originally designed for typing keyboards which would not prefer such attitude. ###

Reference：ohayuta's blog
https://translate.google.com/translate?sl=ja&tl=en&u=https://itmlearner.blogspot.com/2021/07/midi.html

# Keyboard kit
foostan's Corne keyboard is introduced here.  
https://github.com/foostan/crkbd  


# Firmware
Based on Corne's codes on github, MIDI features were enabled. Since the firmware size was too big, 'RGBLIGHT_ANIMATIONS' feature had to be disabled in config.h. If you use them, you need to make room for it by disabling other unused features.  

Check [here](https://github.com/3araht/crkbd2ConcertinaMIDI/blob/main/crkbd_rev1_via_concertinaMIDI_hex.zip) for the actual hex file.  

# Changes
The below were modified:
- 'MIDI_ENABLE = yes' in rules.mk
- 'MIDI_ADVANCED' defined in config.h
-  ( 'RGBLIGHT_ANIMATIONS' was commented out due to the firmware size issue.)
- Initial velocity setting and Octave setting were specified in keymap.c.

The detailed diff output is shown [here](https://github.com/3araht/crkbd2ConcertinaMIDI/blob/main/crkbd_ConcertinaMIDI.diff).  

# Contact
***PLEASE MAKE SURE NOT TO CONTACT foostan REGARDING 3araht's UNOFFICIAL MIDI CUSTOMIZATION PROPOSAL.***  

If you need any help, you know where to find me.  
http://twitter.com/3araht  
https://www.youtube.com/channel/UC0zYtYMoxb0P7S8DPAkl0zA/  
https://www.instagram.com/3araht/  
