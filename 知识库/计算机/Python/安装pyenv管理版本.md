---
tags:
  - Python
  - Python版本管理
  - pyenv
---
# 1、安装

```bash
brew install pyenv
```

# 2、配置 Shell 环境

对于 zsh 用户(添加到 ~/.zshrc)
```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc

export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
```

# 3、使配置生效

```bash
source ~/.zshrc # 如果使用 zsh
source ~/.bash_profile # 如果使用 bash
```

# 4、常用命令

```bash
# 查看所有可用的 Python 版本
pyenv install --list

# 安装指定版本的 Python
pyenv install 3.12.0
pyenv install 3.9.18

# 查看已安装的版本
pyenv versions

# 设置全局默认版本
pyenv global 3.12.0

# 为特定项目设置本地版本
cd your_project
pyenv local 3.9.18
```

