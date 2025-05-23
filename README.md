# sso - Простой Сервис Аутентификации

Этот репозиторий содержит простую реализацию Сервиса Аутентификации (SSO) с использованием gRPC и Go. Он демонстрирует основные функции регистрации пользователей, входа в систему и аутентификации, установки прав администратора.

## Функциональность

*   **gRPC API:** Определяет gRPC сервис для регистрации пользователей, входа в систему и аутентификации, установки прав администратора.
*   **Аутентификация пользователей:** Предоставляет механизмы для проверки учетных данных пользователя.
*   **JWT:** Использует JWT для безопасной аутентификации на основе токенов.
*   **SQLite Database:** Хранит информацию о пользователях в легковесной базе данных SQLite.
*   **Конфигурация:** Использует YAML файлы для настройки параметров.
*   **Тестирование:** Включает полный набор тестов для проверки функциональности.

## Архитектура

Проект имеет простую архитектуру со следующими ключевыми компонентами:

*   **`internal/services/auth`:** Реализует gRPC сервер для сервиса аутентификации. Он обрабатывает запросы на регистрацию, вход в систему и проверку токенов.
*   **`internal/config`:** Загружает и управляет конфигурацией приложения из YAML файлов.
*   **`internal/lib/jwt`:** Предоставляет утилиты для генерации и проверки JWT токенов.
*   **`migrations`:** Миграции БД.
*   **`internal/storage/sqlite`:** Инкапсулирует логику взаимодействия с базой данных SQLite.
*   **`tests`:** Содержит функциональные тесты для сервиса.

## Предварительные требования

*   **Go:** Go 1.22 или выше.
*   **Сгенерированный gRPC код:**  Необходимо иметь сгенерированный Go код из proto файлов.  Инструкции по генерации кода можно найти в репозитории `protos`(смотреть в разделе Установка).
*   **SQLite:** Установите библиотеку базы данных SQLite.

## Установка

1.  **Клонируйте репозиторий:**

    ```bash
    git clone https://github.com/sj-shoff/sso.git
    cd sso
    ```

2.  **Установите зависимости:**

    ```bash
    go mod download
    go mod tidy
    ```

3.  **Получите сгенерированный gRPC код:**

    *   Клонируйте репозиторий с proto файлами:
        ```bash
        git clone https://github.com/sj-shoff/protos.git
        ```
    *   Убедитесь, что сгенерированный код доступен в вашем проекте `sso`. Необходимо настроить импорты.

4.  **Скомпилируйте приложение:**

    ```bash
    make run
    ```

4.  **Применение миграций:**

    ```bash
    make migrator
    ```

6.  **Тестирование:**

    ```bash
    make test
    ```

## Конфигурация

Конфигурация приложения загружается из YAML файлов. Файл конфигурации по умолчанию - `config/local.yaml`. Вы можете указать другой файл конфигурации с помощью переменной окружения `CONFIG_PATH`