i2s_task 作为核心的音频处理任务，使用 Tokio 的 spawn 方法异步启动。

afe_worker 接收音频数据，他也是在后台线程运行的。


## 项目的音频流走向

MIC -> ASR

- 1. 音频数据在 i2s_player_ 中采集并传入 AFE。

- 2. afe_worker 则会接收 AFE 吐出的数据，并传入 main 函数中定义的 evt_tx 通道。

- 3. main_work 监听 MicAudioChunk 和 MicAudioEnd 事件，并将相关数据发送到 ASR Server。

