---
name: api-keys-env-local
description: "用户把个人 API key 放在 C:\\Users\\y3264\\.env.local;需要 key 时从这里读,别让他在聊天里贴明文"
metadata: 
  node_type: memory
  type: reference
  originSessionId: e0fbf26e-ac66-4e20-85ed-282b408c5bf7
---

用户把个人 API key 集中存在 `C:\Users\y3264\.env.local`(每行 `KEY=VALUE`)。已确认存在的变量:`OPENAI_API_KEY`(有效 OpenAI key)、`ZEP_API_KEY`(Zep Cloud)。

**How to apply:** 任何任务需要 API key 时,优先指向 / 读取这个文件,而不是让用户把密钥贴进聊天。用脚本从文件解析出值、直接注入目标配置文件,**绝不打印 value**(见 [[feedback_api_key_security]])。本会话中用户正是用"发文件路径"的方式提供了 OpenAI 和 Zep 两个 key。
