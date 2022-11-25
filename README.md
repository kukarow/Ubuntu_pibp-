# Ubuntu 22.04 LTS «Jammy Jellyfish» post install build pack 
Минимальная сборка пакетов которые необходимо поставить после установки ОС.

Все что нужно собрано в одном скрипте, для минимизации гемора.

Содержимое скрипта имеет следующий вид:

```bash
!/bin/bash


echo -n "Установить пакет кодеков мультимедия ubuntu-restricted-extras ? "
read EXTRAS
echo -n "Установить пакеты nautilus-admin exe-thumbnailer ? "
read NAUTILUS
echo -n "Решить проблему с отображением кириллицы в текстовом редакторе Gedit ? " 
read GEDIT
echo -n "Установить дополнительную поддержку архиваторов ? "
read RAR
echo -n "Установить дополнительное ПО: GNOME Tweaks, Synaptic, Gdebi, Gnome-tweaks, Chrome-gnome-shell, Flameshot и Peek ? " 
read TWEAKS
echo -n "Установить Bashtop, htop - консольная утилита, аналог Top, для проверки использования ресурсов ? " 
read BASHTOP
echo -n "Для обладателей видеокарт Nvidia. Выбрать версию видеодрайвера можно в Программы и обновления. Подключить репозиторий ppa:graphics-drivers? " 
read NVIDIA
echo -n "Включить поддержку приложений Flatpak / Flathub? " 
read FLATPAK
echo -n "Установка МС? " 
read MC
###
echo -n "- установка чистильщика системы Bleachbit:? " 
read Bleachbit
###
echo -n "- Установка Stacer - мониторинг и оптимизация системы? " 
read Stacer
#################################################################
echo -n "- Установка PHP 8.1? " 
read PHP8
#php8.1-cli- интерпретатор команд, полезный для тестирования сценариев PHP из оболочки или выполнения общих задач сценариев оболочки.
#php8.1-common- документация, примеры и общие модули для PHP
#php8.1-mysql- для работы с базами данных MySQL
#php8.1-zip- для работы со сжатыми файлами
#php8.1-gd- для работы с изображениями
#php8.1-mbstring- используется для управления строками, отличными от ASCII
#php8.1-curl- позволяет делать HTTP-запросы в PHP
#php8.1-xml- для работы с XML-данными
#php8.1-bcmath- используется при работе с прецизионными поплавками
###
echo -n "Установка Docker на Ubuntu ? " 
read Docker
###
echo -n "Установка Docker Compose 1.21.0 ? " 
read DockerCompose

if [[ "$EXTRAS" == "yes" || "$EXTRAS" == "y" || "$EXTRAS" == "да" || "$EXTRAS" == "д" || "$EXTRAS" == "Д" ]]
then 
  sudo apt install ubuntu-restricted-extras  -y
fi
#
if [[ "$NAUTILUS" == "yes" || "$NAUTILUS" == "y" || "$NAUTILUS" == "да" || "$NAUTILUS" == "д" || "$NAUTILUS" == "Д" ]]
then
  sudo apt install nautilus-admin exe-thumbnailer -y
  nautilus -q
fi
#
if [[ "$GEDIT" == "yes" || "$GEDIT" == "y" || "$GEDIT" == "да" || "$GEDIT" == "д" || "$GEDIT" == "Д" ]]
then
  gsettings set org.gnome.gedit.preferences.encodings candidate-encodings "['UTF-8', 'WINDOWS-1251', 'KOI8-R', 'CURRENT', 'ISO-8859-15', 'UTF-16']"
fi
#
if [[ "$RAR" == "yes" || "$RAR" == "y" || "$RAR" == "да" || "$RAR" == "д" || "$RAR" == "Д" ]]
then
  sudo apt install p7zip-rar rar unrar unace arj cabextract -y  
echo "Установлены пакеты p7zip-rar rar unrar unace arj cabextract "    
fi
#
if [[ "$TWEAKS" == "yes" || "$TWEAKS" == "y" || "$TWEAKS" == "да" || "$TWEAKS" == "д" || "$TWEAKS" == "Д" ]]
then
  sudo apt install synaptic gdebi chrome-gnome-shell gnome-tweaks flameshot peek -y
fi
#
if [[ "$BASHTOP" == "yes" || "$BASHTOP" == "y" || "$BASHTOP" == "да" || "$BASHTOP" == "д" || "$BASHTOP" == "Д" ]]
then
  sudo apt install bashtop htop -y
fi
#
if [[ "$NVIDIA" == "yes" || "$NVIDIA" == "y" || "$NVIDIA" == "да" || "$NVIDIA" == "д" || "$NVIDIA" == "Д" ]]
then
  sudo add-apt-repository ppa:graphics-drivers/ppa -y && sudo dpkg --add-architecture i386 && sudo apt update
fi
#
if [[ "$FLATPAK" == "yes" || "$FLATPAK" == "y" || "$FLATPAK" == "да" || "$FLATPAK" == "д" || "$FLATPAK" == "Д" ]]
then
  sudo apt install flatpak gnome-software-plugin-flatpak gnome-software -y && flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
fi
#
if [[ "$MC" == "yes" || "$MC" == "y" || "$MC" == "да" || "$MC" == "д" || "$MC" == "Д" ]]
then 
  sudo apt install mc  -y
fi
#
if [[ "$Bleachbit" == "yes" || "$Bleachbit" == "y" || "$Bleachbit" == "да" || "$Bleachbit" == "д" || "$Bleachbit" == "Д" ]]
then 
  sudo apt install bleachbit -y
fi
#
if [[ "$Stacer" == "yes" || "$Stacer" == "y" || "$Stacer" == "да" || "$Stacer" == "д" || "$Stacer" == "Д" ]]
then 
  sudo apt install stacer -y
fi
##################################################################
if [[ "$PHP8" == "yes" || "$PHP8" == "y" || "$PHP8" == "да" || "$PHP8" == "д" || "$PHP8" == "Д" ]]
then 
  sudo apt update -y
  sudo apt install --no-install-recommends php8.1 -y
  #Проверьте информацию о версии PHP с помощью следующей команды:
  php -v
  sudo apt-get install -y php8.1-cli php8.1-common php8.1-mysql php8.1-zip php8.1-gd php8.1-mbstring php8.1-curl php8.1-xml php8.1-bcmath
  php -m
fi
####################################################################
if [[ "$Docker" == "yes" || "$Docker" == "y" || "$Docker" == "да" || "$Docker" == "д" || "$Docker" == "Д" ]]
then 
  sudo apt update -y
  sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  sudo apt update && sudo apt install docker-ce
  sudo groupadd docker
  sudo usermod -aG docker $USER
  docker run hello-world
fi
#####################################################################
if [[ "$DockerCompose" == "yes" || "$DockerCompose" == "y" || "$DockerCompose" == "да" || "$DockerCompose" == "д" || "$DockerCompose" == "Д" ]]
then 
# Качаем
  sudo curl -L https://github.com/docker/compose/releases/download/1.21.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
# Делаем метку выполняемого файла
  sudo chmod +x /usr/local/bin/docker-compose
# Проверяем
  docker-compose --version
fi

echo "Текстовая статья по настройке Ubuntu 22.04 доступна на github :) ! "
```
Возможно будут вопросы по блокам - php8. Docker. DockerComposer. ()

Создадим скрипт - 
```
nano script.sh

```

Переместим вышеописанное содержимое в наш ново созданный скрипт. Можно без поля - !/bin/bash
И сохраним наш скрипт.

Но лучше будет если Вы скачаете рядом лежащий файл. 

Так как он чаще будет обновлятся.

***
# Варианты запуска скрипта

Дадим нашему скрипту права на исполнение (устанавливаем флаг на исполнение).
```
chmod ugo+x script.sh
```
Запустим наш скрипт для теста:
```
./script.sh
```
или

Нажимаем правой кнопкой мыши по файлу скрипта > Свойства > поставьте галочку на опцию Разрешить исполнять как программу.

Запустите скрипт в терминале, открытом в папке с файлом скрипта или перетащите файл скрипта в терминал и нажмите клавишу Enter.


