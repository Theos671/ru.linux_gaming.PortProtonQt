# Flatpak пакет PortProtonQt
## Сборка пакета
### Требования
- `git`
- `git-lfs`
- `flatpak`
- `flatpak-builder`
### Сборка
- Клонировать репозиторий:  
  `git clone https://github.com/Theos671/ru.linux_gaming.PortProtonQt.git`
- Загрузить сабмодули:  
  `git submodule update --init --recursive`
- Собрать:
    1. Поэтапно
        - Собрать PortProtonQt:  
        `flatpak-builder --force-clean --install-deps-from=flathub build/build-dir ru.linux_gaming.PortProtonQt.yml`
        - Экспортировать собранные файлы для подготовки к установке:  
        `flatpak build-export build/export-dir build/build-dir`
        - Создать установочный файл .flatpak:  
        `flatpak build-bundle build/export-dir build/PortProtonQt.flatpak ru.linux_gaming.PortProtonQt`
    2. Сразу
        - Собрать и создать установочный файл:  
        `flatpak-builder --force-clean --install-deps-from=flathub --repo=build/export-dir build/build-dir ru.linux_gaming.PortProtonQt.yml && flatpak build-bundle build/export-dir build/PortProtonQt.flatpak ru.linux_gaming.PortProtonQt`
- Установка и запуск:
    1. Запуск без установки  
       `flatpak-builder --run build/build-dir ru.linux_gaming.PortProtonQt.yml portprotonqt`
    2. Сначала установка, потом запуск  
        - Установка:  
          `flatpak install --user build/PortProtonQt.flatpak`
        - Запуск:  
          `flatpak run --user ru.linux_gaming.PortProtonQt`
## Генерация списка зависимостей (при внесении изменений)
### Требования
- `req2flatpak`  
### Генерация
- Внести необходимые изменения в [requirements.txt](./requirements.txt)
- `req2flatpak --requirements-file requirements.txt --yaml --target-platforms 313-x86_64 --outfile ru.linux_gaming.PortProtonQt.pypi-deps.yaml`
