---
ms.date: 03/27/2018
contributor: JKeithB
keywords: коллекция,powershell,psgallery,GDPR
title: Соответствие коллекции PowerShell регламенту GDPR
ms.openlocfilehash: 14b82fa07df52f02f0d7577cb0eef70faa4285a2
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893252"
---
# <a name="powershell-gallery-gdpr-compliance"></a>Соответствие коллекции PowerShell регламенту GDPR

## <a name="overview"></a>Обзор

В мае 2018 г. вступает в силу европейский закон о конфиденциальности — Общий регламент по защите данных (GDPR).
GDPR налагает новые требования на компании, государственные учреждения, некоммерческие и другие организации, которые предоставляют товары и услуги жителям ЕС либо собирают и анализируют данные, связанные с резидентами ЕС.
GDPR применяется независимо от того, где вы находитесь.

> [!NOTE]
> Эта статья описывает шаги по удалению персональных данных из коллекции PowerShell и помогает вам выполнить обязательства в рамках GDPR. Если вы ищете общие сведения о GDPR, см. [раздел о GDPR на Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="personally-identifiable-data"></a>Персональные данные

Коллекция PowerShell хранит следующие сведения, в том числе и предоставляемые пользователями, куда могут входить и персональные данные.

- Учетная запись коллекции PowerShell
- Элементы, опубликованные в коллекции PowerShell
- Переписка с группой коллекции PowerShell по электронной почте

Большинство пользователей не создает учетную запись коллекции PowerShell.
Учетная запись не требуется, если только вы не захотите опубликовать элемент или воспользоваться функцией Contact Owner (Связаться с владельцем) в коллекции PowerShell.
Кроме переписки по электронной почте, начатой пользователем, коллекция PowerShell не сохраняет персональные данные для пользователей без учетной записи.

Пользователи, создающие учетную запись, могут публиковать элементы в коллекции PowerShell.
Эти элементы должны быть кодом PowerShell, но могут содержать и другие сведения, включая личные данные.
Приведенные ниже сведения показывают, как получить все элементы, опубликованные вами в коллекции PowerShell.

## <a name="dsr-export-of-powershell-gallery-data"></a>Экспорт данных из коллекции PowerShell по запросу DSR

Следующие разделы описывают, как коллекция PowerShell поддерживает запросы субъекта данных (DSR), и поясняют, как экспортировать данные, хранящиеся в коллекции PowerShell, и запросить их удаление.

### <a name="email"></a>Электронная почта

Переписка по электронной почте может содержать любые из следующих сведений.

- Сообщение, отправленное владельцам элементов в коллекции PowerShell, если анализ кода выявил проблему с любым из опубликованных ими элементов.
- Сообщение, отправленное любым сотрудником группы коллекции PowerShell с использованием адреса электронной почты на странице контактов [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com).
- Зарегистрированные пользователи, использующие функцию Contact Owner (Связаться с владельцем) для отправки сообщения владельцу элемента.

Для сообщений, которыми пользователи обмениваются с группой коллекции PowerShell, действует политика хранения в течение 90 дней для проведения возможных расследований в случае обнаружения вредоносного кода в коллекции PowerShell.
Через 90 дней сообщения удаляются.

Вы можете запросить копии всех сообщений, которыми вы обменивались с группой коллекции PowerShell со своего адреса электронной почты за последние 90 дней.
Чтобы запросить эту переписку, отправьте на адрес [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com) сообщение электронной почты с заголовком DSR Request for emails relating to this account (Запрос DSR на получение сообщений электронной почты, связанных с этой учетной записью).
В тексте сообщения укажите, какую именно информацию вы запрашиваете (например, попросите отправить все сообщения электронной почты, отправленные или полученные с помощью этого адреса электронной почты). Все сообщения, связанные с вашим адресом электронной почты, за 90 дней будут отправлены вам в течение 7 рабочих дней.

### <a name="powershell-gallery-account-information"></a>Информация об учетной записи коллекции PowerShell

Если вы создали учетную запись коллекции PowerShell, то можете найти все хранящиеся в коллекции персональные данные, сделав следующее.

1. Войдите в коллекцию PowerShell и щелкните свое имя пользователя.
2. Отображается страница учетной записи, где указан адрес электронной почты, используемый для этой учетной записи коллекции PowerShell.

Если вы создали в коллекции PowerShell несколько учетных записей, потребуется повторить эти шаги для каждой из них.

### <a name="items-in-the-powershell-gallery"></a>Элементы в коллекции PowerShell

Чтобы упростить экспорт элементов, опубликованных в коллекции PowerShell, корпорация Майкрософт опубликовала сценарий GetPSGalleryItemsForAuthor в коллекции PowerShell.
Он экспортирует копию каждой версии каждого элемента, помещенного в коллекцию PowerShell, на основе хранящихся в элементе сведений об авторе.

> [!NOTE]
> Автор сохраняется в манифесте элемента при публикации элемента.
> Нет никакой гарантии, что автор относится к тому же удостоверению, что и учетная запись, используемая вами в коллекции PowerShell.
> Если в поле "Автор" вы используете другое значение, нужно указать его при использовании этого сценария.

Вы можете скачать сценарий, используя следующую команду PowerShell:

```powershell
Save-Script Get-repository psgallery
```

После этого его можно запустить напрямую с помощью следующих команд PowerShell:

```powershell
# cd <local folder location>
.\GetPSGalleryItemsForAuthor.ps1
```

Вам будет предложено указать автора и папку в системе, куда требуется сохранить элементы.

## <a name="deleting-personal-data-from-the-powershell-gallery"></a>Удаление персональных данных из коллекции PowerShell

Чтобы удалить учетную запись коллекции PowerShell или любой принадлежащий вам элемент в этой коллекции, отправьте на адрес cgadmin@microsoft.com сообщение электронной почты с заголовком GDPR Request for items relating to this account (Запрос GDPR по элементам, связанным с этой учетной записью).
В тексте сообщения укажите, какую информацию требуется удалить. Например:

- попросите удалить версию x.y.z своего элемента "имя элемента";
- попросите удалить все версии своего элемента "имя элемента";
- попросите удалить свою учетную запись коллекции PowerShell.

Администраторы коллекции PowerShell ответят вам в течение 7 рабочих дней.
Указанные элементы будут удалены в течение 30 дней после отправки запроса.