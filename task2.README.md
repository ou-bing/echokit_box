i2s_task 作为核心的音频处理任务，使用 Tokio 的 spawn 方法异步启动。

afe_worker 接收音频数据，他也是在后台线程运行的。


## 项目的音频流走向

MIC -> ASR

- 1. 音频数据在 i2s_player_ 中采集并传入 AFE。

- 2. afe_worker 函数则会接收 AFE 吐出的数据，并使用 main 函数中定义的 evt_tx 向通道传入数据。

- 3. main_work 函数使用 main 函数中定义的 evt_rx 读取通道数据，并监听 MicAudioChunk 和 MicAudioEnd 事件，最后将相关数据发送到 ASR Server。





## 写入模型

espflash write-bin --baud=921600 0x710000 assets/srmodels.bin

## 使用分区表

espflash flash --baud=921600 --monitor --flash-size 16mb --partition-table partitions.csv target/xtensa-esp32s3-espidf/debug/echokit