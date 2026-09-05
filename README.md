# 广宁县建筑项目场景管理系统

一个基于高德地图卫星三维影像的建筑项目场景管理 Web 应用，用于展示广宁县各镇项目地点、航拍图、规划图及项目数据。

---

## 在线预览

部署到 GitHub Pages 后，访问地址为：

```
https://你的用户名.github.io/guangning-map-system/
```

---

## 核心功能

- **高德卫星三维地图**：默认定位肇庆市广宁县，支持缩放、拖拽、三维视角
- **项目地点标记**：带脉冲动画的缩略图标记，点击可查看详情
- **右侧详情面板**：展示项目标题、地址、数据字段、航拍图、规划图等
- **全局搜索**：支持按项目名称、地点/镇名搜索
- **镇级数据看板**：统计各镇项目数量、投资额、规划面积、项目类型分布
- **大屏风格**：深色底 + 蓝青色系科技感 UI

---

## 高德地图 Key 配置（重要）

本系统使用高德地图 JS API，需要您先申请高德地图 Key。

### 1. 申请 Key

1. 访问 [高德开放平台](https://lbs.amap.com/)
2. 注册/登录账号
3. 进入「控制台」→「应用管理」→「我的应用」
4. 创建新应用，添加 Key
   - 服务平台选择：**Web端(JS API)**
   - 启用服务：**JS API**、**Web服务API**
5. 复制 Key 字符串

### 2. 配置到项目

打开 `index.html`，找到第 23 行左右：

```javascript
AMapLoader.load({
    key: 'YOUR_AMAP_KEY',
    // ...
})
```

将 `YOUR_AMAP_KEY` 替换为您申请到的高德 Key。

### 3. 安全密钥配置（可选）

如果高德要求安全密钥，请将第 10 行的：

```javascript
window._AMapSecurityConfig = {
    securityJsCode: 'YOUR_SECURITY_CONFIG'
}
```

替换为真实的安全密钥，或删除整个 `window._AMapSecurityConfig` 代码块。

---

## GitHub Pages 部署步骤

### 方式一：直接上传文件

1. 在 GitHub 创建新仓库，命名为 `guangning-map-system`
2. 将本目录下的 `index.html` 和 `README.md` 上传到仓库根目录
3. 进入仓库 **Settings → Pages**
4. Source 选择 **Deploy from a branch**，分支选择 **main**，文件夹选择 **/(root)**
5. 保存后等待 1-2 分钟，即可通过 `https://你的用户名.github.io/guangning-map-system/` 访问

### 方式二：使用 Git 命令行

```bash
# 1. 进入项目目录
cd guangning-map-system

# 2. 初始化 Git 仓库
git init

# 3. 添加文件
git add .

# 4. 提交
git commit -m "init: 广宁县建筑项目场景管理系统"

# 5. 关联远程仓库（替换为你的仓库地址）
git remote add origin https://github.com/你的用户名/guangning-map-system.git

# 6. 推送
git push -u origin main
```

然后在 GitHub 仓库 Settings → Pages 中开启 GitHub Pages。

---

## 如何替换项目数据

所有项目数据都在 `index.html` 的 `projects` 数组中。每个项目对象结构如下：

```javascript
{
    id: 1,
    name: "项目名称",
    town: "所属镇街",
    address: "详细地址",
    lng: 112.4406,        // 经度
    lat: 23.6345,         // 纬度
    type: "项目类型",
    status: "项目状态",
    area: 125000,         // 规划面积（平方米）
    investment: 8.5,      // 投资额（亿元）
    target: "项目目标描述",
    manager: "负责人",
    startDate: "2025-03", // 预计开工时间
    duration: "36个月",   // 建设周期
    description: "项目简介",
    aerialImages: [       // 航拍图，可多张
        "图片路径1.jpg",
        "图片路径2.jpg"
    ],
    planImages: [         // 规划图，可多张
        "图片路径1.jpg",
        "图片路径2.jpg"
    ]
}
```

### 图片路径说明

- **相对路径**：如果图片放在仓库的 `images/` 目录下，路径写为 `"images/xxx.jpg"`
- **网络图片**：可以直接使用图片 URL
- **GitHub 图床**：也可以将图片上传到图床后使用外链

### 获取经纬度

1. 访问高德地图坐标拾取工具：https://lbs.amap.com/tools/picker
2. 搜索项目地点
3. 复制经纬度填入 `lng` 和 `lat`

---

## 注意事项

1. **高德 Key 必须配置正确**，否则地图无法加载
2. **GitHub Pages 访问高德 API** 时，需要在高德控制台配置正确的 **Web端(JS API)** 安全域名，或先不限制域名用于测试
3. 当前使用的图片为 `picsum.photos` 占位图，部署前请替换为真实项目图片
4. 如需修改默认中心点或缩放级别，请修改 `initMap()` 函数中的 `center` 和 `zoom` 参数

---

## 技术栈

- HTML5 + CSS3 + JavaScript（原生）
- 高德地图 JS API 2.0
- ECharts 5.x（数据可视化）
- GitHub Pages（静态部署）

---

## 本地预览

由于浏览器安全策略限制，直接在本地双击打开 `index.html` 可能无法加载高德地图。

建议使用本地服务器预览：

```bash
# 使用 Python
python -m http.server 8080

# 或使用 Node.js
npx serve .
```

然后访问 `http://localhost:8080`。
