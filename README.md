# ai-journey

AI 应用开发 24 周学习计划的代码仓库（贸易/供应链方向）。

- 计划全文：[docs/学习计划.md](docs/学习计划.md)
- 进度看板：[docs/进度看板.md](docs/进度看板.md)
- 环境安装：[docs/环境安装.md](docs/环境安装.md)
- Git 入门：[docs/Git入门.md](docs/Git入门.md)
- 每日日志：[docs/日志/](docs/日志/)

## 环境

| 项 | 版本 | 说明 |
|---|---|---|
| Git | 2.56.0.windows.4 | `D:\study\Git` |
| Python | 3.15.2 | 官方 install manager 安装，解释器 `%LOCALAPPDATA%\Python\pythoncore-3.15-64\python.exe` |
| uv | 待装 | 第 4 周前补 |
| VS Code | 1.145.2 | `D:\study\Microsoft VS Code`，已装 Python 扩展 |

## 第一个程序

```bash
python hello.py
```

输出：

```
Hello, ai-journey!
Python 版本： 3.15.2
运行成功 = 环境装好了。
```

## 第一次调用大模型（第 0 周交付）

`api_test.py` 用 Python 通过 HTTP 调用 DeepSeek API：

```python
resp = client.chat.completions.create(
    model="deepseek-flash",
    messages=[{"role": "user", "content": "用一句话解释贸易里的 FOB 价格"}],
)
print(resp.choices[0].message.content)
```

实际返回（2026-11-10）：

> FOB价格（船上交货价）是指卖方负责将货物运至装运港并装上买方指定船舶、承担装船前费用和风险，货物装船后费用和风险转由买方承担，且不含海运费和保险费的成交价格。

运行方式：

```bash
python -m pip install openai python-dotenv
python api_test.py
```

密钥放在 `.env`（已被 `.gitignore` 忽略，永不入库），代码通过 `os.environ` 读取。

## 目录约定

```
ai-journey/
├── hello.py            # 第 0 周：第一段代码
├── api_test.py         # 第 0 周：第一次调用大模型
├── weeks/              # 每周练习，week01/ week02/ ...
├── projects/           # 三个正式项目
└── docs/               # 计划、进度、日志
```
