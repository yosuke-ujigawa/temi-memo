### temi method
temiのsampleに含まれていた内容の自分用まとめ

layoutこしょこしょ話

```{#lst:id python caption="あいさつ"}
　 <ScrollView
        android:layout_width="wrap_content"
        android:layout_height="match_parent">

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="vertical">
            
            hogehoge
            
        </LinearLayout>
    </ScrollView>
```

## save_location
入力した場所現在地を登録する

layout
```{#lst:id python caption="あいさつ"}
            <EditText
                android:id="@+id/etSaveLocation"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:ems="10"
                android:gravity="center_horizontal"
                android:hint="@string/enter_location"
                android:inputType="textPersonName"
                android:textColor="@color/colorWhite"
                android:textColorHint="@color/colorGrey" />

            <Button
                android:id="@+id/btnSaveLocation"
                style="@style/ButtonCommon"
                android:text="@string/save_location" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * This is an example of saving locations.
     */
    private fun saveLocation() {
        val location =
                etSaveLocation.text.toString().toLowerCase(Locale.getDefault()).trim { it <= ' ' }
        val result = robot.saveLocation(location)
        if (result) {
            robot.speak(create("I've successfully saved the $location location.", true))
        } else {
            robot.speak(create("Saved the $location location failed.", true))
        }
        hideKeyboard()
    }

```


## Go to
上記で登録した場所に向かう
（「行き先は」「到着」のステータス表示）

layout
```{#lst:id python caption="あいさつ"}
           <EditText
                android:id="@+id/etGoTo"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="10dp"
                android:ems="10"
                android:gravity="center_horizontal"
                android:hint="@string/go_to_location"
                android:inputType="textPersonName"
                android:textColor="@color/colorWhite"
                android:textColorHint="@color/colorGrey" />

            <Button
                android:id="@+id/btnGoTo"
                style="@style/ButtonCommon"
                android:text="@string/go_to" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * goTo checks that the location sent is saved then goes to that location.
     */
    private fun goTo() {
        for (location in robot.locations) {
            if (location == etGoTo.text.toString().toLowerCase(Locale.getDefault())
                            .trim { it <= ' ' }
            ) {
                robot.goTo(
                        etGoTo.text.toString().toLowerCase(Locale.getDefault()).trim { it <= ' ' })
                hideKeyboard()
            }
        }
    }

```

## Speek
入力した言葉を喋ります
発言前に言語選択？ができる

layout
```{#lst:id python caption="あいさつ"}
            <EditText
                android:id="@+id/etSpeak"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="10dp"
                android:ems="10"
                android:gravity="center_horizontal"
                android:hint="@string/enter_speech"
                android:inputType="textPersonName"
                android:textColor="@color/colorWhite"
                android:textColorHint="@color/colorGrey" />

            <Button
                android:id="@+id/btnSpeak"
                style="@style/ButtonCommon"
                android:text="@string/speak" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * Have the robot speak while displaying what is being said.
     */
    private fun speak() {
        val text = etSpeak.text.toString()
        val languages = ArrayList<TtsRequest.Language>()
        languages.add(TtsRequest.Language.SYSTEM)
        languages.add(TtsRequest.Language.EN_US)
        languages.add(TtsRequest.Language.ZH_CN)
        languages.add(TtsRequest.Language.ZH_HK)
        languages.add(TtsRequest.Language.ZH_TW)
        languages.add(TtsRequest.Language.TH_TH)
        languages.add(TtsRequest.Language.HE_IL)
        languages.add(TtsRequest.Language.KO_KR)
        languages.add(TtsRequest.Language.JA_JP)
        languages.add(TtsRequest.Language.IN_ID)
        languages.add(TtsRequest.Language.ID_ID)
        languages.add(TtsRequest.Language.DE_DE)
        languages.add(TtsRequest.Language.FR_FR)
        languages.add(TtsRequest.Language.FR_CA)
        languages.add(TtsRequest.Language.PT_BR)
        languages.add(TtsRequest.Language.AR_EG)
        languages.add(TtsRequest.Language.AR_AE)
        languages.add(TtsRequest.Language.AR_XA)
        languages.add(TtsRequest.Language.RU_RU)
        languages.add(TtsRequest.Language.IT_IT)
        languages.add(TtsRequest.Language.PL_PL)
        languages.add(TtsRequest.Language.ES_ES)
        val adapter = ArrayAdapter(this, R.layout.item_dialog_row, R.id.name, languages)
        val dialog = AlertDialog.Builder(this)
                .setTitle("Select Speaking Language")
                .setAdapter(adapter, null)
                .create()
        dialog.listView.onItemClickListener =
                OnItemClickListener { _: AdapterView<*>?, _: View?, position: Int, _: Long ->
                    val ttsRequest =
                            create(text, language = adapter.getItem(position)!!, showAnimationOnly = true)
                    robot.speak(ttsRequest)
                    printLog("Speak: ${adapter.getItem(position)}")
                    dialog.dismiss()
                }
        dialog.show()
        hideKeyboard()
    }

```

## colorGrey
設定変更の許可のポップアップが出たけど何をしているか不明

layout
```{#lst:id python caption="あいさつ"}
            <EditText
                android:id="@+id/etDistance"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="10dp"
                android:ems="10"
                android:gravity="center_horizontal"
                android:hint="Please enter the distance"
                android:inputType="numberDecimal"
                android:maxLines="1"
                android:textColor="@color/colorWhite"
                android:textColorHint="@color/colorGrey" />

            <Button
                android:id="@+id/btnStartDetectionModeWithDistance"
                style="@style/ButtonCommon"
                android:text="Start Detection Mode with Distance" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Start NLU
???

layout
```{#lst:id python caption="あいさつ"}
            <EditText
                android:id="@+id/etNlu"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="10dp"
                android:gravity="center_horizontal"
                android:hint="@string/enter_speech"
                android:textColor="@color/colorWhite"
                android:textColorHint="@color/colorGrey" />

            <Button
                android:id="@+id/btnNlu"
                style="@style/ButtonCommon"
                android:text="Start NLU" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Go to Position
1,1,0で実行すると「不明不明不明」怖かった

layout
```{#lst:id python caption="あいさつ"}
            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginLeft="50dp"
                android:layout_marginTop="10dp"
                android:layout_marginRight="50dp"
                android:orientation="horizontal">

                <EditText
                    android:id="@+id/etX"
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:gravity="center_horizontal"
                    android:hint="x"
                    android:textColor="@color/colorWhite"
                    android:textColorHint="@color/colorGrey" />

                <EditText
                    android:id="@+id/etY"
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:gravity="center_horizontal"
                    android:hint="y"
                    android:textColor="@color/colorWhite"
                    android:textColorHint="@color/colorGrey" />

                <EditText
                    android:id="@+id/etYaw"
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:gravity="center_horizontal"
                    android:hint="yaw"
                    android:textColor="@color/colorWhite"
                    android:textColorHint="@color/colorGrey" />
            </LinearLayout>

            <Button
                android:id="@+id/btnGoToPosition"
                style="@style/ButtonCommon"
                android:text="Go To Position" />

```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun goToPosition() {
        try {
            val x = etX.text.toString().toFloat()
            val y = etY.text.toString().toFloat()
            val yaw = etYaw.text.toString().toFloat()
            robot.goToPosition(Position(x, y, yaw, 0))
        } catch (e: Exception) {
            e.printStackTrace()
            printLog(e.message ?: "")
        }
    }
```

## ここから二行目

## Current Fllor
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnGetCurrentFloor"
                style="@style/ButtonCommon"
                android:text="Current Floor" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## load Floor At Elevator
マップの読み込み許可のポップアップ
マップの読み込み？
登録地点を読み込んでる

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnLoadFloorAtElevator"
                style="@style/ButtonCommon"
                android:text="Load Floor At Elevator" />

```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Get All Floors
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnGetAllFloors"
                style="@style/ButtonCommon"
                android:text="Get All Floors" />

```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Is Back TOF Enabled
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnIsBackTOFEnabled"
                style="@style/ButtonCommon"
                android:text="Is Back TOF Enabled" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Toggle Back TOF
aaa

layout
```{#lst:id python caption="あいさつ"}
           <Button
                android:id="@+id/btnToggleBackTOF"
                style="@style/ButtonCommon"
                android:text="Toggle Back TOF" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Toggle Front TOF
aaa

layout
```{#lst:id python caption="あいさつ"}
           <Button
                android:id="@+id/btnToggleFrontTOF"
                style="@style/ButtonCommon"
                android:text="Toggle Front TOF" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Get Head Depth Sensitivity
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnGetHeadDepthSensitivity"
                style="@style/ButtonCommon"
                android:text="Get Head Depth Sensitivity" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Set Head Depth Sensitivity
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnSetHeadDepthSensitivity"
                style="@style/ButtonCommon"
                android:text="Set Head Depth Sensitivity" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Get Cliff Sensor Mode
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnGetCliffSensorMode"
                style="@style/ButtonCommon"
                android:text="Get Cliff Sensor Mode" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Set Cliff Sensor Mode
テキスト行212残り50個以上きりがないんすわぶっとばすね

layout
```{#lst:id python caption="あいさつ"}
                android:id="@+id/btnSetCliffSensorMode"
                style="@style/ButtonCommon"
                android:text="Set Cliff Sensor Mode" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Mute Alexa
284
アレクサの無効化？

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnMuteAlexa"
                style="@style/ButtonCommon"
                android:text="Mute Alexa" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun muteAlexa() {
        if (robot.launcherVersion.contains("usa")) {
            printLog("Mute Alexa")
            robot.muteAlexa()
            return
        }
        printLog("muteAlexa() is useful only for Global version")
    }

```
## Shutdown
押しても落ちなかった

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnShutdown"
                style="@style/ButtonCommon"
                android:text="Shutdown" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun shutdown() {
        if (!robot.isSelectedKioskApp()) {
            return
        }
        val builder = AlertDialog.Builder(this@MainActivity)
        builder.setTitle("Shutdown temi?").create()
        builder.setPositiveButton("Yes") { _: DialogInterface?, _: Int ->
            printLog("shutdown")
            robot.shutdown()
        }
        builder.setNegativeButton("No") { _: DialogInterface?, _: Int -> }
        builder.create().show()
    }
```

## Lock
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnLock"
                style="@style/ButtonCommon"
                android:text="Lock" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun lock() {
        robot.locked = true
        printLog("Is temi locked: " + robot.locked)
    }
```

## Unlock
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnUnlock"
                style="@style/ButtonCommon"
                android:text="Unlock" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun unlock() {
        robot.locked = false
        printLog("Is temi locked: " + robot.locked)
    }
```

## Load Map
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnLoadMap"
                style="@style/ButtonCommon"
                android:text="Load Map" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun loadMap(reposeRequired: Boolean, position: Position?) {
        if (mapList.isEmpty()) {
            getMapList()
        }
        if (robot.checkSelfPermission(Permission.MAP) != Permission.GRANTED) {
            return
        }
        val mapListString: MutableList<String> = ArrayList()
        for (i in mapList.indices) {
            mapListString.add(mapList[i].name)
        }
        val mapListAdapter = ArrayAdapter(this, R.layout.item_dialog_row, R.id.name, mapListString)
        val builder = AlertDialog.Builder(this)
        builder.setTitle("Click item to load specific map")
        builder.setAdapter(mapListAdapter, null)
        val dialog = builder.create()
        dialog.listView.onItemClickListener =
                OnItemClickListener { _: AdapterView<*>?, _: View?, pos: Int, _: Long ->
                    printLog("Loading map: " + mapList[pos])
                    if (position == null) {
                        robot.loadMap(mapList[pos].id, reposeRequired)
                    } else {
                        robot.loadMap(mapList[pos].id, reposeRequired, position)
                    }
                    dialog.dismiss()
                }
        dialog.show()
    }




    private fun loadMap() {
        loadMap(false, null)
    }
   
```

## Repose
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnRepose"
                style="@style/ButtonCommon"
                android:text="Repose" />

```
MainActivity
```{#lst:id python caption="あいさつ"}
def greeting():
   print ("Hello World!")
```

## Get Volume
現状の音量表示

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnGetVolume"
                style="@style/ButtonCommon"
                android:text="Get Volume" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun getVolume() {
        printLog("Current volume is: " + robot.volume)
    }
```

## Set Volume
0-10で音量をセット出来る

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnSetVolume"
                style="@style/ButtonCommon"
                android:text="Set Volume" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun setVolume() {
        if (requestPermissionIfNeeded(Permission.SETTINGS, REQUEST_CODE_NORMAL)) {
            return
        }
        val volumeList: List<String> =
                ArrayList(listOf("0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "10"))
        val adapter = ArrayAdapter(this, R.layout.item_dialog_row, R.id.name, volumeList)
        val dialog = AlertDialog.Builder(this)
                .setTitle("Set Volume")
                .setAdapter(adapter, null)
                .create()
        dialog.listView.onItemClickListener =
                OnItemClickListener { _: AdapterView<*>?, _: View?, position: Int, _: Long ->
                    robot.volume = adapter.getItem(position)!!.toInt()
                    printLog("Set volume to ${adapter.getItem(position)}")
                    dialog.dismiss()
                }
        dialog.show()
    }

```

## follow_me
追従モード

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnFollow"
                style="@style/ButtonCommon"
                android:text="@string/follow_me" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * Simple follow me example.
     */
    private fun followMe() {
        robot.beWithMe()
        hideKeyboard()
    }
```

## skidjoy
aaa

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnskidJoy"
                style="@style/ButtonCommon"
                android:text="@string/skidjoy" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * Manually navigate the robot with skidJoy, tiltAngle, turnBy and tiltBy.
     * skidJoy moves the robot exactly forward for about a second. It controls both
     * the linear and angular velocity. Float numbers must be between -1.0 and 1.0
     */
    private fun skidJoy() {
        val t = System.currentTimeMillis()
        val end = t + 500
        val speedX = try {
            etX.text.toString().toFloat()
        } catch (e: Exception) {
            1f
        }
        val speedY = try {
            etY.text.toString().toFloat()
        } catch (e: Exception) {
            0f
        }
        printLog("speedX: $speedX, speedY: $speedY")
        while (System.currentTimeMillis() < end) {
            robot.skidJoy(speedX, speedY)
        }
    }
```

## tiltangle
画面上向く

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnTiltAngle"
                style="@style/ButtonCommon"
                android:text="@string/tiltangle" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * tiltAngle controls temi's head by specifying which angle you want
     * to tilt to and at which speed.
     */
    private fun tiltAngle() {
        val speed = try {
            etDistance.text.toString().toFloat()
        } catch (e: Exception) {
            1f
        }
        robot.tiltAngle(23, speed)
    }
```

## tiltBy
画面下向く

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnTiltBy"
                style="@style/ButtonCommon"
                android:text="tiltBy" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * tiltBy is used to tilt temi's head from its current position.
     */
    private fun tiltBy() {
        val speed = try {
            etDistance.text.toString().toFloat()
        } catch (e: Exception) {
            1f
        }
        robot.tiltBy(70, speed)
    }
```

## turnby
左90度回転

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnTurnBy"
                style="@style/ButtonCommon"
                android:text="@string/turnby" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    private fun turnBy() {
        val speed = try {
            etDistance.text.toString().toFloat()
        } catch (e: Exception) {
            1f
        }
        robot.turnBy(90, speed)
    }
```

## stop_movement
動作停止

layout
```{#lst:id python caption="あいさつ"}
            <Button
                android:id="@+id/btnStopMovement"
                style="@style/ButtonCommon"
                android:text="@string/stop_movement" />
```
MainActivity
```{#lst:id python caption="あいさつ"}
    /**
     * stopMovement() is used whenever you want the robot to stop any movement
     * it is currently doing.
     */
    private fun stopMovement() {
        robot.stopMovement()
        robot.speak(create("And so I have stopped", true))
    }
```



あとはバッテリー情報、上のバー表示非表示、移動速度のセッティング
