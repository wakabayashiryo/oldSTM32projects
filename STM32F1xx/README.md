<div style="text-align: center; color:cyan;">
<h1>STM32F1ファミリー用GNU-GCCプロジェクト</h1>
</div>

- ## 概要
    STM32F1ファミリのプログラムをコンパイルするためのプロジェクト

- ## プロジェクトの使い方
    端末より、プロジェクトのディレクトリまで移動し,makeコマンドでコンパイルされます。コンパイル完了後、BinとDebugフォルダ内に実行ファイルとオブジェクトファイルが生成されます。以下にコンパイルのコマンドを示します。

- ## コマンド一覧

    | コマンド | 内容 |
    |:---------:|:------------------------------------------------------:|
    | make | すべてのソースファイルがコンパイルされBinフォルダに実行ファイルが生成されます。 |
    | make clean | Debug Binフォルダが消去され、実行ファイル、オブジェクトファイルが消去されます。 |
    | make -j | コンパイル時CPUが並列で処理します。他のオプションと兼用可能 |
    | make -B | すべてのファイルが強制的に再コンパイルされます。 |
    | make OPTIMIZE=-Ox | 最適化オプションを変更します。xの値で最適化レベルを変更できます。デフォルトは-O0 |

- ## プロジェクト詳細


~~~
    STM32F1xx
    ├── Apprication
    ├── Drivers
    │   ├── CMSIS
    │   │   ├── Device
    │   │   │   ├── Inc
    │   │   │   │   ├── デバイスのヘッダーファイル
    │   │   │   │   ├── stm32f1xx.h
    │   │   │   │   └── system_stm32f1xx.h
    │   │   │   └── Src
    │   │   │       ├── gcc
    │   │   │       │   └── スタートアップファイル
    │   │   │       └── system_stm32f1xx.c
    │   │   ├── Inc
    │   │   │   ├── arm_common_tables.h
    │   │   │   ├── arm_const_structs.h
    │   │   │   ├── arm_math.h
    │   │   │   ├── cmsis_armcc.h
    │   │   │   ├── cmsis_armcc_V6.h
    │   │   │   ├── cmsis_gcc.h
    │   │   │   ├── core_cm0.h
    │   │   │   ├── core_cm0plus.h
    │   │   │   ├── core_cm3.h
    │   │   │   ├── core_cm4.h
    │   │   │   ├── core_cm7.h
    │   │   │   ├── core_cmFunc.h
    │   │   │   ├── core_cmInstr.h
    │   │   │   ├── core_cmSimd.h
    │   │   │   ├── core_sc000.h
    │   │   │   └── core_sc300.h
    │   │   └── doc
    │   ├── LinkerScript
    │   │   └── リンカースクリプトファイル
    │   └── STM32F1xx_HAL_Driver
    │       ├── Inc
    │       │   ├── Legacy
    │       │   │   └── stm32_hal_legacy.h
    │       │   ├──HALドライバーのヘッダーファイル
    │       └── Src
    │           └── HALドライバーのソースファイル
    ├── Inc
    │   ├── mxconstants.h
    │   ├── stm32f1xx_hal_conf.h
    │   └── stm32f1xx_it.h
    ├── Makefile
    ├── MidleWare
    ├── UpdateDriver.sh
    ├── README.md
    └── Src
        ├── main.c
        ├── stm32f1xx_hal_msp.c
        └── stm32f1xx_it.c
~~~

- ## 各ディレクトリの説明
    - ./Inc・・・ユーザーが記述したヘッダーファイルを入れます。
    - ./Src・・・メインのプログラムを記述するソースファイルを入れます。
    - ./MidleWare・・・このフォルダーはHALドライバーを制御するプログラムを入れます。
      MidleWare内に各ライブラリのフォルダーを作成し、その中にInc(インクルード)Src(ソース)フォルダーを作成します。
      **Inc Srcフォルダーを作成しないとエラーが発生します**
    - ./Apprication・・・このフォルダーはデータ管理や周辺機器の管理するプログラムを入れます。
      MidleWare内に各ライブラリのフォルダーを作成し、その中にInc(インクルード)Src(ソース)フォルダーを作成します。
      **Inc Srcフォルダーを作成しないとエラーが発生します**
    - ./Bin・・・実行ファイルが出力されるフォルダーです。
    - ./Debug・・・コンパイル時に生成されるオブジェクトファイルと依存関係ファイルが出力されます。
    - ./Drivers・・・デバイスに必要なヘッダーファイルやリンカースクリプト、HALドライバーが入っています。
      基本的にユーザーはこのフォルダ内のファイルは変更しません。
- ## 新規プロジェクトの作成
    1. github上に新しいリポジトリを作成   
    2. githubから以下のコマンドでリポジトリをPC内にクローンする   
        > ~/$ **git clone https://github.com/wakabayashiryo/STM32F1xx.git**   
    3. ２でクローンしたリポジトリのフォルダ名を変更   
    4. ターミナルでカレントディレクトリをリポジトリに移動   
    5. １で作成したリポジトリアドレスを追加   
        > ~/Hoge_Project$ **git remote add hoge https://github.com/yourid/repository.git**   
    6. １で作成したリポジトリにプッシュする   
        > ~/Hoge_Project$ **git push hoge master**   

    **\*Worning** 新しく作成したリポジトリから　***origin***　にプッシュしないでください    

    ### *最新のテンプレートにアップデート
    - 以下のコマンドをプロジェクトフォルダー内で実行してください
        > git pull origin master

- ## ドライバーの更新
    1. ST社のホームページ、またはSTM32Cubeから最新のHALドライバーをダウンロードします。
    2. zipファイルを解凍します。
    3. 以下のコマンドを実行   
        > ~/$ **sudo chmod +x UpdateDriver.sh**   
        > ~/$ **./UpdateDriver.sh <2で解凍したフォルダーのパス>**   
            
        ***HALドライバーのテンプレートファイルは自動で消去されます***
    4. コンパイルを行い、エラーが出ないことを確認してください
    5. README.mdのバージョン情報にライブラリの更新を記述
    6. make cleanした後に、gitにcommitします

    | ファイルの種類| ファイル名    | ディレクトリ               |
    |:--------:|:-------------:|:---------------------------:|
    |デバイスのヘッダーファイル      | stm32f1xx**.h        | ./Drivers/CMSIS/Device/Inc    |
    |デバイスのスタートアップファイル   | startup_stm32f1xx**.s| ./Drivers/CMSIS/Device/Src/gcc|
    |リンカースクリプト | STM32F1XX**.ld| ./Drivers/LinkerScript      |
    |CMSISのヘッダーファイル | cmsis.h or core.h | ./Drivers/CMSIS/Inc|
    |HALドライバーのヘッダーファイル  | stm32_hal_*.h| ./Drivers/STM32F1xx_HAL_Driver/Inc|
    |HALドライバーのソースファイル   | stm32_hal_*.c| ./Drivers/STM32F1xx_HAL_Driver/Src|

- ## 対応デバイス

    |Define|Detail|
    |:-----:|:-------:|
    | STM32F100xB | STM32F100C4, STM32F100R4, STM32F100C6, STM32F100R6, STM32F100C8, STM32F100R8, STM32F100V8, STM32F100CB, STM32F100RB and STM32F100VB  |
    | STM32F100xE | STM32F100RC, STM32F100VC, STM32F100ZC, STM32F100RD, STM32F100VD, STM32F100ZD, STM32F100RE, STM32F100VE and STM32F100ZE  |
    | STM32F101x6 | STM32F101C4, STM32F101R4, STM32F101T4, STM32F101C6, STM32F101R6 and STM32F101T6   |
    | STM32F101xB | STM32F101C8, STM32F101R8, STM32F101T8, STM32F101V8, STM32F101CB, STM32F101RB, STM32F101TB and STM32F101VB  |
    | STM32F101xE | STM32F101RC, STM32F101VC, STM32F101ZC, STM32F101RD, STM32F101VD, STM32F101ZD, STM32F101RE, STM32F101VE and STM32F101ZE  |
    | STM32F101xG | STM32F101RF, STM32F101VF, STM32F101ZF, STM32F101RG, STM32F101VG and STM32F101ZG  |
    | STM32F102x6 | STM32F102C4, STM32F102R4, STM32F102C6 and STM32F102R6  |
    | STM32F102xB | STM32F102C8, STM32F102R8, STM32F102CB and STM32F102RB  |
    | STM32F103x6 | STM32F103C4, STM32F103R4, STM32F103T4, STM32F103C6, STM32F103R6 and STM32F103T6  |
    | STM32F103xB | STM32F103C8, STM32F103R8, STM32F103T8, STM32F103V8, STM32F103CB, STM32F103RB, STM32F103TB and STM32F103VB  |
    | STM32F103xE | STM32F103RC, STM32F103VC, STM32F103ZC, STM32F103RD, STM32F103VD, STM32F103ZD, STM32F103RE, STM32F103VE and STM32F103ZE  |
    | STM32F103xG | STM32F103RF, STM32F103VF, STM32F103ZF, STM32F103RG, STM32F103VG and STM32F103ZG  |
    | STM32F105xC | STM32F105R8, STM32F105V8, STM32F105RB, STM32F105VB, STM32F105RC and STM32F105VC  |
    | STM32F107xC | STM32F107RB, STM32F107VB, STM32F107RC and STM32F107VC |

     - ## NUCLEO使用時の注意
        NUCLEOのST-LINKから出力されるMCO(MasterClockOutput)をメインクロックで使用する場合、必ず回路図を確認してMCOとクロック入力ピンを接続してください。
※デフォルトでは接続されていない。ショート用パッドにハンダ付けして接続する

 - # デバイスの変更

   >  MakeFile冒頭(参考デバイスSTM32F103RBT)

        #project configuration
        PROJECT := F1xx_Project                     ・・・出力する実行ファイル名
        OPTIMIZE := -O0 -g3                         ・・・最適化オプションとデバッグオプション
        DEVICENAME := STM32F103xB                   ・・・使用するデバイスを定義します。定義名は上の表より選択してください
        STARTUP_FILE := startup_stm32f103xb.s       ・・・スタートアップファイル名を記述してください
        LINKERSCRIPT_FILE := STM32F103RBTx_FLASH.ld ・・・リンカースクリプト名を記述してください

 - ### バージョン情報
    |バージョン  |日付|更新内容 |
    |:-----:|:-------:|:----------------:|
    |ver1.0 |2017/3/18|READMEの記述|
    |ver1.01 |2017/8/12|コンパイル時に使用しているメモリを表示させるようにした|
    |ver1.0.2| 2018/3/26| 新規プロジェクトの作成を追記|
    |ver1.1.0|2018/3/28|UpdateDriverの追加、ドライバーの更新|
 - # ライセンス情報
    ## This software is released under the MIT License, see LICENSE