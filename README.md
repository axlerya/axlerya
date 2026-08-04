<h1 align="center">Александр Рябов</h1>

<p align="center">
  <b>Backend / AI Engineer</b><br>
  Python · FastAPI · LLM-оркестрация · событийные системы
</p>

<p align="center">
  <a href="https://t.me/axlerya"><img src="https://img.shields.io/badge/Telegram-000?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram"></a>
  <a href="mailto:alexander.ryabov.002@gmail.com"><img src="https://img.shields.io/badge/Email-000?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
</p>

---

Три года в коммерческой разработке на стыке backend и AI. Собираю асинхронные
сервисы на FastAPI и событийные системы на Kafka и RabbitMQ, строю LLM-оркестрацию
на LangGraph и LangChain, RAG и векторный поиск. Веду сервис целиком: от доменной
модели и контрактов API до rolling-деплоя в Docker Swarm.

Сейчас Backend / AI Engineer в [Nexorium](https://nexorium.ru/). Параллельно —
магистратура НИЯУ МИФИ, науки о данных и искусственный интеллект.

## Стек

| | |
| --- | --- |
| **Язык и фреймворки** | ![Python](https://img.shields.io/badge/Python-000?style=for-the-badge&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-000?style=for-the-badge&logo=fastapi&logoColor=white) ![Django REST](https://img.shields.io/badge/Django_REST-000?style=for-the-badge&logo=django&logoColor=white) ![Pydantic](https://img.shields.io/badge/Pydantic-000?style=for-the-badge&logo=pydantic&logoColor=white) ![Celery](https://img.shields.io/badge/Celery-000?style=for-the-badge&logo=celery&logoColor=white) ![gRPC](https://img.shields.io/badge/gRPC-000?style=for-the-badge) |
| **AI / LLM** | ![LangGraph](https://img.shields.io/badge/LangGraph-000?style=for-the-badge) ![LangChain](https://img.shields.io/badge/LangChain-000?style=for-the-badge&logo=langchain&logoColor=white) ![RAG](https://img.shields.io/badge/RAG-000?style=for-the-badge) ![Qdrant](https://img.shields.io/badge/Qdrant-000?style=for-the-badge&logo=qdrant&logoColor=white) ![Milvus](https://img.shields.io/badge/Milvus-000?style=for-the-badge&logo=milvus&logoColor=white) ![OpenAI](https://img.shields.io/badge/OpenAI-000?style=for-the-badge) |
| **Данные и очереди** | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-000?style=for-the-badge&logo=postgresql&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-000?style=for-the-badge&logo=redis&logoColor=white) ![Kafka](https://img.shields.io/badge/Kafka-000?style=for-the-badge&logo=apachekafka&logoColor=white) ![RabbitMQ](https://img.shields.io/badge/RabbitMQ-000?style=for-the-badge&logo=rabbitmq&logoColor=white) ![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-000?style=for-the-badge&logo=sqlalchemy&logoColor=white) ![MinIO](https://img.shields.io/badge/S3_/_MinIO-000?style=for-the-badge&logo=minio&logoColor=white) |
| **Инфраструктура** | ![Docker](https://img.shields.io/badge/Docker-000?style=for-the-badge&logo=docker&logoColor=white) ![Docker Swarm](https://img.shields.io/badge/Swarm-000?style=for-the-badge&logo=docker&logoColor=white) ![Traefik](https://img.shields.io/badge/Traefik-000?style=for-the-badge&logo=traefikproxy&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-000?style=for-the-badge&logo=githubactions&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-000?style=for-the-badge&logo=grafana&logoColor=white) ![Prometheus](https://img.shields.io/badge/Prometheus-000?style=for-the-badge&logo=prometheus&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-000?style=for-the-badge&logo=linux&logoColor=white) |

## Проекты

### 🔎 [product-research-platform](https://github.com/axlerya/product-research-platform)

ИИ-ассистент для исследования товаров: отвечает на вопросы о каталоге, ищет
рыночную информацию и детерминированно считает маржинальность. Каждый факт в
ответе снабжён ссылкой на источник, а число маржи — идентификатором среза, по
которому результат воспроизводится в каталоге, так что модель ничего не
выдумывает.

Четыре микросервиса связаны только событиями. Каталог публикует изменения через
outbox, индекс догоняет их сам — ре-индекс руками не нужен. Если реранкер
отвалился, ответ всё равно придёт: в нём появятся `degradations` и пониженная
`confidence`. Правило зависимостей Clean Architecture проверяет `import-linter`,
сквозные тесты гоняют платформу целиком на реальных Qdrant и RabbitMQ.

`FastAPI` · `LangChain` · `Qdrant` · `RabbitMQ` · `gRPC` · `PostgreSQL` · `Clean Architecture`

### 🤖 [llm-consult-microservices](https://github.com/axlerya/llm-consult-microservices)

Два независимых сервиса: Auth на FastAPI выпускает JWT, Telegram-бот принимает
вопросы и отдаёт их в очередь. Celery-воркер ходит в LLM и возвращает ответ, не
блокируя бота.

Границы держатся строго: JWT создаётся только в Auth, бот знает лишь как
проверить подпись, и в чужую базу не лезет. 141 тест проходит без PostgreSQL,
Redis и Telegram — на in-memory репозиториях и `fakeredis`.

`FastAPI` · `JWT` · `aiogram` · `Celery` · `RabbitMQ` · `Redis` · `PostgreSQL`

### 📊 [human_activity_clustering](https://github.com/axlerya/human_activity_clustering)

Безразметочная кластеризация физической активности по трём IMU-модулям.
Активность видна не в одном измерении, а во временном паттерне, поэтому
кластеризация идёт по окнам в 64 строки, а метки потом переносятся на все
534 601 строку.

**16 место на Kaggle**, score 0.69634.

`scikit-learn` · `MiniBatchKMeans` · `PCA` · `feature engineering` · `pandas`

### 📡 [signal_types_classification](https://github.com/axlerya/signal_types_classification)

Разделение сигналов сцинтилляционного детектора на физические типы без
размеченных ответов. Ключ к разделению нашёлся не в амплитуде, а в форме хвоста
импульса после максимума — на нём и построено финальное решение.

**Public score 0.84083** на Kaggle.

`scikit-learn` · `KMeans` · `PCA` · `unsupervised learning` · `numpy`

## Чем занимаюсь в продакшене

Рабочий код лежит в приватных репозиториях, поэтому коротко о задачах.

**Nexorium** — платформа расчёта мультимодальных перевозок.
Построил AI-оркестрацию на LangGraph: stateful-граф с узлами-инструментами
превращает свободный запрос пользователя в структурированный расчёт — парсинг
параметров, валидация, сборка маршрута и тарификация с ветвлением по условиям.
Спроектировал доменную модель составных маршрутов (плечи, перевалки, тарифы,
сроки) и REST API на FastAPI, разбил систему на четыре микросервиса на Kafka.
Настроил CI/CD в GitHub Actions и держу кластер Docker Swarm с rolling-обновлениями
и маршрутизацией через Traefik.

**FaceX** — продуктовые и внутренние сервисы.
Встроил в приложение для паломников AI-ассистента на LLM и RAG: векторный поиск
по справочному контенту и оркестрация промптов через LangChain. Развернул локально
open-source модель DeepSeek-R1-Distill-Qwen-32B. Собрал микросервисный backend
распознавания лиц: по одному селфи он находит все фото человека среди репортажей
портала GEOMETRIA.ru — детекция, эмбеддинги, векторный поиск, асинхронная
индексация и хранение в S3. Оптимизировал запросы в PostgreSQL: разбор через
`EXPLAIN`, индексы, устранение N+1. Поддерживал Docker Swarm и мониторинг на
Grafana, Prometheus и Loki.

## Связаться

Открыт к предложениям по позициям **Backend Developer** и **AI / LLM Engineer**.

- Telegram — [@axlerya](https://t.me/axlerya)
- Почта — [alexander.ryabov.002@gmail.com](mailto:alexander.ryabov.002@gmail.com)
