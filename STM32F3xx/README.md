
<div style="text-align: center; color:cyan;">
<h1>STM32F3ファミリー用GNU-GCCプロジェクト</h1>
</div>

- ## 概要
    STM32F3ファミリのプログラムをコンパイルするためのプロジェクト

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
    STM32F3xx
    ├── Apprication
    ├── Drivers
    │   ├── CMSIS
    │   │   ├── Device
    │   │   │   ├── Inc
    │   │   │   │   ├── デバイスのヘッダーファイル
    │   │   │   │   ├── stm32f3xx.h
    │   │   │   │   └── system_stm32f3xx.h
    │   │   │   └── Src
    │   │   │       ├── gcc
    │   │   │       │   └── スタートアップファイル
    │   │   │       └── system_stm32f3xx.c
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
    │   └── STM32F3xx_HAL_Driver
    │       ├── Inc
    │       │   ├── Legacy
    │       │   │   └── stm32_hal_legacy.h
    │       │   ├──HALドライバーのヘッダーファイル
    │       └── Src
    │           └── HALドライバーのソースファイル
    ├── Inc
    │   ├── mxconstants.h
    │   ├── stm32f3xx_hal_conf.h
    │   └── stm32f3xx_it.h
    ├── Makefile
    ├── UpdateDriver.sh
    ├── MidleWare
    ├── README.md
    └── Src
        ├── main.c
        ├── stm32f3xx_hal_msp.c
        └── stm32f3xx_it.c
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
        > ~/$ **git clone https://github.com/wakabayashiryo/STM32F3xx.git**   
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
    |デバイスのヘッダーファイル      | stm32f3xx**.h        | ./Drivers/CMSIS/Device/Inc    |
    |デバイスのスタートアップファイル   | startup_stm32f3xx**.s| ./Drivers/CMSIS/Device/Src/gcc|
    |リンカースクリプト | STM32F3XX**.ld| ./Drivers/LinkerScript      |
    |CMSISのヘッダーファイル | cmsis.h or core.h | ./Drivers/CMSIS/Inc|
    |HALドライバーのヘッダーファイル  | stm32_hal_*.h| ./Drivers/STM32F3xx_HAL_Driver/Inc|
    |HALドライバーのソースファイル   | stm32_hal_*.c| ./Drivers/STM32F3xx_HAL_Driver/Src|

- ## 対応デバイス
    
    |Define|Detail|
    |:-----:|:-------:|
    |  STM32F301x8  | STM32F301K6, STM32F301K8, STM32F301C6, STM32F301C8,STM32F301R6 and STM32F301R8   |
    |  STM32F302x8  | STM32F302K6, STM32F302K8, STM32F302C6, STM32F302C8,STM32F302R6 and STM32F302R8   |
    |  STM32F302xC  | STM32F302CB, STM32F302CC, STM32F302RB, STM32F302RC,STM32F302VB and STM32F302VC   |
    |  STM32F302xE  | STM32F302RE, STM32F302VE, STM32F302ZE, STM32F302RD,STM32F302VD and STM32F302ZD   |
    |  STM32F303x8  | STM32F303K6, STM32F303K8, STM32F303C6, STM32F303C8, STM32F303R6 and STM32F303R8   |
    |  STM32F303xC  | STM32F303CB, STM32F303CC, STM32F303RB, STM32F303RC,STM32F303VB and STM32F303VC   |
    |  STM32F303xE  | STM32F303RE, STM32F303VE, STM32F303ZE, STM32F303RD,STM32F303VD and STM32F303ZD   |
    |  STM32F373xC  | STM32F373C8, STM32F373CB, STM32F373CC,STM32F373R8, STM32F373RB, STM32F373RC,STM32F373V8, STM32F373VB and STM32F373VC  |
    |  STM32F334x8  | STM32F334K4, STM32F334K6, STM32F334K8,STM32F334C4, STM32F334C6, STM32F334C8,STM32F334R4, STM32F334R6 and STM32F334R8  |
    |  STM32F318xx  | STM32F318K8, STM32F318C8: STM32F301x8 with regulator off: STM32F318xx  |
    |  STM32F328xx  | STM32F328C8, STM32F328R8: STM32F334x8 with regulator off: STM32F328xx  |
    |  STM32F358xx  | STM32F358CC, STM32F358RC, STM32F358VC: STM32F303xC with regulator off: STM32F358xx |
    |  STM32F378xx  | STM32F378CC, STM32F378RC, STM32F378VC: STM32F373xC with regulator off: STM32F378xx |
    |  STM32F398xx  | STM32F398VE: STM32F303xE with regulator off: STM32F398xx |

     - ## NUCLEO使用時の注意
        NUCLEOのST-LINKから出力されるMCO(MasterClockOutput)をメインクロックで使用する場合、必ず回路図を確認してMCOとクロック入力ピンを接続してください。
※デフォルトでは接続されていない。ショート用パッドにハンダ付けして接続する
 - # デバイスの変更

   >  MakeFile冒頭(参考デバイスSTM32F303K8)

        #project configuration
        PROJECT := F3xx_Project                     ・・・出力する実行ファイル名
        OPTIMIZE := -O0 -g3                         ・・・最適化オプションとデバッグオプション
        HARDFP := 0                                 ・・・浮動小数点計算をハードウェアで行うか 0:Disable1:Enable
        DEVICENAME := STM32F303xE                   ・・・使用するデバイスを定義します。定義名は上の表より選択してください
        STARTUP_FILE := startup_stm32f303xe.s       ・・・スタートアップファイル名を記述してください
        LINKERSCRIPT_FILE := STM32F303RETx_FLASH.ld ・・・リンカースクリプト名を記述してください

 - ### バージョン情報
    |バージョン  |日付|更新内容 |
    |:-----:|:-------:|:----------------:|
    |ver1.0 |2017/3/18|READMEの記述|
    |ver1.01|2017/8/12 |コンパイル時に使用しているメモリを表示させた| 
    | ver 1.0.2| 2018/3/26| 新規プロジェクトの作成を追記|
    |ver1.1.0|2018/3/28|UpdateDriverの追加、ドライバーの更新|
 - # ライセンス情報
    ## This software is released under the MIT License, see LICENSE