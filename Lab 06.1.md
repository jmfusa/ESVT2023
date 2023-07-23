### **Ubuntu VM - Python虛擬環境介紹與應用** - 學習筆記

Python 虛擬環境可以讓使用者在同一台機器上獨立地安裝和管理不同版本的 Python 和相應的套件，這對於開發和測試不同的 Python 項目非常有用。

**Step 1：安裝所需套件**
在開始安裝之前，先確保系統已經安裝了一些必要的套件。打開終端機（Terminal）並執行以下指令：

```
sudo apt update
sudo apt install -y curl git make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev
```

**Step 2：安裝 Pyenv**
接下來，安裝 Pyenv，這是一個用於管理 Python 版本的工具。在終端機中執行以下指令來安裝 Pyenv：

```
curl https://pyenv.run | bash
```

這將下載並執行 Pyenv 的安裝範本。安裝完成後，重新啟動終端機會話或執行以下指令讓 Pyenv 立即生效：

```
exec $SHELL
```

**Step 3：設定環境變數**
安裝完 Pyenv 後，設定相應的環境變數。在終端機中執行以下指令：

```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
```

**注意**，如果使用的是其他 shell，例如 Zsh，則需要修改相應的設定文件（例如 `~/.zshrc`）。

**Step 4：重新載入環境變數**
設定完環境變數後，重新載入 shell 環境，使更改生效：

```
exec $SHELL
```

**Step 5：安裝 Python 版本**
已經準備好使用 Pyenv 安裝不同版本的 Python。例如，要安裝 Python 3.9.6，在終端機中執行以下指令：

```
pyenv install 3.9.6
```

安裝完成後，使用以下指令來查看已安裝的 Python 版本：

```
pyenv versions
```

**Step 6：建立虛擬環境**
使用 Pyenv 安裝不同版本的 Python 後，使用這些版本來建立虛擬環境。假設要在專案中使用 Python 3.9.6，請執行以下指令建立虛擬環境：

```
pyenv virtualenv 3.9.6 my_project_env
```

這將在 `~/.pyenv/versions/3.9.6/envs/` 目錄下建立一個名為 `my_project_env` 的虛擬環境。

**Step 7：啟用虛擬環境**
啟用虛擬環境後，專案將使用指定版本的 Python 和相應的套件。執行以下指令來啟用虛擬環境：

```
pyenv activate my_project_env
```

啟用虛擬環境後，終端機提示會顯示虛擬環境名稱，表示虛擬環境已經啟用。

**Step 8：安裝套件**
現在，可以在虛擬環境中安裝需要的 Python 套件，例如使用 `pip`：

```
pip install package_name
```

**Step 9：退出虛擬環境**
完成了專案的工作，可以使用指令退出虛擬環境：

```
pyenv deactivate
```
