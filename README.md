# 辽宁大学图书馆座位预约助手

一个面向辽宁大学图书馆预约流程的 Python 自动化项目。项目通过 Selenium 操作网页、检查自习室与座位可约状态，并按配置执行预约；同时使用 OCR 组件处理页面中的图像验证码场景。它也是我将浏览器自动化、模板化配置和计算机视觉结合起来的一次实践。

> 本项目仅供个人学习与技术作品展示。请先确认学校图书馆系统的使用规则，并仅在获得授权的范围内测试。自动化操作和验证码识别可能不被目标系统允许；请勿用于规避访问控制或影响他人正常使用。

## 项目亮点

- **配置驱动生成脚本**：通过 `configs/config.json` 保存校区、预约时段、偏好自习室和座位等参数，由 Jinja2 模板生成运行脚本。
- **多时段与偏好选择**：提供两套脚本模板，可配置不同账号及时段；优先检查偏好座位，并在不可用时按脚本逻辑查找其他可用位置。
- **网页自动化与状态检查**：使用 Selenium 完成页面交互、可约状态判断、预约结果检查和失败重试。
- **OCR 组件实践**：结合 `ddddocr` 与本地 PaddleOCR 推理模型，处理项目涉及的图像识别流程。
- **自动化工作流示例**：仓库包含 GitHub Actions 工作流，用于定时运行及日志通知；运行前需要正确配置环境和 Actions Secrets。

## 技术栈

Python、Selenium、Jinja2、Pillow、NumPy、ddddocr、PaddleOCR、PaddlePaddle、GitHub Actions。

## 项目结构

```text
├── configs/
│   └── config.json                 # 本地运行配置示例
├── templates/
│   ├── script_template1.py.j2      # 脚本模板一
│   └── script_template2.py.j2      # 脚本模板二
├── ocr_model/                      # OCR 推理模型与字符表
├── .github/workflows/              # 自动生成与定时运行工作流
├── generate_script.py              # 从配置渲染脚本
├── script1.py                      # 生成的运行脚本一
├── script2.py                      # 生成的运行脚本二
└── requirements.txt                # Python 依赖
```

## 配置与运行

建议使用与项目依赖兼容的 Python 环境，并确保本机浏览器及 WebDriver 配置正确。

1. 克隆仓库并进入项目目录。
2. 安装依赖：

   ```bash
   pip install -r requirements.txt
   ```

3. 在本机编辑 `configs/config.json`，填写自己的校区、预约时段及座位偏好。
4. 生成脚本：

   ```bash
   python generate_script.py
   ```

5. 在确认符合图书馆规则并完成必要配置后，按需运行 `script1.py` 或 `script2.py`。

项目依赖浏览器页面结构和图书馆系统规则，页面更新、网络状态、系统开放时间及依赖版本都可能影响运行结果。首次运行前请在非关键时段检查配置和行为。

## 配置与凭据安全

`configs/config.json` 仅用于本地配置示例。请勿将真实的校园账号、密码、令牌或邮箱凭据提交到公开仓库。若使用 GitHub Actions，请把通知邮箱凭据放在仓库 Secrets 中；不要在公开工作流或配置文件中写入任何真实凭据。启用自动运行前，也应确认工作流的行为符合学校政策。

## 免责声明

本项目用于展示个人的自动化脚本、数据处理及 OCR 集成实践，不代表辽宁大学图书馆官方工具，也不保证对当前系统持续有效。使用者应自行确认授权、遵守相关规定，并对运行行为及后果负责。
