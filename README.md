# Kimi Code — русская локализация

Неофициальная русская локализация десктопного клиента [Kimi Code](https://www.kimi.com/) для Windows.
Скрипт добавляет в приложение полноценный русский словарь (2954 строки интерфейса) и пункт «Русский» в настройки языка.

## Установка

1. Скачайте репозиторий (Code → Download ZIP) и распакуйте.
2. Полностью закройте Kimi Code.
3. Запустите:

```powershell
powershell -ExecutionPolicy Bypass -File install.ps1
```

Если приложение установлено в `Program Files`, появится запрос UAC — подтвердите.
4. Запустите Kimi Code. На русской Windows язык включится автоматически; иначе выберите **Настройки → Language → Русский**.

Без скачивания всего репозитория (одной командой):

```powershell
iwr https://raw.githubusercontent.com/fedorka812/kimi-code-ru/main/install.ps1 -OutFile "$env:TEMP\kimi-ru-install.ps1"; powershell -ExecutionPolicy Bypass -File "$env:TEMP\kimi-ru-install.ps1"
```

Если Kimi Code установлен в нестандартном месте:

```powershell
powershell -ExecutionPolicy Bypass -File install.ps1 -InstallDir "D:\Apps\Kimi Code"
```

## Удаление (откат)

```powershell
powershell -ExecutionPolicy Bypass -File install.ps1 -Restore
```

Оригинальные файлы восстановятся из бэкапов `.orig`, которые скрипт создаёт при первой установке.

## Как это работает

Kimi Code — Electron-приложение со встроенной системой локализации (vue-i18n) и двумя языками из коробки: английским и китайским. Скрипт:

- встраивает словарь `ru` в `resources\desktop-dist\assets\SegmentedControl-*.js`;
- разрешает локаль `ru` в функции определения языка (включая автоопределение по `navigator.language`);
- добавляет «Русский» в переключатель языка в `main-*.js`.

Перед изменением каждый файл сохраняется с расширением `.orig`. Если ожидаемые участки кода не найдены (например, после крупного обновления), скрипт завершается с ошибкой, **ничего не меняя**.

## Важно

- После обновления Kimi Code патч затирается — просто запустите скрипт ещё раз.
- Проверено на сборке Kimi Code от 20.11.2026 (Windows 11).
- Проект неофициальный и не связан с Moonshot AI. Используйте на свой страх и риск.

## Словарь

Перевод лежит в [ru.json](ru.json) — пригодится, если захотите улучшить формулировки. Плейсхолдеры вида `{name}`, `{count}` и разметку изменять нельзя.
