# Mac from scratch

Руководство по настройке нового MacBook для разработки.
Охватывает установку основных приложений, инструментов и настройку окружения

---

## Содержание

- [Приложения](#приложения)
- [Homebrew](#homebrew)
- [Терминал](#терминал)
- [Python](#python)
- [Клавиатура](#клавиатура)
- [Raycast](#raycast)

---

## Приложения

* [Warp](https://www.warp.dev/) - Современный терминал с AI-ассистентом, умным автодополнением,
кастомизацией и многими другими возможностями. Возможно, кому-то покажется слишком перегруженым,
поэтому можно выбрать blazzingly fast альтернативу [Ghostty](https://github.com/ghostty-org/ghostty)
* [Raycast](https://www.raycast.com/) - Мощная замена Spotlight с расширениями, историей буфера,
обмена и встроенным AI (платно). Содержит множество полезных функций и поддерживает плагины.
Рекомендую заменить Spotlight (и шорткат для вызова) на Raycast.
* [Zed Editor](https://zed.dev/) - Быстрый и лёгкий редактор кода, написанный на Rust, с поддержкой
AI и совместного редактирования. Либо по классике [VS Code](https://code.visualstudio.com/docs/setup/mac#_install-vs-code-on-macos)
* [OrbStack](https://orbstack.dev/) - Лёгкая и быстрая альтернатива Docker Desktop для запуска
контейнеров на Mac. Альтернативы:
[Docker Desktop](https://www.docker.com/products/docker-desktop),
[Colima](https://github.com/abiosoft/colima).
* [Arc Browser](https://arc.net/) - Очень крутой браузер с боковой панелью вкладок, разделением
рабочих пространств (профили) и другими инструментами для повышения продуктивности. К сожалению,
разработчики решили пойти за хайпом и делать другой браузер на основе AI, поэтому новых фич
и активного развития не будет. Можно также дать шанс
[Zen](https://zen-browser.app/download/),
[Helium](https://helium.computer/),
Safari (Зато там работают всякие интеграции с экосистемой Apple)
* [Rectangle](https://rectangleapp.com/) - Менеджер окон с горячими клавишами для размещения окон
по половинам, углам и другим зонам экрана. Я использую [конфиг от Никиты Соболева](https://github.com/sobolevn/dotfiles/blob/master/config/RectangleConfig.json).
* [Scroll Reverser](https://pilotmoon.com/scrollreverser/) - Позволяет независимо настроить
направление прокрутки для мыши и трекпада. Альтернатива: [Mos](https://github.com/Caldis/Mos)
* [Shottr](https://shottr.cc/) - Одно из лучших приложений для скриншотов на MacOS.
* [Karabiner Elements](https://karabiner-elements.pqrs.org/) - Кастомизация клавиатуры и шорткатов.
* [TopNotch](https://topnotch.app/) - Скрывает чёлку MacBook, делая строку меню полностью чёрной.
* [HazeOver](https://hazeover.com/) - Затемняет неактивные окна, помогая сосредоточиться на текущем приложении (Платное).

---

## Homebrew

[Homebrew](https://brew.sh/) — самый популярный пакетный менеджер для macOS. Позволяет устанавливать утилиты командной строки и приложения прямо из терминала.

**Установка:**

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

После установки следуйте инструкциям в терминале, чтобы добавить Homebrew в `PATH`.

**Проверка:**

```sh
brew --version
```

---

## Терминал

### Zsh

Zsh является оболочкой по умолчанию в macOS. [Oh My Zsh](https://ohmyz.sh/) — популярный фреймворк для управления конфигурацией, темами и плагинами Zsh.

**Плагины:**

Я использую следуюшие плагины (`zsh-autosuggestions` и `zsh-syntax-highlighting` требуют отдельной установки):

```sh
plugins=(
  git
  docker
  composer
  npm
  sudo
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```

* [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) - Предлагает команды по мере ввода на основе истории.
* [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) - Подсвечивает команды в терминале во время набора.

**Тема:**

[powerlevel10k/powerlevel10k](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#installation) - Высоконастраиваемая тема для Zsh с быстрым рендерингом и интерактивным мастером настройки.

### Редактор в терминале

Для быстрого редактирования иногда удобно использовать редактор в терминале. Т.к. я делаю
только небольшие изменения, пользуюсь в основном [Helix](https://helix-editor.com/) -
cовременный модальный редактор со встроенной поддержкой LSP и tree-sitter.
Для ценителей как альтернатива [Neovim](https://neovim.io/) - расширяемый и гибко
настраиваемый текстовый редактор.

**Установка:**

```sh
brew install neovim
# или
brew install helix
```

### Git

macOS поставляется с Git, установленным через Xcode Command Line Tools — запрос на их установку появляется при первом использовании `git`. Также можно установить актуальную версию через Homebrew:

```sh
brew install git
```

**Базовая настройка:**

```sh
git config --global user.name "Ваше Имя"
git config --global user.email "ваш@email.com"
git config --global init.defaultBranch main
git config --global core.editor "hx"  # Helix если нужно
```

**SSH-ключ:** Рекомендуется настроить SSH-ключ для аутентификации на GitHub. См. [документацию GitHub по SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).

---

## Python

macOS поставляется с системным Python. Для управления версиями Python и виртуальными окружениями рекомендуется использовать [uv](https://docs.astral.sh/uv/) — быстрый и современный менеджер пакетов и проектов для Python.

**Установка uv:**

```sh
brew install uv
```

**Установка последней версии Python:**

```sh
# чтобы установить глобально
brew install python
# или можно через uv
uv python install
```

**Установка глобальной версии по умолчанию:**

```sh
uv python pin --global
```

> Это задаёт версию Python по умолчанию для всех команд `uv` (например, `uv run`, `uv venv`). Системный бинарник `python3` в терминале при этом не изменяется.

**`uvx`** позволяет запускать CLI-инструменты Python в изолированных окружениях без глобальной установки, аналогично `pipx`:

```sh
uvx ruff check .
```

---

## Клавиатура

### Раскладка Russian - PC

По-умолчанию русская раскладка на MacOS немного странная, хотя соответствует русской гравировке
(запятая shift+6, ё может быть не в том месте). Лучше установить другую:
Перейдите в **Системные настройки → Клавиатура → Ввод текста → Изменить** и добавьте раскладку
**Russian - PC**.

### Скорость повтора клавиш

По умолчанию macOS добавляет задержку перед началом повтора символа при зажатии клавиши. Это
неудобно в Neovim/Helix, где клавиши `h`, `j`, `k`, `l` используются для навигации при удержании.

Перейдите в **Системные настройки → Клавиатура** и установите:
- **Скорость повтора клавиш** — на максимальное значение (Fast/Быстро)
- **Задержка до повтора** — на минимальное значение (Short/Короткое)

Для более точной настройки можно полностью убрать задержку через терминал (опционально):

```sh
defaults write -g InitialKeyRepeat -int 10
defaults write -g KeyRepeat -int 1
```

После этого перезагрузите Mac, чтобы изменения вступили в силу.

### Caps Lock → Escape

Caps Lock используется редко, но занимает удобное положение на клавиатуре. Переназначение его на
`Escape` значительно упрощает выход из режима вставки в Neovim/Helix.

Перейдите в **Системные настройки → Клавиатура → Горячие клавиши → Клавиши-модификаторы** 
установите для **Caps Lock** действие **Escape**.

Но гораздо лучше сделать это через Raycast.

---

## Raycast

### Плагины

Плагины можно найти в [магазине на официальном сайте](https://www.raycast.com/store?platform=macOS#list),
устанавливаются они легко и по клику. Я просто выделю интересные:

- [One Time Password](https://www.raycast.com/lachero/one-time-password) - легко получать OTP токены
- [Github](https://www.raycast.com/raycast/github) - работа с GitHub (уведомления, поиск)
- [Brew](https://www.raycast.com/nhojb/brew) - работа с brew прямо из Raycast

### Настройка

По нажатию `CMD + ,` можно открыть настройки и найти там много интересного.
Но самое главное - нужно превратить бесполезный Caps Lock в суперполезную
Hyper клавишу:

Advanced -> Hyper Key = Caps Lock; Quick Press = Triggers Esc

Теперь можно пойти во вкладу Extensions и поставить Hotkey через Caps Lock
на любые приложения.
