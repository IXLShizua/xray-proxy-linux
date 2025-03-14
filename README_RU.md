# xray-proxy-linux

## VLESS + REALITY + Linux TPROXY

Этот репозиторий содержит конфигурационные файлы и настройки для **VLESS + REALITY + Linux TPROXY**.

---

## Настройка

Для начала работы откройте этот репозиторий в вашем любимом IDE и укажите свои значения в следующих переменных:

### Необходимые переменные

Переменные отмечены комментариями в конфигурационных файлах:

- **JSON-файлы**: Переменные помечены комментариями `//`.
- **Конфигурация nftables**: Переменные помечены комментариями `#`.

#### Переменные:

- **TPROXY-порт (опционально):**  
  `_DOKODEMO_TPROXY_PORT`

- **Адрес сервера VLESS:**  
  `_VLESS_ADDRESS`

- **Порт VLESS:**  
  `_VLESS_PORT`

- **UUID пользователя VLESS:**  
  `_VLESS_USER_ID`

- **Имя сервера REALITY (SNI):**  
  `_REALITY_SERVER_NAME`

- **Открытый ключ REALITY:**  
  `_REALITY_PUBLIC_KEY`

- **Short ID REALITY:**  
  `_REALITY_SHORT_ID`

---

## Необходимые пакеты

Перед установкой убедитесь, что установлены следующие пакеты:

Для **Ubuntu/Debian**:

```bash
sudo apt update && sudo apt install -y nftables iproute2
```

Для **CentOS/RHEL**:

```bash
sudo yum install -y nftables iproute
```

Для **Arch Linux**:

```bash
sudo pacman -S nftables iproute2
```

Убедитесь, что служба `nftables` включена и запущена:

```bash
sudo systemctl enable --now nftables
```

---

## Установка Xray Core

Скачайте и установите последнюю версию Xray из [репозитория xray-core](https://github.com/XTLS/Xray-core/releases):

```bash
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install
```

Проверьте установленную версию:

```bash
xray --version
```

---

## Руководство по установке

### 1. Клонирование репозитория

```bash
git clone https://github.com/IXLShizua/xray-proxy-linux.git
cd xray-proxy-linux
```

### 2. Настройка конфигурации

Откройте необходимые файлы в текстовом редакторе и внесите требуемые изменения.

### 3. Установка конфигурационных файлов

#### 3.1 Конфигурация Xray

Скопируйте конфигурационный файл Xray в нужную директорию:

```bash
mkdir -p /etc/xray
cp config.json /etc/xray/config.json
```

#### 3.2 Systemd-сервис

Скопируйте systemd-файл сервиса и включите его:

```bash
cp xray-proxy.service /etc/systemd/system/xray-proxy.service
systemctl daemon-reload
systemctl enable xray-proxy
```

#### 3.3 Настройка маршрутизации и брандмауэра

Убедитесь, что конфигурация nftables установлена:

```bash
mkdir -p /etc/nftables
cp proxy.conf /etc/nftables/proxy.conf
```

---

### 4. Запуск сервиса

```bash
systemctl start xray-proxy
```

### 5. Проверка статуса сервиса

```bash
systemctl status xray-proxy
```

---

## Поддержка и участие

Если у вас есть вопросы или предложения по улучшению проекта, откройте issue или отправьте pull request.
