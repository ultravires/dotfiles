# dotfiles

个人配置文件仓库，使用 [GNU Stow](https://www.gnu.org/software/stow/) 管理，通过符号链接将配置部署到家目录。

## 依赖

```bash
brew install stow
brew install --cask font-maple-mono-nf-cn   # Ghostty 使用的字体
```

## 仓库结构

每个工具对应一个 stow 包，包内目录结构与其在 `~` 下的真实路径一致：

```text
.
├── ghostty/                   # Ghostty 终端
│   └── .config/
│       └── ghostty/
│           └── config         # ~/.config/ghostty/config
└── starship/                  # starship 提示符
    └── .config/
        └── starship.toml      # ~/.config/starship.toml
```

部署后，`~/.config/starship.toml` 是指向仓库内真实文件的符号链接，程序读取时透明无感知。

## 新机器初始化

```bash
git clone https://github.com/ultravires/dotfiles.git ~/dotfiles
cd ~/dotfiles
stow starship ghostty
```

> 仓库固定克隆到 `~/dotfiles`。stow 的默认目标目录是仓库的上级目录（即 `~`），因此无需额外指定 `--target`。

## 日常操作

| 操作 | 命令 |
| --- | --- |
| 部署某个包 | `stow <包名>` |
| 撤销某个包 | `stow -D <包名>` |
| 移动仓库后重新部署 | `stow -R <包名>` |
| 部署所有包 | `stow */` |

## 新增配置

以 `git` 为例：

```bash
mkdir -p git/.config/git
mv ~/.config/git/config git/.config/git/config
stow git
```

将真实文件移入仓库后，stow 会在原位置创建符号链接。
