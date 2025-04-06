# 人生周历

这是一个交互式的人生地图，每个小方框代表我生命中的一周。方框的边框颜色代表我生活的地点，填充颜色代表我在做什么。点击方框可以查看那一周我在哪里做什么。

我创建这个项目是为了帮助自己看清人生路上的全景图。

这段代码改编自[Buster Benson](https://busterbenson.com/life-in-weeks)。它是一个使用[Hugo](https://gohugo.io/)静态渲染的单页网站，托管在Netlify上。主要由[两个数据文件](data/events.yml)[和颜色定义](data/colors.yml)、[一个简介页面](content/index.md)和[一个模板](layouts/_default/index.html)组成。

## 🚀 安装

1. 安装Hugo:
   ```sh
   brew install hugo  # Mac系统
   ```
2. 克隆并在本地运行:
```sh
    git clone https://github.com/33Enigma/life-in-weeks.git
    cd life-in-weeks
    hugo server -D
```
3. 访问 [http://localhost:1313/](http://localhost:1313/)。

## ✨ 自定义内容

本项目提供了多种自定义选项，以下是详细的自定义指南：

### 基本信息自定义 (hugo.toml)

修改 `hugo.toml` 文件可以更改站点的基本信息：
```toml
baseURL = '你的网站URL'
languageCode = 'zh-cn'  # 可以改为中文
title = '我的人生周历'
disableKinds = ["taxonomy", "taxonomy"]
enableEmoji = true

[params]
author = "你的名字"
```

### 个人简介自定义 (content/index.md)

修改 `content/index.md` 可以自定义首页上方的个人介绍：
```markdown
---
title       : 我的人生周历
description : 这是我生命的地图，每个小方框代表我生命中的一周。
start_date  : 1990-01-01  # 改为你的出生日期
end_year    : 2090        # 改为你期望的结束年份
---

👋 嗨，我是[你的名字](你的个人网站链接)。这是我生命的地图，每个小方框代表我生命中的一周。点击方框可以看到那时我在做什么。

🌱 这个人生地图正在进行中。我会不断更新它。

🍯 我的人生格言 - "把研究当作休闲活动。"
```

### 生活事件自定义 (data/events.yml)

`data/events.yml` 是整个网站最核心的数据文件，记录了你生命中的所有重要事件：

```yaml
# 第一个事件应该是出生
# 日期应该与content/index.md中的start_date匹配
"1990-01-01":
    - headline: "🐣 我出生了"
      description: "我在北京出生，是家里的第一个孩子。"
      based: "北京"  # 居住地点，会影响边框颜色
      doing: "我还很小"  # 正在做的事，会影响填充颜色

"2000-09-01":
    - headline: "🏫 开始上中学"
      description: "进入xx中学读书，认识了很多好朋友。"
      based: "北京"
      doing: "学生"
      association: "xx中学"  # 可选，关联的组织或机构
```

每个事件格式说明：
- `headline`: 事件标题，会显示在点击方框后
- `description`: 事件详细描述
- `based`: 当时的居住地，对应colors.yml中的边框颜色定义
- `doing`: 当时的身份/活动，对应colors.yml中的填充颜色定义
- `association`: 可选，关联的组织、学校或公司
- `url`: 可选，可以添加相关链接

### 颜色定义自定义 (data/colors.yml)

`data/colors.yml` 用于定义不同生活地点和活动的颜色：

```yaml
# 这个列表为生命周历网格定义颜色。
# 方框的边框颜色代表我生活的地点，
# 背景色代表那一周我在做什么。
# based和doing值应该与events.yml中的匹配。
# 将based和doing的class_name转换为小写并用连字符替换空格
# 例如，New York City变成new-york-city

# 居住地点的边框颜色
- class_name: "北京"  # 对应events.yml中的based值
  element: "border"
  color_name: "#8eb2d6"  # 十六进制颜色代码

# 活动/身份的填充颜色
- class_name: "学生"  # 对应events.yml中的doing值
  element: "background-color"
  color_name: "#E8F9FF"
```

### 页面样式自定义 (assets/sass/main.scss)

修改 `assets/sass/main.scss` 可以自定义网站的视觉风格：

```scss
:root {
    --main-bg-color: #fff7e9;  // 主背景色
    --text-color: #3f5c72;     // 文字颜色
    --header-text-color: var(--text-color);  // 标题文字颜色
    --link-color: var(--text-color);         // 链接颜色
    --highlight-color: #f05d2b;              // 强调色
    --future-border: #dee2e6;                // 未来方框边框
    --future-bg-color: #eee;                 // 未来方框背景
    // 字体大小设置
    --body-font-size-desktop: 16px;
    --body-font-size-mobile: 12px;
    --header-font-size-desktop: 72px;
    --header-font-size-mobile: 36px;
}
```

### 模板自定义 (layouts/)

如果你熟悉HTML和Hugo模板，可以修改以下文件来调整网站结构和行为：

- `layouts/_default/index.html`: 主页模板
- `layouts/partials/life-in-weeks.html`: 生成周历网格的核心模板
- `layouts/partials/header/navbar.html`: 导航栏模板
- `layouts/partials/helpers/`: 包含多个辅助模板用于生成网格元素

## 技术说明

本页面使用 [Bootstrap](https://getbootstrap.com/) 处理布局和交互，并使用少量 [jQuery](https://jquery.com/) 在地图上反映当前周。

字体是 [Red Hat Display](https://fonts.google.com/specimen/Red+Hat+Display)。颜色选自 [Color Hunt](https://colorhunt.co/)。使用 [Zed](https://zed.dev) 编辑。

## 更多人生周历工具

这里有几个不错的人生周历示例和工具：

- [Weeksofyour.life](https://www.weeksofyour.life/): 完全基于浏览器创建你自己的周历
- [Life Calendar](https://lifecalendar.io): 创建带有多层的自定义周历
- [My Life in Days](https://days.sonnet.io/): 精美的重构版，以天为单位

🍯 "我总是通过离开过去的地方到达我要去的地方。" – 小熊