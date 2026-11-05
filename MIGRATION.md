# 启动页 适配清单

目标：把 `views/` 里的页面改成只依赖 `PCL.Modular.Abstractions` 的契约，不再直接摸全局状态。

## 全局符号依赖（按文件）

| 文件 | 行数 | 仍在直接引用的全局符号 |
| --- | --- | --- |
| `MyMsgLogin.xaml.vb` | 160 | `FrmMain`×6、`MyMsgBox`×2、`ModLaunch`×1、`Hint`×1、`RunInUi`×1 |
| `MySkin.xaml.vb` | 313 | `Hint`×16、`Settings`×3 |
| `PageLaunchLeft.xaml.vb` | 837 | `Settings`×33、`RunInUi`×15、`FrmMain`×11、`Hint`×2、`ThemeUnlock`×1 |
| `PageLaunchRight.xaml.vb` | 293 | `Settings`×12、`FrmMain`×2、`Hint`×2、`MyMsgBox`×1、`RunInUi`×1 |
| `PageLoginAuth.xaml.vb` | 86 | `Settings`×21 |
| `PageLoginAuthSkin.xaml.vb` | 85 | `Settings`×14、`Hint`×3、`RunInUi`×1 |
| `PageLoginLegacy.xaml.vb` | 77 | `Settings`×10、`FrmMain`×1、`Hint`×1、`RunInUi`×1 |
| `PageLoginMs.xaml.vb` | 108 | `Settings`×4、`RunInUi`×3、`Hint`×1 |
| `PageLoginMsSkin.xaml.vb` | 180 | `Settings`×16、`Hint`×10 |
| `PageLoginNide.xaml.vb` | 80 | `Settings`×16 |
| `PageLoginNideSkin.xaml.vb` | 57 | `Settings`×10 |

## 适配步骤

1. **换数据来源**：把 `ModMain` / `States` 的读取改成 `IModuleContext.Services` 里对应的服务调用。
2. **换宿主窗口引用**：`FrmMain.PanXXX` 这类直接操作宿主控件的代码，改成通过 `IHostShell` 暴露的插槽。
3. **换提示**：`Hint` / `MyMsgBox` 改成 `INotificationService`。
4. **换主题**：`ThemeUnlock` 等主题开关改成 `IThemeService`。
5. 每换完一个文件，就在下表中把该行删掉；表空了才算这个模块真正独立。

> 说明：这一步是**迁移进度的账本**，不是待办愿望单。没做完的行必须留着。
