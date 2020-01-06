# Медиа сервер из старого ноутбука

Старый ноутбук валяется дома без дела? Сделай из него модный сервак! Путем нехитрых манипуляций твой ноут сможет:

1. Качать и раздавать торренты
2. Стримить фильмы на разные устройства
3. Хранить документы и фотки на собственном облаке, аналог гугл диска. Теперь сотрудники гугла больше не увидят фото твоего члена (возможно это минус)

Использованые репозитории:

1. [docker-transmission](https://github.com/linuxserver/docker-transmission)
2. [docker-plex](https://github.com/linuxserver/docker-plex)
3. [docker-owncloud](https://github.com/owncloud-docker/server)

## Установка

### Пердварительная подготовка

Ставим себе убунту сервер, желательно последний LTS

1. Устанавливаем докер

   ```bash
   sudo apt install docker.io
   ```

2. Добавляем текущего юзера в группу docker, чтобы использовать его без sudo

   ```bash
   sudo usermod -aG docker $USER
   ```

3. Устанавливаем docker-compose

   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

4. Даем права на запуск docker-compose

   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

### Lid-switch

Чтобы ноут не отключался при закрытии крышки нужно игнорировать lid-switch.
Открываем /etc/systemd/logind.conf в любом редакторе

```bash
sudo vim /etc/systemd/logind.conf
```

и создаем/редактируем там строку(у строки не должно быть символа коммента #)

` HandleLidSwitch=ignore

Перезапускаем сервис

```bash
sudo systemctl restart systemd-logind
```

### Поднимаем контейнеры

Нам нужно поднять три сервиса:

1. transmission для торрентов
2. plex для медиа сервиса
3. owncloud для облака

Заходим в соответствующие папки, редактируем .env под себя и запускаем

```bash
docker-compose up -d
```
