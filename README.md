[app]

# Название вашего приложения
title = BitcoinWalletApp

# Пакетное имя приложения (должно быть уникальным)
package.name = bitcoin_wallet_app

# Версия вашего приложения
version = 0.1

# Используемые пакеты Python и их версии
requirements = kivy

# Конфигурация сборки для Android
# (эти параметры могут варьироваться в зависимости от ваших требований)
[buildozer]

# Установите архитектуру для сборки (armeabi-v7a, arm64-v8a, x86, x86_64)
# Укажите только одну архитектуру для более быстрой сборки
# android.arch = armeabi-v7a

# Путь к SDK Android (установленный через Android Studio)
android.sdk = /путь/к/sdk

# Путь к NDK (установленный через Android Studio)
android.ndk = /путь/к/ndk

# Дополнительные инструменты для сборки
# (если они необходимы, например, JDK, ANT, Apache ANT)
# android.gradle_dependencies = 'com.android.support:support-core-utils:28.0.0'

# Список разрешений приложения (если они необходимы)
# android.permissions = INTERNET

# Путь к исходным файлам проекта (где находится ваш файл main.py)
source.dir = .

# Пусть к исходным файлам проекта (где находятся ваши .py файлы)
source.include_exts = py

# Пусть к исходным файлам проекта (где находятся ваши .kv файлы)
# Поместите ваши файлы .kv в папку с исходными файлами проекта
# или укажите их здесь, если они находятся в другом месте
# source.include_exts = py,kv

# Настройки сборки для Android
[app]

# Настройки сборки для Android
# (эти параметры могут варьироваться в зависимости от ваших требований)
android.permissions = INTERNET

# Имя файла иконки вашего приложения
# (если он находится в папке с исходными файлами проекта)
# android.icon = icon.png

# Тема вашего приложения
# android.theme = @android:style/Theme.NoTitleBar

# Архитектура сборки (по умолчанию armeabi-v7a)
# android.arch = armeabi-v7a
