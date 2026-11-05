# PCL.UI.Launch

PCL 模块化拆分 · **启动页** UI 模块。

| 项 | 值 |
| --- | --- |
| 模块 Id | `pcl.ui.launch` |
| 依赖 | `pcl.core`, `pcl.theme`, `pcl.launch.microsoft`, `pcl.ui.controls` |
| 源码来源 | `Meloong-Git/PCL` → `Plain Craft Launcher 2/Pages/PageLaunch` |
| 迁移文件 | 22 个文件 / 2721 行 |
| 状态 | **阶段 1：源码已归位，适配未完成** |

## 现在能用什么

- `views/` 里是与上游**逐字一致**的原始 XAML 与代码，可以直接对照阅读。
- `module.json` 是加载器认的清单，依赖关系已经写死，顺序不会靠猜。
- `MIGRATION.md` 列出了这些页面当前仍在直接读哪些全局状态（`States` / `ModMain` / `FrmMain` …），
  这些就是适配层要替换掉的东西。

## 为什么还不能直接编译

上游 UI 是单程序集里的"全局状态 + 页面"结构：页面直接读 `ModMain`、`States`、`FrmMain.PanXXX`。
要让它变成独立模块，必须先把这些读取换成契约调用（见 MIGRATION.md 的对照表）。
**在契约没补齐之前，硬凑一个能编译的空壳只会假装成功**，所以这里不提供编译产物。

## 依赖的契约（待补）

- `Settings` × 139
- `Hint` × 36
- `RunInUi` × 22
- `FrmMain` × 20
- `MyMsgBox` × 3
- `ModLaunch` × 1
- `ThemeUnlock` × 1
