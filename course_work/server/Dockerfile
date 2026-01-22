# Используем Ubuntu как базовый образ
FROM ubuntu:22.04

# Устанавливаем необходимые зависимости
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    libsodium-dev \
    && rm -rf /var/lib/apt/lists/*

# Создаем рабочую директорию
WORKDIR /app

# Копируем исходные файлы сервера
COPY . /app/

# Создаем директорию для сборки
RUN mkdir -p build

# Собираем проект
WORKDIR /app/build
RUN cmake .. && make

# Создаем директорию для данных
RUN mkdir -p /app/data

# Возвращаемся в директорию с данными как рабочую директорию
WORKDIR /app/data

# Открываем порт 8080
EXPOSE 8080

# Запускаем сервер (из директории /app/data, чтобы файлы создавались здесь)
CMD ["/app/build/password_server", "8080"]
