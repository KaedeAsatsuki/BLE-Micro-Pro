## ビルド時にnrf_delay.hが見つからないというエラーが出る。
NRDSDK15_ROOTがあっているか、ダウンロードしたSDKのバージョンが正しいか確認して下さい

## 書き込み時にハッシュエラーが出る
bootloaderかnrfutilのバグで、正常なバイナリでも書き込みエラーが出ることがあるようです。master.cかslave.c内の関数をコメントアウトしたり書きかえたりして、
バイナリを変えると書き込めるようになります

## 書き込み時にusb_serialが見つからないとエラーが出る
qmk/tmk_core/nrf.mkの862行目

`$(NRFUTIL) dfu usb_serial -pkg $(TARGET).zip -p $$USB; \`

を

`$(NRFUTIL) dfu usb-serial -pkg $(TARGET).zip -p $$USB; \`

に書き換えてください

## PCやmaster-slaveの接続が上手くいかなくなった
両方のデバイス(PCとmaster, masterとslave)からペアリング情報を消してから再ペアリングしてください。

後述のターミナルを使って確認しながら削除・再ペアリングするとわかりやすいです。

## ペアリングが上手くいったのか、情報を消せたのかわからない
Tera Terminal等のターミナルソフトでファーム書き込み済みBLE Micro Proのターミナルを開くと、ペアリングの確認や削除ができます。

また、BLE接続時・切断時にメッセージが表示されます。

|コマンド |説明  |
|-|-|
|help|コマンド一覧を表示|
|adv|デバイスの探索を開始|
|show|保存済みのペアリングの数を表示|
|del [id]|id番目のペアリングを削除|

## チャタリングする
config.hのDEBOUNCEを1ずつ増やしてみてください。
