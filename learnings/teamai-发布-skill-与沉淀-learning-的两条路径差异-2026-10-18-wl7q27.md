---
title: "TeamAI 发布 skill 与沉淀 learning 的两条路径差异"
author: GelatoMao
date: 2026-10-17
tags: [teamai, workflow, best-practice]
---

## Context
从零搭建团队 TeamAI 后,分别验证了发布 skill(`teamai push`)和沉淀 learning(`teamai contribute`)两条分发路径。两者看起来都是"分享给团队",行为却不同,容易误判"为什么没生效"或"怎么合并"。

## Solution
- 发布 skill:`teamai push --skill <path>` 会推到新分支 `teamai/push/<用户>/<时间戳>` 并自动创建 PR,PR 合并进 `main` 后队友才能拉到。先用 `teamai --dry-run push` 预览,没指定 `--role` 或 `--project` 时资源放根目录,全员可见。
- 沉淀 learning:`teamai contribute --file <md> --title <标题>` 直接提交到独立分支 `teamai-learnings` 的 `learnings/` 下,没有 PR、不需要合并。
- `teamai-learnings` 与 `main` 是完全无关的提交历史,在 GitHub 上对比会显示 "There isn't anything to compare",也无法开 PR,这是设计如此。
- 队友执行 `teamai pull` 时,最后一步会刷新本地 `learnings-wt` 并重建搜索索引,所以能收到 learning。
- 自动沉淀依赖 recall:团队默认关闭,`teamai recall enable` 只影响本机,团队级需在 `teamai.yaml` 设 `sharing.recall.enabled: true` 后 push。

## Lessons
- skill 走 PR 要人工合并,learning 直接写入,卡控主要靠仓库写权限。
- 不要强行把 `teamai-learnings` 合进 `main`,会混入无关历史并破坏读取方式。
- 发布前先 `--dry-run` 看清楚范围,避免误发给全员。
- 经验文档里不要写密钥或敏感信息,所有有读权限的人都能看到。

## Related Skills
- teamai
