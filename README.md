2024/09/18 更新

#### FXシリーズ内部の温度を確認、温度アラートを検知する。

---

#### Browser Settings による確認

1. CPU温度の確認

   "Status" > "Temprature""

   ![1718267190149](image/README/1718267190149.png)

   * **Temperature: **Display current temperature of reader in Celsius and Fahrenheit.

   </br>
2. 温度イベント（High, Critical )発生回数の確認

   "Operation Statistics" > "Events"

   ![1718267163207](image/README/1718267163207.png)

   | Event                           | Defenition                                                                   | Threshold (Celsius)<br />FX9600 | Threshold (Celsius)<br />FX7500 |
   | ------------------------------- | ---------------------------------------------------------------------------- | ------------------------------- | ------------------------------- |
   | AmbientTemperatureHighAlarm     | Displays the number of events raised for ambient temperature high alarm.     | 127                             | 75                              |
   | AmbientTemperatureCriticalAlarm | Displays the number of events raised for ambient temperature critical alarm. | 127                             | 85                              |
   | PATemperatureHighAlarm          | Displays the number of events raised for PA temperature high alarm.          | 127                             | 105                             |
   | PATemperatureCriticalAlarm      | Displays the number of events raised for PA temperature critical alarm.      | 127                             | 125                             |

   </br>

   #### 用語解説

   The device has 2 temperature probes. It measures the temperature around the device (ambient) which can be higher than the actual environment temperature since the device emits heat. PA temp is related to Power Amplifier (PA) temperature. If the alarms are created the device is ‘running hot’. High alarm makes the device change the duty cycle, critical stops the RF section of the device to allow to cool down.

   | Terms                            | Definition                                   |
   | -------------------------------- | -------------------------------------------- |
   | Ambient temperature              | デバイス基板周囲の温度のこと。               |
   | Power Amplifier (PA) temperature | デバイス電力増幅モジュール周囲の温度のこと。 |

   </br>

   イベントは下記方法で収集が可能。

   - Browser Settings > System Log
   - /var/log/messages
   - Syslog サーバにてSystem Logを受信
   - API経由でEventを収集


   </br>

   #### API経由で取得について

   APIは下記の様にアラートデータを出力する。

   ##### API Format

   ```
   private TEMPERATURE_SOURCE m_sourceName;  {can be PA or Ambient}
   private ushort m_currentTemperature; {Temperature in deg Celsius}
   private ALARM_LEVEL m_AlarmLevel; {Low, High or Critical}
   ```

   ##### 例、情報取得(PA High Alert)
   ```
   Status Notification: TEMPERATURE_ALARM_EVENT
   Source: PA
   Temperature: 53
   Alarm Level: HIGH
   ```
