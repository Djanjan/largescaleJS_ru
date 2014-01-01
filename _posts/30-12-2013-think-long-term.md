---
layout: page
title: "Глава 4. Мозговой штурм"
---

Давайте на мгновение задумаемся достичь то, что нам нужно.

Мы хотим слабосвязанную архитектуру с функциональностью, разбитой
на **независимые модули**, которые в идеале не должны иметь зависимостей от друг
друга. Когда происходит что-то интересное, модули **сообщают** об этом другим
частям приложения, промежуточный слой интерпретирует их сообщения и необходимым
образом реагирует на них.

Для примера, у нас есть JavaScript-приложение, отвечающее за онлайн-пекарню,
и одно из интересных сообщений может быть таким: «Партия из 42 батонов готова
к доставке».

Мы используем отдельный слой для обработки сообщений от модулей для того, чтобы
а) модули не взаимодействовали напрямую с ядром б) модули не взаимодействовали
напрямую друг с другом. Это помогает удержать приложение от падения из-за
различных ошибок внутри какого-нибудь модуля, и позволяет нам перезапускать
модули если они перестали работать из-за ошибки.

Еще один момент — безопасность. В действительгности, многие из нас не заботятся
в должной мере о внутренней безопасности приложений. Когда мы определяем
структуру приложений, мы говорим себе, что мы достаточно умны для того, чтобы
понимать что должно быть доступно публично, а что приватно. 

Как бы то ни было, поможет ли это если вы решите определить что именно разрешено
модулю выполнять в системе? К примеру, в моей системе, ограничив доступ из
модуля веб-чата к интерфейсу модуля администрирования, я смогу уменьшить шансы
на успешное экплуатирование XSS уязвимостей, которые я не смог найти в виджете.
Модули не должны иметь доступ ко всему. Вероятно, в вашей существующей
архитектуре они могут использовать любые части системы, но уверенны ли вы, что
это действительно необходимо?

Промежуточный слой, проверяющий имеет ли модуль доступ к определенной части
вашего фреймворка, обеспечивает большую безопасность вашей системы. Фактически,
это значит что модули могут взаимодействовать только с теми компонентами 
системы, с которым мы разрешим им взаимодействовать.