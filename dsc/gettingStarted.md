---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Начало работы с настройкой требуемого состояния PowerShell
ms.openlocfilehash: a449382c979e680ea311c887c86cb675ba6162b7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189726"
---
# <a name="getting-started-with-powershell-desired-state-configuration"></a>Начало работы с настройкой требуемого состояния PowerShell #

В этом руководстве описывается, как приступить к созданию документов настройки требуемого состояния PowerShell и применять их к компьютерам. Предполагается, что пользователь уже знаком с командлетами, модулями и компонентами PowerShell.


## <a name="create-a-configuration"></a>Создание конфигурации ##

[**Конфигурации**](https://msdn.microsoft.com/powershell/dsc/configurations) — это документы, которые описывают среду. Среды состоят из "**узлов**", которые обычно представляют собой компьютеры или виртуальные машины.

Конфигурации могут иметь различные формы. Самый простой способ создания конфигурацию — с помощью PS1-файла (сценария PowerShell). Чтобы создать этот файл, откройте любой текстовый редактор. Лучше всего использовать интегрированную среду сценариев PowerShell — она работает с DSC наилучшим образом. Сохраните следующее как PS1-файл:

```powershell
configuration MyFirstConfiguration
{
    Import-DscResource -Name WindowsFeature

    Node localhost
    {
        WindowsFeature IIS
        {
            Name = "IIS"

        }

    }

}
```
## <a name="parts-of-a-configuration"></a>Элементы конфигурации ##
**Configuration** — это ключевое слово, добавленное в PowerShell 4.0. Оно означает особый вид компонентов PowerShell, используемых настройкой требуемого состояния. В этом примере компоненту присвоено имя myFirstConfiguration.

Следующая строка представляет собой оператор импорта, который аналогичен импорту модуля. Его мы обсудим позже.

Узел — это имя компьютера, на котором эта конфигурация будет запущена. Данная конфигурация редактируется локально, однако конфигурации могут охватывать не только локальные, но и удаленные узлы.

Узлы могут задаваться именами или IP-адресами компьютеров. Один документ конфигурации может содержать сразу несколько узлов. Используя [данные конфигурации](https://msdn.microsoft.com/powershell/dsc/configdata), можно применить одну и ту же конфигурацию сразу к нескольким узлам. В данном случае указан узел localhost, т. е. локальный компьютер.

Следующий элемент — это [**ресурс**](https://msdn.microsoft.com/powershell/dsc/resources). Ресурсы — это составные компоненты конфигураций. Каждый ресурс — это модуль, определяющий логику реализации отдельного аспекта компьютера. Каждый ресурс можно просмотреть на компьютере, выполнив командлет **Get-DscResource** в PowerShell. Для использования в конфигурации ресурсы необходимо импортировать на локальный компьютер с помощью командлета **Import-DscResource**, который находится во второй строке данной конфигурации.

**Активирование конфигурации**

При сохранении и выполнении представленного выше сценария выходные данные не создаются. Это связано с тем, что конфигурация — это просто функция, а в представленном выше сценарии эта функция определена, но еще не запущена. После определения функцию необходимо вызвать:
```powershell
myFirstConfiguration
```

Во время выполнения функции конфигурации проверяют ее работоспособность. В конфигурации не должно быть синтаксических ошибок, в ресурсах должны присутствовать все обязательные параметры, при этом все ресурсы перед выполнением должны быть импортированы.

После выполнения конфигурации создается папка с именем конфигурации, содержащая **MOF-файл** для каждого включенного в нее узла. MOF-файл — это формат управления на основе стандартов, используемый DSC PowerShell для обмена данными по сети.

Активирование конфигурации:
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration
```
Эта команда создает задание PowerShell, которое настраивает указанные в конфигурации узлы. Для просмотра выходных данных задания используйте параметр -Wait.
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration -Wait
```