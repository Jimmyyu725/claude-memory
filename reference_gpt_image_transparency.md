---
name: reference-gpt-image-transparency
description: OpenAI 图像模型透明背景支持情况(做游戏精灵图/贴图时用)
metadata: 
  node_type: memory
  type: reference
  originSessionId: 0ab2c3ea-406c-4595-90d5-bcba3f13f30e
---

OpenAI 图像生成 API 里,**`gpt-image-2` 系列不支持透明背景**(请求 `background: "transparent"` 会报 400 `invalid_value`)。**`gpt-image-1` 和 `gpt-image-1.5` 支持透明**。

做需要透明 PNG 的素材(游戏精灵图、图标、抠图)时用 `gpt-image-1.5`(更新);只需要不透明大图(背景、天空)时 `gpt-image-2` 也行。

调用要点:`output_format: "png"`,`background: "transparent"`,size 支持 1024x1024 / 1024x1536 / 1536x1024。返回 `data[0].b64_json`,解码写文件即可。key 见 [[feedback-api-key-security]](只测存在、绝不打印)。

用于 [[project-doomfollow-game]] 的美术生成。
