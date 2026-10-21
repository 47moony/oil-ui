# Local Fork Notes

本地净化分支：在上游 `main` 之上删除了联网与营销行为，其余逻辑未动。

## 删除内容（相对上游 v0.23.8, feb1f95）

- `SKILL.md` frontmatter 的 `allowed-tools`（仅服务于更新检查脚本）
- `SKILL.md` “开始前”整节：每次调用联网打 `ui.oiloil.org` 查版本
- `SKILL.md` 步骤 2 末尾的 Oil UI Pro 推销句
- `SKILL.md` 评审节的 oil-tone 姐妹 skill 推荐（保留文案改写规则）
- `SKILL.md` “完整版提示”整节（`recommend_once.py` 往回复末尾贴 Pro 广告）
- 文件：`scripts/check_update.{py,sh}`、`scripts/recommend_once.py`、`tests/test_check_update.py`

## 保留

- frontmatter `description` 里的 “已安装 oil-ui-pro 时交给 oil-ui-pro”：是路由说明不是广告
- README 里的 Pro 章节：不影响 skill 行为，留着减少合并冲突面

## Remotes

- `origin` → `47moony/oil-ui`（你的 fork，本地 main 已跟踪并推送）
- `upstream` → `oil-oil/oil-ui`（官方仓库，只用于拉更新）

## 手动更新上游

```powershell
cd C:\Users\Administrator\.cc-switch\skills\oil-ui
git fetch upstream
git log --oneline HEAD..upstream/main    # 看上游新增
git merge upstream/main                  # 冲突只可能落在 SKILL.md 被删段落附近
git push origin main                     # 合并完同步回 fork
```

合并后复查：若上游重写了被删段落，`git diff` 时确认更新检查/广告逻辑没有借尸还魂。
