# 🔥 让你的桌面养一只"代码媛"！程序员的摸鱼神器来了！

**「每天对着屏幕写BUG，不如养只小老虎陪你摸鱼」**

---

## 📖 项目起源

作为一名程序员，每天面对最多的就是：

```
需求评审 📋 → 写代码 💻 → BUG调试 🐛 → 需求变更 📝 → 继续加班 🌙
```

有一天我在摸鱼的时候突发奇想：**为什么我的桌面不能有一只小宠物陪我coding呢？**

于是就有了这个项目 —— **DesktopPet**，一只会说话的小老虎！

---

## 🎯 它能做什么？

### 功能演示

| 功能 | 说明 |
|------|------|
| 🐯 **随机待机动画** | 3种GIF动画随机切换，永不重复 |
| 💬 **自动播放语录** | 每3秒随机说一条程序员黑话 |
| 🖱️ **拖拽移动** | 鼠标左键拖动，想放哪放哪 |
| 👆 **点击互动** | 点击小老虎，它会"咬"你一口 |
| 🍔 **右键菜单** | 显示/隐藏/退出，简单实用 |
| 📌 **托盘运行** | 最小化到托盘，不占用任务栏 |

---

## 💬 语录大赏

我的 `dialog.txt` 里写满了程序员黑话：

```
Hello World!
996 ICU
BUG呢？BUG去哪了？
需求改改改
我写的代码没有bug
Ctrl+C Ctrl+V
Stack Overflow救我
今天不加班
代码能跑就行
注释？什么注释？
Python是最好的语言
TypeError: 'NoneType' object is not callable
递归：如果你知道什么是递归，那就不用解释了
缓存过期了吗？
404 Not Found
Git merge冲突了
npm install失败了
单元测试？不存在的
上线前：代码完美；上线后：谁写的垃圾代码
测试环境：一切正常；生产环境：当场去世
```

**你品，你细品，是不是每一条都在戳你的心窝子？** 😭

---

## 🛠️ 技术栈

这个项目用到的技术：

| 技术 | 用途 |
|------|------|
| **Python 3** | 编程语言 |
| **PyQt5** | GUI图形界面框架 |
| **QLabel** | 显示GIF动画 |
| **QMovie** | 播放GIF动图 |
| **QTimer** | 定时器，控制语录切换 |
| **QSystemTrayIcon** | 系统托盘功能 |
| **mouseEvent** | 鼠标事件处理 |

**整个项目只有250行代码，非常适合新手学习！**

---

## 🚀 快速开始

### 1️⃣ 环境要求

- Python 3.7 或更高版本
- Windows/Linux/MacOS（理论上支持所有平台）

### 2️⃣ 安装依赖

```bash
pip install PyQt5
```

### 3️⃣ 运行程序

```bash
cd DesktopPet
python main.py
```

然后你就会看到一只小老虎出现在屏幕上！

---

## 📁 项目结构详解

```
DesktopPet/
│
├── main.py              # 🎯 主程序入口，包含所有核心逻辑
│
├── dialog.txt           # 💬 语录配置文件，每行一条，支持中文
│
├── tigerIcon.jpg        # 🖼️ 托盘图标（16x16 ~ 256x256）
│
├── normal/              # 📽️ 待机动画目录（可随意添加GIF）
│   ├── normal1.gif
│   ├── normal2.gif
│   └── normal3.gif
│
└── click/               # 📽️ 点击动画目录
    └── click.gif
```

---

## 🔍 核心代码解析

### 1. 窗口初始化 - 无边框 + 透明

```python
def init(self):
    # 设置窗口属性:窗口无标题栏且固定在最前面
    self.setWindowFlags(
        Qt.FramelessWindowHint |  # 无边框窗口
        Qt.WindowStaysOnTopHint |  # 窗口总显示在最上面
        Qt.SubWindow               # 子窗口
    )
    self.setAutoFillBackground(False)
    self.setAttribute(Qt.WA_TranslucentBackground, True)  # 透明背景
```

**效果**：窗口没有标题栏，但可以通过鼠标拖动移动位置。

### 2. GIF动画播放

```python
def initPetImage(self):
    self.movie = QMovie("normal/normal1.gif")
    self.movie.setScaledSize(QSize(200, 200))  # 设置播放尺寸
    self.image.setMovie(self.movie)
    self.movie.start()
```

### 3. 随机语录播放

```python
def talk(self):
    # 从语录列表中随机选择一条
    self.talkLabel.setText(random.choice(self.dialog))
    self.talkLabel.setStyleSheet(self.getTalkStyle())
    self.talkLabel.adjustSize()
```

### 4. 鼠标拖拽移动

```python
def mousePressEvent(self, event):
    if event.button() == Qt.LeftButton:
        self.is_follow_mouse = True  # 开始跟随
    self.mouse_drag_pos = event.globalPos() - self.pos()

def mouseMoveEvent(self, event):
    if Qt.LeftButton and self.is_follow_mouse:
        self.move(event.globalPos() - self.mouse_drag_pos)  # 跟随移动
```

---

## 🎨 自定义改造

### 1. 更换宠物外观

只需要替换 `normal/` 和 `click/` 目录下的GIF图片即可！

```
建议尺寸：200x200 像素
格式：GIF（支持透明背景）
```

### 2. 修改语录内容

编辑 `dialog.txt`，想说什么就写什么！

```
🌟 示例：改成心灵鸡汤
今天也要加油鸭！
bug终将被消灭！
代码改变世界！
```

### 3. 更换托盘图标

替换 `tigerIcon.jpg` 即可，建议尺寸 16x16 像素。

---

## 📦 打包成exe

想要把程序分享给同事？打包成exe！

### 1. 安装打包工具

```bash
pip install pyinstaller
```

### 2. 执行打包命令

```bash
pyinstaller --onefile --windowed --icon=tigerIcon.jpg --name=DesktopPet main.py
```

### 3. 查找exe文件

打包完成后，exe文件位于：
```
dist/DesktopPet.exe
```

### ⚠️ 注意事项

打包后的exe运行时，资源文件路径会发生变化。项目代码中已经添加了 `get_resource_path()` 函数来自动处理这个问题，**无需额外修改**！

---

## 💡 扩展思路

这个项目还有很多可以扩展的方向：

| 扩展功能 | 实现难度 | 说明 |
|---------|---------|------|
| 🐾 投喂零食 | ⭐⭐ | 添加喂食动画和互动 |
| ☀️ 天气播报 | ⭐⭐ | 调用API显示天气 |
| ⏰ 番茄钟 | ⭐⭐ | 定时提醒休息 |
| 🎵 音乐控制 | ⭐⭐⭐ | 桌面歌词显示 |
| 💭 今日格子 | ⭐ | 显示工作日志 |

---

## 🤔 常见问题

### Q: 为什么窗口拖不动？
> 检查是否在无边框模式下实现了 `mousePressEvent` 和 `mouseMoveEvent`

### Q: GIF动画不显示？
> 确保GIF文件路径正确，且文件格式支持

### Q: 中文显示乱码？
> 确保 `dialog.txt` 文件编码为 **UTF-8**

### Q: 托盘图标不显示？
> 检查 `tigerIcon.jpg` 是否存在，路径是否正确

---

## 📢 写在最后

> **"代码是写不完的，但摸鱼是必须的"**

这只小老虎或许不能帮你写代码，但它能：

- 😄 在你debug崩溃时给你一点心理安慰
- 😂 用程序员黑话替你发泄心中的不满
- 🐯 让你的桌面不再单调乏味

---

**如果你觉得这个项目有意思，欢迎：**

- ⭐ **Star** 支持一下
- 🍴 **Fork** 二次开发
- 💬 **评论** 区聊聊你们的"程序员黑话"

也可以在评论区留下你想让小老虎说的话，我会挑选有趣的加入默认语录！

---

**项目地址**：[你的GitHub仓库地址]

**完整代码**：[CSDN下载链接]

---

#Python #PyQt5 #桌面宠物 #程序员 #摸鱼神器 #GUI #开源项目 #HelloWorld #桌面宠物开发