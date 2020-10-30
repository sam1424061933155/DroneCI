# DroneCI

結合github和DroneCI，當有git commit並push的時候會觸發Drone CI

![droneCI](/img/droneciResult.png)

## 操作

1. 後續docker-compose 設定 DRONE_SERVER_HOST 必須使用public ip，可以透過 ngrok 讓 Port 開放 IP 讓外界存取

- 開放 port 的方法

ngrok http 8081，就會把剛剛架設的 drone 伺服器 localhost 的 8081 端口綁定到特定的 ngrok 網址

2. 透過 github settings/developer settings/OAuth application 綁定droneCI

- Authorization callback URL
使用drone 1.x, URL 是 {ngrok ip}/login

3. 設定 doccker-compose 並執行

- 需修改 DRONE_SERVER_HOST, DRONE_GITHUB_CLIENT_ID, DRONE_GITHUB_CLIENT_SECRET
- DRONE_SERVER_HOST: ngrok ip
- DRONE_GITHUB_CLIENT_ID: github 綁定 application 後產生
- DRONE_GITHUB_CLIENT_SECRET: github 綁定 application 後產生

4. 確認 .drone.yml 在資料夾 root，定義觸發 drone 後要做甚麼

- 設定branch，似乎預設是處理 master 下的 push 事件，如果 project 不是在 master 下要自己設定

5. 如果 push 後 drone 還是沒有反應，可以確認 DroneCI/Settings/Webhooks, 確認這個 post有成功