---
ms.date: 06/12/2017
keywords: wmf,powershell,установка
title: Усовершенствования консоли в WMF 5.1
ms.openlocfilehash: a8e82e2f973916c2ed5007eba90ee6f2b7a9a769
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892932"
---
# <a name="console-improvements-in-wmf-51"></a>Усовершенствования консоли в WMF 5.1

## <a name="powershell-console-improvements"></a>Усовершенствования консоли PowerShell

Для улучшения работы с консолью в Powershell.exe в WMF 5.1 были внесены перечисленные ниже изменения.

### <a name="vt100-support"></a>Поддержка VT100

В Windows 10 реализована поддержка [escape-последовательностей VT100](/windows/console/console-virtual-terminal-sequences).
При расчете ширины таблиц PowerShell игнорирует некоторые escape-последовательности форматирования VT100.

В PowerShell также появился новый интерфейс API, который можно использовать при форматировании кода для определения наличия поддержки VT100.
Например:

```powershell
if ($host.UI.SupportsVirtualTerminal)
{
    $esc = [char]0x1b
    "A yellow ${esc}[93mhello${esc}[0m"
}
else
{
    "A default hello"
}
```

Вот полный [пример](https://gist.github.com/lzybkr/dcb973dccd54900b67783c48083c28f7), который можно использовать для выделения совпадений в результатах выполнения командлета `Select-String`.
Сохраните пример в файле с именем `MatchInfo.format.ps1xml`. Чтобы использовать его, в своем профиле или другом месте выполните команду `Update-FormatData -Prepend MatchInfo.format.ps1xml`.

Имейте в виду, что escape-последовательности VT100 поддерживаются начиная с юбилейного обновления Windows 10. В более ранних системах они не поддерживаются.

### <a name="vi-mode-support-in-psreadline"></a>Поддержка режима vi в PSReadline

В [PSReadline](https://github.com/lzybkr/PSReadLine) добавлена поддержка режима vi. Чтобы включить режим vi, выполните команду `Set-PSReadlineOption -EditMode Vi`.

### <a name="redirected-stdin-with-interactive-input"></a>Перенаправленный поток stdin с интерактивным вводом

В предыдущих версиях среду PowerShell требовалось запускать с помощью команды `powershell -File -`, если поток stdin перенаправлялся и необходимо было вводить команды в интерактивном режиме.

В WMF 5.1 этот сложный для обнаружения вариант больше не требуется.
PowerShell можно запустить без параметров, например `powershell`.

Обратите внимание на то, что PSReadline в настоящее время не поддерживает перенаправленный поток stdin, а встроенные возможности редактирования в командной строке с перенаправленным потоком stdin крайне ограничены, например не работают клавиши со стрелками.
В будущих версиях PSReadline эта проблема должна быть решена.