# 飞书渠道伙伴内容推送 Skill — 配置模板

> **用途：** 首次初始化时，Agent 将读取此模板引导用户完成配置。配置完成后存储在飞书知识库中。

---

## 一、知识库空间配置

```yaml
# 知识库空间
space_name: "飞书渠道伙伴知识库"
space_description: "渠道销售内容归档：行业资讯、产品更新、培训资料、推送记录"

# 分类目录节点
directories:
  industry_news:
    title: "📰 行业资讯"
    node_token: "<初始化后填入>"
  feishu_updates:
    title: "🚀 飞书新功能"
    node_token: "<初始化后填入>"
  training_materials:
    title: "📚 培训资料"
    node_token: "<初始化后填入>"
  push_history:
    title: "📤 推送记录"
    node_token: "<初始化后填入>"
```

---

## 二、伙伴分组配置

```yaml
partner_groups:
  全体伙伴:
    description: "所有签约合作的渠道代理商"
    chat_name: "飞书渠道-全体伙伴"
    chat_id: "<初始化后填入>"
    push_scope: ["行业资讯", "飞书新功能-通用", "培训-FAQ", "紧急通知"]

  核心伙伴:
    description: "主力开单、高产出伙伴"
    chat_name: "飞书渠道-核心伙伴"
    chat_id: "<初始化后填入>"
    push_scope: ["行业资讯", "飞书新功能-全部", "培训-全部", "紧急通知"]

  新签约伙伴:
    description: "入职/合作30天内的新伙伴"
    chat_name: "飞书渠道-新签约伙伴"
    chat_id: "<初始化后填入>"
    push_scope: ["行业资讯-精简", "飞书新功能-通用", "培训-基础入门", "培训-FAQ"]

  低效伙伴:
    description: "前期业绩分级中「高危/预警」的伙伴"
    chat_name: "飞书渠道-低效伙伴"
    chat_id: "<初始化后填入>"
    push_scope: ["行业资讯-精简", "飞书新功能-通用", "培训-销售话术", "培训-基础入门", "培训-FAQ"]
```

---

## 三、内容标签体系

```yaml
content_tags:
  行业资讯:
    icon: "📰"
    sub_tags: ["行业动态", "竞品动态", "政策解读", "市场热点"]
    default_push_group: "全体伙伴"

  飞书新功能:
    icon: "🚀"
    sub_tags: ["新版本", "AI能力", "定价调整", "功能优化", "使用技巧"]
    default_push_group: "全体伙伴"
    advanced_sub_tags: ["AI能力-高级", "定价调整"]  # 仅推核心伙伴

  培训资料:
    icon: "📚"
    sub_tags: ["销售话术", "客户方案", "行业案例", "陪访总结", "FAQ"]
    default_push_group: "视子类决定"
```

---

## 四、推送时段配置

```yaml
push_schedule:
  # ⭐ v2.0 新增：自动采集调度
  auto_collect:
    time: "09:30"  # 每日自动采集时间
    timezone: "Asia/Shanghai"
    weekdays: [1, 2, 3, 4, 5]  # 仅工作日
    sources:
      saas_news:
        - search_rounds: 3
        - time_filter: "48h"  # 仅48小时内新闻
        - target_count: "3-5条"
      feishu_updates:
        - search_rounds: 2
        - time_filter: "7d"  # 7天内更新
        - target_count: "1-3条"
    preview_before_archive: true  # 归档前必须人工确认

  daily_regular:
    time: "16:00"  # 每日固定推送时间
    timezone: "Asia/Shanghai"
    auto_generate: true
    preview_before_send: true  # 发送前预览确认

  weekly_review:
    day: "Friday"
    time: "17:00"
    auto_generate: true  # 是否自动生成周报复盘

  urgent:
    immediate: true  # 紧急推送即时发送
    default_groups: ["全体伙伴", "核心伙伴"]
```

---

## 五、Scope 权限清单

初始化时需要确保以下飞书应用权限已开通：

| Scope | 用途 | 身份 |
|-------|------|------|
| `wiki:wiki_space:write` | 创建/管理知识库空间 | user / bot |
| `wiki:wiki_node:write` | 创建/管理知识库节点 | user / bot |
| `wiki:wiki_node:readonly` | 读取知识库节点 | user / bot |
| `im:message:create_as_bot` | 以 bot 身份发送消息 | bot |
| `im:message:send_as_user` | 以用户身份发送消息 | user |
| `im:chat:write` | 创建群聊 | user |
| `docs:doc:readonly` | 搜索文档和知识库 | user / bot |
| `contact:user:readonly` | 读取用户信息 | user |

---

## 六、初始化流程

```
Step 1: 确认 lark-cli 已安装 → lark-cli --version
Step 2: 确认已授权 → lark-cli auth login --domain feishu
Step 3: 运行初始化 → AI Agent 对话中输入「帮我初始化飞书渠道伙伴内容推送技能」
Step 4: Agent 自动完成：创建空间 → 创建目录 → 创建群聊 → 保存配置
Step 5: 验证 → 录入一条测试数据，确认全流程可用
```
