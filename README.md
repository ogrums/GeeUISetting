# GeeUISetting

System settings for the robot.

## Package

- `com.robot.geeui.setting`
- system uid
- The launcher is `ListActivity`, not `MainActivity`
- Permissions include `MASTER_CLEAR`, `WRITE_SECURE_SETTINGS`, and `REBOOT`

`GeeUIDesktop` launches this package as `PACKAGE_NAME_GEEUI_SETTINGS`.

## What it does

`ListActivity.initRecyclerview` builds the menu: About, Wi-Fi, Sound, Bluetooth, Wake and talk, Sleep, Date and time, Mode switching, Brightness, Shutdown, Update, Unbind and restore, Calibration. Mijia is added only when `SystemUtil.isInChinese()`.

Rows of type `activity` open `CommonBackActivity` and pass the row title as extra `fragment`. That activity hosts `BrightnessFragment`, `DateAndTimeFragment`, `ModeSwitchFragment`, `SleepFragment`, `WakeFragment`, `UnbindAndRestoreFragment`, `MijiaFragment`, and the nested screens `WakeWordFragment`, `WakeYinseFragment` (timbre), `SleepTimeFragment`, `TimeZoneFragment`, `Twenty4Fragment`, `UnbindFragment`, `RestoreFragment`, `LocalResetFragment`, and `ChargFragment`.

Dedicated activities: `DeviceInfoActivity`, `WifiActivity`, `SoundActivity`, `BlueActivity`, `ShutdownActivity`, `UpdateActivity`, `LanguageActivity`, `WalkActivity`, `OtherActivity`. `ResettingActivity` exists; its menu row is commented out. `MainActivity` is only a button into `ListActivity`.

`WifiActivity` reads the current SSID. `LocalResetFragment` is factory reset. `Util` compares versions by length first, then by characters. `SystemUtils` reads the ROM version and can bring auto-recharge to the foreground. `PickerView` is a scrolling wheel; the swipe comments describe passing the leave distance up or down.

## Outside this app

- `SettingService` binds `com.renhejia.robot.letianpaiservice` (`android.intent.action.LETIANPAI`) and keeps the binder. Log strings, not comments: "乐天派 完成AIDLService服务" means the bind finished, and "解除绑定aidlserver的AIDLService服务" means it unbound.
- Update starts `com.letianpai.otaservice` / `GeeUpdateService` (`ListActivity.openOta`).
- Calibration starts `com.letianpai.ltp_factory_test2.CalibrationActivity`.

Submodule: `GeeUIComponets` (`Components`, `CommChannel`).

## Comment glossary

| Where | Chinese | English |
|---|---|---|
| `WifiActivity` | 获取当前连接WIFI的SSID | SSID of the connected Wi-Fi |
| `LocalResetFragment` | 恢复出厂设置 | Factory reset |
| `ResettingActivity` | 恢复出厂设置 | Factory reset (the call is commented out) |
| `SystemUtils` | 自动回充前台 | Bring auto-recharge to the foreground |
| `SystemUtils` | 判断ROM版本号 | Read the ROM version |
| `Util` | 先比较长度 再比较字符 | Compare length first, then characters |
| `PickerView` | 滚动选择器 | Scrolling picker |
| `PickerView` | 往下滑超过离开距离 / 往上滑超过离开距离 | Swipe down or up past the leave distance |
