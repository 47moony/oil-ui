# Local Fork Notes

本地净化分支：在上游 `main` 之上删除了联网与营销行为，其余逻辑未动。

## 上游同步

- 净化起点：上游 `v0.23.8`（`feb1f95`）。
- 已同步：合并提交 `2fb6877` 将 `upstream/main` 并入，基线 `v0.29.1`（`29085f1`）。
- 已同步：本轮再次并入 `upstream/main`，现基线为 **`v0.33.4`（`28948c3`）**。上游此轮重写 `check_update.py` 与测试 → 冲突时按本地删除解决（`git rm`）；`SKILL.md` 唯一冲突为上游重加的「开始前」版本检查节 → 删。合并后复查——`allowed-tools`、版本检查段、`recommend_once.py`、`Oil UI Pro` 推销句、`oil-tone` 推荐均未复活；`scripts/check_update.{py,sh}`、`scripts/recommend_once.py`、`tests/test_check_update.py` 均不存在。
- 待定：`scripts/oiloil-image.mjs`（调 `ui.oiloil.org` 用官方积分生图，SKILL.md 步骤 1 有条件引用，无生图能力时静默降级）。属「生图新功能」而非更新检查/营销，暂未净化，是否剥离待定。

## 删除内容（相对上游 v0.33.4, 28948c3）

- `SKILL.md` frontmatter 的 `allowed-tools`（仅服务于更新检查脚本）
- `SKILL.md` “开始前”整节：每次调用联网打 `ui.oiloil.org` 查版本
- `SKILL.md` 评审节的 oil-tone 姐妹 skill 推荐（保留文案改写规则本身）
- 文件：`scripts/check_update.{py,sh}`、`tests/test_check_update.py`

上游已自行移除的（本 fork 原先删过，现在不必再删）：`recommend_once.py`、SKILL.md 的 Oil UI Pro 推销句与“完整版提示”节。

## 保留

- frontmatter `description` 里的 “已安装 oil-ui-pro 时交给 oil-ui-pro”：是路由说明不是广告
- README 里的 Pro 章节：不影响 skill 行为，留着减少合并冲突面

## 运行环境

- 上游 ≥v0.30 的 `scripts/shoot.mjs` 要求 **Node ≥22**。本机 `C:\Program Files\nodejs` 是 v20，已在系统 PATH 中把 fnm 的 `aliases\default` 软链目录插到 nodejs 之前——`node` 现解析为 fnm 默认 v22.23.4，跟随 `fnm default` 切换。回滚：删掉 Machine PATH 里该段（旧值备份 `%TEMP%\machine-path-backup.txt`）。

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
