### Этапы разработки проекта Atlas

> [!INFO]
> Временные промежутки указанные ниже являются примерными и будут обговариваться командой. 
> 
#### 1. **Создание и тестирование базовых микросервисов**
##### Делаем:
- Разработка первых трёх ключевых сервисов:
    1. User Management Service.
    2. Project Management Service.
    3. OAuth Configuration Service.
- Тестирование сервисов в изоляции:
    - Проверка базового функционала каждого сервиса.
    - Юнит-тестирование основных методов и API-эндпоинтов.
- Реализация mock-хранилищ для каждого сервиса для имитации работы с данными.
##### Почему:
- Начало с отдельных микросервисов позволяет сфокусироваться на функционале каждого компонента. Это упрощает разработку и тестирование, поскольку на начальном этапе нет зависимости от других сервисов.
- Изоляция сервисов помогает быстрее находить ошибки и повышает стабильность дальнейшей интеграции.
##### Цель:
- Убедиться, что каждый сервис выполняет свои основные функции корректно и стабильно в изолированной среде. Подготовить их к интеграции с другими компонентами.
##### Временные промежутки:
- 3-4 недели
#### 2. **Интеграция баз данных**
##### Делаем:
- PostgreSQL как основная база данных для хранения пользователей и проектов.
- Добавление Redis для кэширования данных OAuth.
- Настройка взаимодействия между сервисами и базой данных.
- Тестирование взаимодействия:
    - Проверка транзакций.
    - Обработка ошибок при работе с базой данных.
##### Почему:
 - После отработки базового функционала сервисов добавляется хранилище данных. Это упрощает миграцию от mock-хранилищ к реальной работе с данными.
 - Сразу настраивается взаимодействие с данными, чтобы избежать проблем в интеграции сервисов на поздних этапах.
##### Цель:
- Обеспечить надёжное хранилище данных для системы и наладить работу сервисов с реальными данными. Устранить потенциальные проблемы взаимодействия с базой данных.
##### Временные промежутки:
- 2 недели
#### 3. **Добавление Gateway для маршрутизации**
##### Делаем:
- Реализация API Gateway для унифицированного входа в систему.
- Настройка маршрутов между сервисами через Gateway.
- Внедрение базовой системы авторизации в Gateway.
##### Почему:
- Gateway вводится на этапе, когда базовые сервисы и взаимодействие с данными работают стабильно. Это позволяет объединить сервисы в единую систему без лишних сложностей.
- Настройка маршрутизации через Gateway на этом этапе упрощает тестирование взаимодействия между микросервисами.
##### Цель:
- Объединить все сервисы под единым шлюзом для удобной маршрутизации запросов. Обеспечить централизованную точку входа в систему.
##### Временные промежутки:
- 1-2 недели
#### 4. **Разработка Auth Service**
##### Делаем:
- Создание сервиса аутентификации:
    - Хранение учётных данных и токенов OAuth.
    - Проверка токенов для обеспечения безопасности.
- Интеграция Auth Service с Gateway для обработки запросов.
- Тестирование работы аутентификации.
##### Почему:
- Auth Service разрабатывается после Gateway, так как требует настроенного входного шлюза для управления доступом к сервисам.
- Безопасность интегрируется на этапе, когда базовые функции системы уже работают, чтобы минимизировать риск проблем с доступом.
##### Цель:
- Реализовать механизм аутентификации и управления доступом, чтобы обеспечить безопасность взаимодействия между пользователями и сервисами.
##### Временные промежутки:
- 2-3 недели
#### 5. **Создание Web Application**
##### Делаем:
- Разработка пользовательского интерфейса:
    - Управление пользователями и проектами.
    - Настройка OAuth интеграции через интерфейс.
- Интеграция Web Application с Gateway.
##### Почему:
- Пользовательский интерфейс внедряется только после создания backend-компонентов, чтобы UI мог сразу работать с полноценным API.
- Это предотвращает необходимость переработки интерфейса при изменении backend-логики.
##### Цель:
- Предоставить пользователям интерфейс для взаимодействия с системой, включающий управление пользователями, проектами и настройкой OAuth.
##### Временные промежутки:
- 3-4 недели
#### 6. **Тестирование взаимодействия системы**
##### Делаем:
- Проведение интеграционных тестов:
    - Проверка работы всех сервисов в связке.
    - Нагрузочное тестирование.
    - Проверка отказоустойчивости.
##### Почему:
- Интеграционные тесты запускаются после завершения всех ключевых компонентов, чтобы проверить их совместную работу. Если тесты запускать раньше, то возможны ложные сбои из-за недоработанных частей системы.
##### Цель:
- Проверить совместную работу всех компонентов системы. Убедиться, что они корректно обмениваются данными и выдерживают нагрузки.
##### Временные промежутки:
- 1-2 недели
#### 7. **Автоматизация процессов с помощью DevOps**
##### Делаем:
- Настройка CI/CD конвейеров для автоматической сборки и развертывания.
- Контейнеризация сервисов с использованием Docker.
- Развёртывание системы в Kubernetes для управления микросервисами.
- Настройка мониторинга и логирования.
##### Почему:
- Автоматизация развёртывания выполняется ближе к финальной стадии разработки, так как на ранних этапах архитектура ещё активно изменяется.
- Настройка CI/CD для стабилизированной системы позволяет ускорить обновления и поддерживать её работоспособность.
##### Цель:
- Снизить трудозатраты на развёртывание и управление системой. Обеспечить стабильность и скорость обновлений за счёт CI/CD и мониторинга.
##### Временные промежутки:
- 2-3 недели
#### 8. **Оптимизация и масштабирование**
##### Делаем:
- Оптимизация кэша для OAuth токенов (улучшение работы с Redis).
- Подключение новых OAuth провайдеров.
- Улучшение производительности базы данных.
- Горизонтальное масштабирование для повышения доступности.
##### Почему:
- Оптимизация проводится после того, как все основные элементы системы протестированы и работают стабильно.
- Это позволяет понять узкие места и целенаправленно работать над их устранением.
##### Цель:
- Улучшить производительность системы, устранив выявленные узкие места. Обеспечить возможность обработки большего количества запросов и подключения новых провайдеров OAuth.
##### Временные промежутки:
- 1-2 недели
#### 9. **Финальная проверка и выпуск**
##### Делаем:
- Финальное тестирование системы.
- Развёртывание на production-окружении.
- Настройка процессов поддержки и обновления системы.
##### Почему:
- Завершающий этап проводится на полностью собранной системе, чтобы убедиться в готовности к использованию.
##### Цель:
- Подготовить систему к использованию в продакшене. Убедиться, что она полностью соответствует требованиям пользователей и работает без сбоев.
##### Временные промежутки:
- 1-2 недели

![Diagram_Gant](Diagram_Gant.png)

***
### Возможные параллельные задачи:

1. **Этап 1 (Создание и тестирование первых сервисов)**:
    
    - Разделить разработку первых трёх микросервисов между программистами. Например, один работает над **User Management**, другой над **Project Management**, третий над **OAuth Configuration**.
    - Это обеспечит независимую разработку компонентов, которые потом можно интегрировать.
2. **Этап 2 (Интеграция баз данных)**:
    
    - Один программист занимается настройкой баз данных (PostgreSQL и Redis).
    - Другие начинают писать тестовые сценарии взаимодействия с базами данных для своих сервисов.
3. **Этап 3 (Добавление Gateway)**:
    
    - Один программист разрабатывает Gateway.
    - Другие тестируют взаимодействие своих сервисов через Gateway, включая начальную конфигурацию API маршрутов.
4. **Этап 4 (Разработка Auth Service)**:
    
    - Один программист разрабатывает Auth Service.
    - Другие начинают настройку окружения для интеграции всех сервисов через Gateway, что позволит ускорить тестирование.
5. **Этап 5 (Создание Web Application)**:
    
    - Один программист занимается разработкой фронтенда.
    - Другие работают над улучшением взаимодействия Auth Service с другими микросервисами.
6. **Этап 6 (Тестирование взаимодействия системы)**:
    
    - Здесь могут работать все одновременно, распределив тестовые сценарии. Например, один тестирует взаимодействие через Gateway, другой — производительность сервисов, третий — безопасность.
7. **Этап 7 (Автоматизация с DevOps)**:
    
    - Один занимается настройкой CI/CD.
    - Другие продолжают искать и исправлять баги на основе первых автоматизированных тестов.
8. **Этап 8 (Оптимизация и масштабирование)**:
    
    - Здесь работа может быть параллельной: один улучшает производительность баз данных, второй оптимизирует микросервисы, третий работает с автоскейлингом в Kubernetes.
9. **Этап 9 (Финальная проверка и выпуск)**:
    
    - Все работают совместно, проверяя разные аспекты системы: пользовательский интерфейс, API, безопасность, производительность.
