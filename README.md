# Полезные команды для работы с Proxmox

1. Прокидываем хостовую директорию в lxc контейнер:
pct set lxcid -mp0 /path/to,mp=/path/to

lxcid - это id lxc контейнера
mp0 - точка монтирования, может быть от 0 до 7
/path/to - хостовой путь до директории которую нужно закинуть в контейнер
mp=/path/to - путь в самом lxc контейнере, куда закинется хостовая директория

Таким образом готовая команда будет иметь вид pct set 100 -mp0 /home/External,mp=/home/External

P.S: Для взаимодействия с файлами (r/w) в прокинутой директории из контейнера необходимо чтобы контейнер был привелигерованный.

2. Прокидываение физического накопителя целиком (например съемный жесткий диск) в VM: 

qm set 101 -sataN /dev/disk/by-id/usbid

101 - id виртуальной машины
sataN - sata контроллер с указанием его номера
/dev/disk/by-id/ - этот путь является обязательным и путь ведет прямиком к устройству
usbid - тут должен быть usbid устройства, которое хочешь прокинуть. Чтобы узнать его можно воспользоваться командой после чего вставить вместо usbid

Полный и правильный вид команды будет иметь вид qm set 111 -sata1 /dev/disk/by-id/usb-_USB_FLASH_DRIVE_XXXXXXXXXXXXXXX-0:0-part1

3. Telegram Webhook URL для уведомлений в телеграмм группу:

https://api.telegram.org/bot{{ secrets.BOT_TOKEN }}/sendMessage?chat_id={{ secrets.CHAT_ID }}&message_thread_id={{ secrets.THREAD_ID }}&text={{ url-encode "Proxmox Notification" }}%0A%0ATitle:+{{ url-encode title }}%0AMessage:+{{ url-encode message }}%0ASeverity:+{{ url-encode severity }}%0ATime:+{{ timestamp }}

BOT_TOKEN - токен телеграмм бота
CHAT_ID - айди чатика
THREAD_ID - айди топика в чатике 

Данные переменные необходимо добавить в Secrets раздел и присвоить им соответствующие значения.
Сам URL необходимо вставить в поле Method/URL (Метод POST)

![image](https://github.com/user-attachments/assets/421cfef4-6079-4f41-ae7d-7d74cfcd3f59)

