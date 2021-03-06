---
title: Установка PowerShell Core в macOS
description: Сведения об установке PowerShell Core в macOS
ms.date: 08/06/2018
ms.openlocfilehash: ff1814d95b3ca3fa8497069dff249fd2ad5576ef
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587471"
---
# <a name="installing-powershell-core-on-macos"></a>Установка PowerShell Core в macOS

PowerShell Core поддерживает macOS версии 10.12 и более поздних версий
Все пакеты доступны на нашей странице [Выпуски][] GitHub.
После установки пакета запустите `pwsh` из терминала.

### <a name="installation-via-homebrew-on-macos-1012"></a>Установка в macOS 10.12+ с помощью Homebrew

[Homebrew][brew] является предпочтительным диспетчером пакетов для macOS.
В окне терминала введите `brew` для запуска Homebrew.  Если команда `brew` не найдена, нужно установить Homebrew по [соответствующим инструкциям][brew].

> [!NOTE]
> Если вы уже установили Homebrew, настоятельно рекомендуется выполнить команды brew update-reset и brew update.
```sh
brew update-reset
brew update
```

> Для более старых версий Homebrew использовалось касание caskroom/cask. Сейчас вместо этого используется homebrew/cask.  Дополнительные сведения см. в справочнике по [Homebrew-cask][cask]. Используйте команду brew tap, чтобы получить список текущих касаний.  Если вы видите caskroom/cask, можно использовать brew-update, чтобы выполнить перенос касаний в Homebrew.

```sh
brew tap
brew update
```

После установки или обновления Homebrew установка PowerShell не вызывает проблем.

Чтобы установить PowerShell:

```sh
brew cask install powershell
```

И наконец, убедитесь, что установка прошла без ошибок.

```sh
pwsh
```

Чтобы выйти из PowerShell и вернуться в bash, используйте команду exit.
```sh
exit
```

После выпуска новых версий PowerShell просто обновите формулы Homebrew и PowerShell:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> Приведенные выше команды можно вызвать с узла PowerShell (pwsh), но затем потребуется выйти из оболочки PowerShell и перезапустить ее, чтобы завершить обновление и обновить значения в таблице $PSVersionTable.

### <a name="installing-preview-via-homebrew-on-macos-1012"></a>Установка предварительной версии в macOS 10.12+ с помощью Homebrew

[Homebrew][brew] является предпочтительным диспетчером пакетов для macOS.
В окне терминала введите `brew` для запуска Homebrew.  Если команда `brew` не найдена, нужно установить Homebrew по [соответствующим инструкциям][brew].

> [!NOTE]
> Если вы уже установили Homebrew, настоятельно рекомендуется выполнить команды brew update-reset и brew update.
```sh
brew update-reset
brew update
```

После этого коснитесь репозитория `versions` casks, чтобы получить пакет предварительной версии:

```sh
brew tap homebrew/cask-versions
```

Чтобы установить предварительную версию PowerShell:

```sh
brew cask install powershell-preview
```

И наконец, убедитесь, что установка прошла без ошибок.

```sh
pwsh-preview
```

После выпуска новых версий PowerShell просто обновите формулы Homebrew и предварительную версию PowerShell:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> Приведенные выше команды можно вызвать с узла PowerShell (pwsh), но затем потребуется выйти из оболочки PowerShell и перезапустить ее, чтобы завершить обновление и обновить значения в таблице $PSVersionTable.

### <a name="installation-via-direct-download"></a>Установка с помощью прямого скачивания

Для компьютера с macOS пакет PKG `powershell-6.0.2-osx.10.12-x64.pkg` можно загрузить на странице [Выпуски][].

Дважды щелкните файл и следуйте инструкциям на экране либо установите его из командной строки:

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a>Архивы двоичных файлов

Для поддержки расширенных сценариев развертывания на платформах macOS и Linux доступны архивы двоичных файлов PowerShell `tar.gz`.

### <a name="installing-binary-archives-on-macos"></a>Установка архивов двоичных файлов в macOS

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.2

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.2

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.2/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.2/pwsh /usr/local/bin/pwsh
```

## <a name="uninstalling-powershell-core"></a>Удаление PowerShell Core

Если вы установили PowerShell с помощью Homebrew, удаление осуществляется очень просто:

```sh
brew cask uninstall powershell
```

Если вы установили PowerShell с помощью прямого скачивания, PowerShell нужно удалить вручную:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Чтобы удалить дополнительные пути PowerShell, ознакомьтесь с разделом [пути][] этой статьи, и удалите необходимые пути с помощью команды `sudo rm`.

> [!NOTE]
> Это не требуется в случае установки с помощью Homebrew.

[пути]:#paths

## <a name="paths"></a>Пути

* `$PSHOME` имеет значение `/usr/local/microsoft/powershell/6.0.2/`.
* Профили пользователей будут считаны из `~/.config/powershell/profile.ps1`.
* Профили по умолчанию будут считаны из `$PSHOME/profile.ps1`.
* Модули пользователей будут считаны из `~/.local/share/powershell/Modules`.
* Общие модули будут считаны из `/usr/local/share/powershell/Modules`.
* Модули по умолчанию будут считаны из `$PSHOME/Modules`.
* Журнал PSReadline будет записан в `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`.

Профили учитывают конфигурацию PowerShell для отдельных узлов.
Поэтому профили конкретных узлов по умолчанию находятся в `Microsoft.PowerShell_profile.ps1` в тех же расположениях.

PowerShell отвечает требованиям [спецификации каталога размещения файлов, связанных со средой настольной графической среды (X-сервера), стандартизированного XDG (X Desktop Group)][xdg-bds] в macOS.

Так как macOS является развитием BSD, необходимо использовать префикс `/usr/local` вместо `/opt`.
Таким образом, `$PSHOME` имеет значение `/usr/local/microsoft/powershell/6.0.2/`, а символьная ссылка размещается в `/usr/local/bin/pwsh`.

## <a name="additional-resources"></a>Дополнительные ресурсы

* [Homebrew Web][brew]
* [Репозиторий Github Homebrew][GitHub]
* [Homebrew-Cask][cask]


[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[Выпуски]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
