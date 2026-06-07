---
name: mirofish
description: "MiroFish 多智能体\"预测引擎\",克隆在 C:\\Project\\MiroFish,配 OpenAI gpt-4o-mini + Zep,前后端已跑通"
metadata: 
  node_type: memory
  type: project
  originSessionId: e0fbf26e-ac66-4e20-85ed-282b408c5bf7
---

MiroFish(多智能体群体模拟"预测引擎",https://github.com/666ghj/MiroFish)克隆在 `C:\Project\MiroFish`。Python(Flask)后端 + Vue/Vite 前端,底层是 CAMEL-AI 的 OASIS 社交模拟(类 Twitter/Reddit 发帖点赞转发)。

**配置:** 走 OpenAI(不是官方默认的阿里百炼)。`.env` 里 `LLM_BASE_URL=https://api.openai.com/v1`、`LLM_MODEL_NAME=gpt-4o-mini`(省钱默认),key 来自 [[api-keys-env-local]]。后端 `Config.validate()` 强制要 `LLM_API_KEY` + `ZEP_API_KEY`,缺一启动即退出。

**启动:** 后端 `uv run --directory C:\Project\MiroFish\backend python run.py`(:5001);前端 `npm --prefix C:\Project\MiroFish\frontend run dev`(:3000)。要求 Python 3.11–3.12,uv 已装托管 3.12.13(系统 Python 是 3.14,不兼容,靠 uv 隔离)。日志在仓库根的 `_run_backend.log` / `_run_frontend.log`。

**成本 & 省钱跑法:** 跑真实推演会按 agent 数 × 轮数 × 双平台狂调 LLM,README 警告"消耗较大"。Step2 末尾 UI 显示的"自动"轮数由 LLM 配置算出、可能很高(实测一个舆情 demo 给到 **168 轮**;后端 env 默认 `OASIS_DEFAULT_MAX_ROUNDS=10` 只是后备)。**首次/省钱:在"模拟轮数设定"打开"自定义"开关,把滑块拖到最小 10 轮**;agent 数由种子材料里的实体数决定,种子越短越省。换更强模型(gpt-4o/4.1/5 都可用)前提醒成本。

**状态:** 完整流程(上传种子 → 建图谱 → 生成 agent → 双平台模拟 → 预测报告 → 可与 agent 对话)已于 2026-06-02 用"星澜科技 AI 客服舆情"虚构案例验证跑通(10 轮 + gpt-4o-mini,~6 个 agent,产出连贯的舆情预测报告)。种子材料样例在 `C:\Users\y3264\Desktop\星澜科技舆情_种子材料.txt`。
