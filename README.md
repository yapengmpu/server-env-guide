# Docker 環境使用說明

每位學生在服務器上都會有一個Docker container環境（下稱環境），每個環境像是一台linux系統一樣，每個環境之間是互相獨立的，都有獨立的port口、儲存空間、帳戶和密碼，因此，學生無法存取到其他人的環境。

## 與服務器建立連線

首先要建立服務器與學生主機之間的連接。因為主機所在內聯網並不能直接連線，所以需要用到Zerotier虛擬內網進行連線。

1. 下載 Zerotier (<https://www.zerotier.com/download/>) 並安裝。
2. 開啟 Zerotier，在 Windows 工具欄右方找到 Zerotier，右鍵，"Join New Network"。
3. 輸入提供的 Zerotier 網絡。
4. **在 Windows 工具欄右方找到 Zerotier，右鍵，回報 "My address" 給 Max**。

與服務器建立連線後，Max 會提供服務器的IP，現在即可連接到自己的環境。

## 連接到 Docker 環境

環境可以使用SSH連接，像連線到Linux系統一樣。每個環境都有獨立的SSH port。連線資料如下：

- IP and port: "服務器的IP":"環境的SSH port"
- username: root
- password: 你的學生證號碼

其中，服務器的IP和環境的SSH port由 Max 提供，你的學生證號碼是環境的初始密碼，**請第一次連接到環境後立即更改密碼**。

## 更改SSH 密碼

通過 SSH 連接到環境後，可以使用 `env-change-ssh-passwd` 更改SSH密碼。新密碼將在重啟環境後生效。

## 重啟環境

通過 SSH 連接到環境後，可以使用 `env-restart` 重啟環境。

## 資料儲存

環境內有兩個資料夾提供資料儲存，這兩個資料夾內的資料不會因重啟環境而消失，而在其他資料夾的資料將在重啟後消失。

### `/datasets`

`/datasets`資料夾掛載到服務器的SSD上以提供高速資料讀取。然而SSD空間有限，請只把數據集等需要高速讀取等資料放在這裡，避免將實驗數據等放在這裡。

### `/workspace`

`/workspace`資料夾掛載到服務器的HDD上提供大量儲存空間，請將實驗數據等放在這裡。

## 環境配置

- Ubuntu 20.04
- CUDA 12.0
- Pytorch 11.3
- Other python libraries: pytorch_lightning, torchmetrics, tensorboard
- Jupyter
- Code-server

## 環境變更

學生可以在環境內自行安裝任何東西，但其將會在重設環境後消失。

## 重設環境

如果環境壞掉了，Max可以幫忙重設環境，但先前自行安裝的東西都會消失。

## Jupyter 與 code-server

環境有內建Jupyter 與 code-server (網頁版VS Code)，學生可以在瀏覽器進入 Jupyter 或 code-server 來使用環境。連線方式如下：

- Jupyter 在瀏覽器輸入 "服務器的IP":"Jupyter的SSH port"
- code-server 在瀏覽器輸入 "服務器的IP":"code-server的SSH port"

每個環境都有不同的"Jupyter的SSH port"和"code-server的SSH port"，請向Max查詢。

Jupyter 和 code-server 都受密碼保護，在第一次使用前，請在SSH中使用`env-change-jupyter-passwd`和`env-change-code-server-passwd` 指令更改密碼，新密碼將在重啟環境後生效。

## 其它

### 環境指令

- `env-restart`: 重啟環境
- `env-change-ssh-passwd`: 更改SSH密碼
- `env-change-jupyter-passwd`: 更改Jupyter密碼
- `env-change-code-server-passwd`: 更改 Code-server密碼
