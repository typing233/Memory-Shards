# 💕 Memory Shards - 情侣拼图游戏

一款让情侣通过轮流拼凑彼此上传的照片碎片，共同还原并融合专属回忆的轻量级互动小游戏。

## ✨ 功能特点

- 📸 **双人图片上传**：支持两位用户各上传一张照片
- 🧩 **智能拼图切割**：每张照片自动切成3块，共6块拼图碎片
- 🎮 **拖拽交互**：流畅的拖拽体验，碎片靠近正确位置时自动吸附
- ✨ **自动吸附**：当碎片靠近正确位置时会自动吸附到目标位置
- 🎆 **浪漫特效**：拼图完成后触发烟花动画和成功提示
- 🎵 **成功音效**：使用Web Audio API播放欢快的成功旋律
- 💕 **图片融合**：展示两张照片重叠融合的最终画面
- 📱 **响应式设计**：支持桌面端和移动端

## 🚀 快速开始

### 环境要求

- Python 3.7+
- pip 包管理器

### 安装步骤

1. **克隆或下载项目**

```bash
cd Memory-Shards
```

2. **安装依赖**

```bash
pip install -r requirements.txt
```

3. **启动服务器**

```bash
python app.py
```

4. **访问应用**

打开浏览器访问：`http://localhost:3765`

## 🎮 使用说明

### 游戏流程

1. **上传照片**
   - 用户1和用户2分别上传一张照片
   - 支持点击上传或拖拽图片上传
   - 支持的格式：PNG、JPG、JPEG、GIF、WebP

2. **开始游戏**
   - 两张照片上传完成后，点击"开始拼图游戏"按钮
   - 系统会将两张照片各切成3块，共6块碎片
   - 碎片会随机打乱并显示在右侧碎片区域

3. **拼图过程**
   - 从右侧碎片区域拖拽碎片到左侧拼图区域
   - 当碎片中心靠近正确位置时会自动吸附
   - 每放置一块正确的碎片，进度条会更新
   - 已放置的碎片会从碎片区域移除

4. **完成游戏**
   - 当6块碎片全部放置正确后，触发成功画面
   - 显示烟花动画特效
   - 播放欢快的成功音效
   - 展示两张照片融合的最终画面
   - 显示随机的浪漫祝福文字

### 玩法建议

- **同一设备游玩**：两位用户可以在同一台设备上轮流操作
- **截图交流**：一位用户可以截图发给另一位，远程协作完成
- **甜蜜回忆**：上传有纪念意义的照片，增加游戏趣味性

## 📁 项目结构

```
Memory-Shards/
├── app.py              # Flask 后端服务器
├── requirements.txt    # Python 依赖列表
├── README.md           # 项目说明文档
├── templates/
│   └── index.html      # 前端页面（包含所有游戏逻辑）
├── uploads/            # 上传的图片存储目录
└── static/             # 静态资源目录
```

## 🔧 技术栈

### 后端
- **Flask** - 轻量级Python Web框架
- **Flask-CORS** - 跨域请求处理

### 前端
- **HTML5 Canvas** - 拼图绘制和图片处理
- **原生JavaScript** - 游戏逻辑实现
- **CSS3** - 响应式样式和动画
- **Web Audio API** - 音效生成
- **Drag & Drop API** - 拖拽交互

## 🎨 核心功能实现

### 图片切割算法
```javascript
// 每张图片切成 3 列 × 2 行 = 6 块
// 实际上每张图片取上半部分切成 3 块
// 最终两张图片共 6 块拼图碎片
```

### 自动吸附逻辑
```javascript
// 计算碎片中心点位置
const centerX = x + cellWidth / 2;
const centerY = y + cellHeight / 2;

// 判断是否在目标位置附近
const col = Math.floor(centerX / cellWidth);
const row = Math.floor(centerY / cellHeight);

// 如果是正确位置且未被占用，则自动吸附
if (col === piece.targetX && row === piece.targetY) {
    placePiece(piece, col, row);
}
```

### 烟花粒子系统
- 使用Canvas实现粒子动画
- 随机颜色和位置
- 物理引擎模拟重力和阻力
- 多轮烟花绽放效果

### 图片融合效果
```javascript
// 使用 Canvas 全局透明度实现两张图片叠加
ctx.globalAlpha = 0.5;
drawCoverImage(ctx, img1, width, height);
ctx.globalAlpha = 0.5;
drawCoverImage(ctx, img2, width, height);

// 添加浪漫滤镜效果
ctx.globalCompositeOperation = 'overlay';
// 绘制径向渐变滤镜
```

## 🌐 部署说明

### 本地开发
```bash
python app.py
# 访问 http://localhost:3765
```

### 生产环境建议
1. 使用 Gunicorn 或 uWSGI 作为WSGI服务器
2. 使用 Nginx 作为反向代理
3. 配置适当的文件上传大小限制
4. 考虑使用 CDN 加速静态资源

## 📝 配置选项

### 修改端口
在 `app.py` 中修改：
```python
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=3765, debug=True)
```

### 修改拼图大小
在 `index.html` 的 `puzzleState` 对象中修改：
```javascript
gridCols: 3,    // 列数
gridRows: 2,    // 行数
```

### 修改文件上传限制
在 `app.py` 中修改：
```python
app.config['MAX_CONTENT_LENGTH'] = 16 * 1024 * 1024  # 16MB
```

## 🐛 常见问题

**Q: 图片上传失败？**
- 检查图片格式是否支持（PNG、JPG、JPEG、GIF、WebP）
- 检查图片大小是否超过16MB
- 检查 `uploads` 目录权限

**Q: 拖拽不流畅？**
- 建议使用现代浏览器（Chrome、Firefox、Safari）
- 检查是否有其他浏览器扩展干扰

**Q: 没有声音？**
- 检查浏览器是否允许自动播放音频
- 某些浏览器需要用户先点击页面才能播放声音

## 📄 许可证

MIT License

## 💡 贡献

欢迎提交 Issue 和 Pull Request！

---

**💕 祝你们玩得开心，拼凑更多甜蜜回忆！💕**
