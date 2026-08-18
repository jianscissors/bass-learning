# 贝斯练习工具

在线地址：**https://jianscissors.github.io/bass-learning/**

麦克风驱动的贝斯练习小工具集，纯静态网页，无需安装、无需登录，数据都存在本地浏览器（localStorage），不上传到任何服务器。

## 工具列表

| 工具 | 链接 | 说明 |
|---|---|---|
| 🎸 指板速认 | [index.html](https://jianscissors.github.io/bass-learning/) | 随机报音/音程，在真琴上弹出来，麦克风听你弹得对不对；支持任意弦/单弦轮换/全指板三种规则 |
| 🥁 节奏跟弹 | [rhythm.html](https://jianscissors.github.io/bass-learning/rhythm.html) | 节拍器 + 麦克风拍点检测，判断拨弦是抢拍、拖拍还是踩得准 |
| 🎧 音程耳音 | [ear-training.html](https://jianscissors.github.io/bass-learning/ear-training.html) | 纯听力练耳，音域限定在贝斯常用的低音区（不是随便找个中央 C 附近糊弄） |
| 🎚️ 分轨播放 | [stem-mixer.html](https://jianscissors.github.io/bass-learning/stem-mixer.html) | 加载分离好的音轨（鼓/贝斯/人声/其他），贝斯调大其他调小，辅助扒谱听歌 |

每个工具都有独立的"学习记录"面板（练习时长、正确率、连对等），存在浏览器本地，换设备不会同步。

## 技术

- 纯 HTML/CSS/JS，无构建步骤，`theme.css` 是三个工具共用的设计系统
- 音高识别用浏览器自带的 Web Audio API（自相关算法），不依赖外部服务
- 节奏检测用 `ScriptProcessorNode` 做采样级精度的起振检测，和节拍器共用同一个音频时钟

## 关于扒谱/分轨

"分轨播放"工具本身只是个播放器，音源分离（把一首歌拆成鼓/贝斯/人声/其他）需要用 [demucs](https://github.com/facebookresearch/demucs) 在本地跑，这一步不在网页里自动完成——GitHub Pages 是纯静态托管，跑不了 Python；而且把"输入任意链接自动下载并分离"做成公开网页功能，等于是个自动扒别人版权内容的工具，这个不太合适公开发布。

目前的流程是本地手动跑：给一首歌（本地文件或链接），本地用 demucs 分离出音轨文件，再把生成的 `drums.wav` / `bass.wav` / `vocals.wav` / `other.wav` 丢进"分轨播放"这个页面就能用。
