#!/bin/bash

# Запрашиваем размер свопа у пользователя
read -p "Введите размер свопа (например, 4G): " SWAP_SIZE

# Шаг 1: Создание своп-файла
echo "Создание своп-файла размером $SWAP_SIZE..."
sudo fallocate -l $SWAP_SIZE /swapfile || sudo dd if=/dev/zero of=/swapfile bs=1G count=${SWAP_SIZE%G}

# Шаг 2: Установка правильных разрешений
echo "Установка прав доступа для своп-файла..."
sudo chmod 600 /swapfile

# Шаг 3: Инициализация свопа
echo "Инициализация свопа..."
sudo mkswap /swapfile

# Шаг 4: Активирование свопа
echo "Активирование своп-файла..."
sudo swapon /swapfile

# Шаг 5: Проверка состояния свопа
echo "Проверка состояния свопа..."
sudo swapon --show
free -h

# Шаг 6: Автоматическое подключение свопа при загрузке
echo "Добавление своп-файла в /etc/fstab для автоматического подключения при загрузке..."
echo "/swapfile none swap sw 0 0" | sudo tee -a /etc/fstab

# Шаг 7: Настройка параметров свопа (по желанию)
echo "Настройка параметров swappiness..."
sudo sysctl vm.swappiness=10
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf

echo "Скрипт выполнен успешно. Своп-файл создан и настроен!"

htop
