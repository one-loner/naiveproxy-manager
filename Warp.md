# 🌐 Интеграция с Cloudflare WARP (Опционально)

Нужно, если хотите скрыть IP сервера или разблокировать региональный контент.

**1. Установить зависимости:**
```shell
apt install -y curl gnupg lsb-release
```

**2. Установка WARP клиента:**
```shell
curl -fsSL https://pkg.cloudflareclient.com/pubkey.gpg | gpg --yes --dearmor --output /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://pkg.cloudflareclient.com/ $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/cloudflare-client.list
apt update && apt install cloudflare-warp -y
```

**3. Настройка режима прокси:**
```shell
warp-cli registration new
warp-cli mode proxy
warp-cli connect
```

**4. Проброс трафика в Caddy:**
Добавьте строку `upstream socks5://127.0.0.1:40000` в ваш `Caddyfile` внутрь блока `forward_proxy` и выполните `systemctl restart caddy`.

---
