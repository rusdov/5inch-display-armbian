script.bin - главный конфигурационный файл ядра использующийся при загрузке ОС на платах Orange Pi (и остальных, базирующихся на sunxi). Это скомпилированный бинарный файл, внесение правок в который - невозможно.
Файл создается при помощи утилиты fex2bin из набора sunxi-tools из текстового файла имя_файла.fex

ПРОЦЕДУРА СОЗДАНИЯ SCRIPT.BIN
Первое что нужно сделать - склонировать репозиторий с утилитами. Для этого у Вас должен быть установлен git, если его нет - установите его sudo apt-get update && sudo apt-get install git
Далее клонируем репозиторий sunxi-tools

git clone git://github.com/linux-sunxi/sunxi-tools.git

Для компиляции script.fex в script.bin необходим бинарник fex2bin. Компилируем его и добавляем в /usr/local/bin для удобства использования.

cd sunxi-tools
make fex2bin 
chmod +x fex2bin
sudo ln -s fex2bin /usr/local/bin/

Теперь нам нужен исходник script.fex для нашей модели платы. Самый простой спрособ - это забрать его из архива подготовленного всем известным Loboris здесь и положить этот файл в папку sunxi-tools.
Вносим изменения в файл script.fex (имя как вы поняли может быть любое, например orange_pi_pc.fex) любым удобным для вас способом (это текстовый файл).
Все готово, правки в файл внесены, файл в директории sunxi-tools. Компилим! fex2bin script.fex script.bin
Итоговый файл script.bin поместите в /boot/ раздел на SD карте (он доступен и под Windows если подключить карту памяти через кард-ридер.
ДЕКОМПИЛЯЦИЯ ИЗ SCRIPT.BIN В SCRIPT.FEX
Бывает так, что нужно вернуть обратно из своего script.bin - исходных script.fex. Это утилитой из этого же набора, называется она - bin2fex. Соберем её.

cd sunxi-tools
make bin2fex
chmod +x bin2fex
sudo ln -s bin2fex /usr/local/bin/
Все готово. Декомпилируем простой командой bin2fex script.bin script.fex

Взято с https://piboard.io
