# small-wolf-hair-configuration

个人双平台 [Rime](https://rime.im/) 输入法配置，基于 [雾凇拼音（rime_ice）](https://github.com/iDvel/rime-ice) 方案体系，同时在 **macOS（鼠须管 Squirrel）** 与 **Windows（小狼毫 Weasel）** 上维护统一的输入习惯。

> 仓库名 "small-wolf-hair" 即 Rime Windows 前端「小狼毫」（Weasel）的直译。

## 目录结构

```
.
├── MacOS/                  # 鼠须管（Squirrel）配置
│   ├── default.yaml        # Rime 全局设置
│   └── squirrel.yaml       # macOS 前端外观配置
├── Windows/                # 小狼毫（Weasel）配置
│   ├── default.yaml        # Rime 全局设置（Windows 版）
│   ├── default.custom.yaml # 补丁文件，覆盖 default.yaml 部分配置
│   └── weasel.yaml         # Windows 前端外观配置
└── .gitignore              # 忽略 Windows 系统文件
```

## 方案列表

`default.yaml` 中启用了以下输入方案：

| 方案 | 说明 |
| --- | --- |
| `rime_ice` | 雾凇拼音（全拼） |
| `t9` | 中文九键（依赖 rime_ice） |
| `double_pinyin` | 自然码双拼 |
| `double_pinyin_abc` | 智能 ABC 双拼 |
| `double_pinyin_mspy` | 微软双拼 |
| `double_pinyin_sogou` | 搜狗双拼 |
| `double_pinyin_flypy` | 小鹤双拼 |
| `double_pinyin_ziguang` | 紫光双拼 |
| `double_pinyin_jiajia` | 拼音加加双拼 |

## 跨平台一致性

两个平台共享同一套雾凇拼音体系。这里的核心目标是**把两个平台的按键习惯抹平**——无论 macOS 还是 Windows，都用完全相同的方式操作候选框，而不是各搞一套快捷键。

无论哪个平台，都统一用 Emacs 风格的 `Control + p/n/f/b` 控制候选框：

| 快捷键 | 作用 |
| --- | --- |
| `Control + p` | 候选框向上翻页 |
| `Control + n` | 候选框向下翻页 |
| `Control + b` | 向左选词 |
| `Control + f` | 向右选词 |

两端的底层实现方式不同，但最终手感一致：

- **macOS**：鼠须管原生支持，直接在 `default.yaml` 的 `key_binder` 中把 `Control + p/n/f/b` 映射为翻页与左右选词。
- **Windows**：小狼毫无法直接接收这组快捷键，因此配合 [autohotkey-scripts](https://github.com/ranmin69/autohotkey-scripts)：先由 AutoHotkey 把 `Control + p/n/f/b` 映射为方向键 `上/下/左/右`，再由 `default.custom.yaml` 的 `key_binder` 把方向键映射为翻页与左右选词。

> Windows 平台需同时部署 [autohotkey-scripts](https://github.com/ranmin69/autohotkey-scripts) 才能获得上述统一的导航体验。

## 外观皮肤

候选框的配色、字体、布局等外观不做统一约定，请根据个人喜好自行调整各平台的前端配置文件：

- **macOS**：`squirrel.yaml`
- **Windows**：`weasel.yaml`

## 使用方法

将对应平台目录下的文件复制到 Rime 用户目录，然后重新部署即可。

- **macOS**：`~/Library/Rime/`
- **Windows**：`%APPDATA%\Rime\`

> 修改配置后需重新部署生效。`default.yaml` / `squirrel.yaml` 中的 `config_version` 需大于共享目录同名文件的版本才会生效。

## 致谢

- [Rime 中州韵输入法引擎](https://rime.im/)
- [雾凇拼音 rime-ice](https://github.com/iDvel/rime-ice)
- [鼠须管 Squirrel](https://github.com/rime/squirrel) · [小狼毫 Weasel](https://github.com/rime/weasel)
