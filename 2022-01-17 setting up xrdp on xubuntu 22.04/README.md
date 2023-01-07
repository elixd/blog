# Настройка работы XRPD на Ubuntu 22.04 и XFCE

### Add Keyboar Layout Swithcer to Task Panel
`sudo apt install xfce4-goodies' (этот пакет включает переключалку)
Зайти в настройки панели и добавить переключалку на панель.

### Активировать русскую раскладку при подключении и переродключении по RDP
Source: https://github.com/neutrinolabs/xrdp/issues/337
Alternative: https://sysadminmosaic.ru/xrdp/xrdp#xrdp_keyboardini

`sudo nano /etc/xrdp/xrdp_keyboard.ini`

```
[default_rdp_layouts]
rdp_layout_none=0x00000000
rdp_layout_us=0x00000409
rdp_layout_us_pd=0xa0000409
rdp_layout_ru=0x00000419

[default_layouts_map]
rdp_layout_none=us,ru
rdp_layout_us=us,ru
rdp_layout_us_pd=us,ru
rdp_layout_ru=us,ru

[rdp_keyboard_ru]
keyboard_type=4
keyboard_subtype=1
options=grp:ctrl_shift_toggle
rdp_layouts=default_rdp_layouts
layouts_map=default_layouts_map
```

### Избавиться от запроса паролья при каждом запуске браузера
Source: https://askubuntu.com/questions/1240905/how-do-i-automatically-unlock-login-keyring-when-logging-into-ubuntu-20-04
Alternative: https://wiki.archlinux.org/title/xrdp


`sudo nano /etc/pam.d/xrdp-sesman`

Заменить на:
```
#%PAM-1.0
# Это вариант конфига решает с проблемы запросом пароля при запуске Chrome
# Кроме того, это едиснтвенный конфиг который я нашел, при котором не слетает русский язык в интерфейсте
# В других вариантах по какой-то причине язык интерфейса XFCE переходил на анлийский
auth requisite pam_nologin.so
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin
@include common-auth
auth optional pam_gnome_keyring.so
auth optional pam_kwallet.so
@include common-account
session [success=ok ignore=ignore module_unknown=ignore default=bad] pam_selinux.so close
session required pam_limits.so
@include common-session
session [success=ok ignore=ignore module_unknown=ignore default=bad] pam_selinux.so open
session optional pam_gnome_keyring.so auto_start
session optional pam_kwallet.so auto_start
session required pam_env.so readenv=1
session required pam_env.so readenv=1 user_readenv=1 envfile=/etc/default/locale
@include common-password
```

### Software
`sudo apt install gnome-terminal` потом зайти в "программы по умолчанию" и выбрать его по умолчанию
`sudo apt-get remove xscreensaver`
- https://github.com/hakandundar34coding/system-monitoring-center/blob/master/README.md

### Внешний вид
Icons: Papirus-Light
Theme (Style): Orchis-Light-Compact
Fonts: Roboto Regular, Roboto Mono Regular

### Решений ошибки light locker при входе в системе
Solution: `sudo mv /etc/xdg/autostart/light-locker.desktop /etc/xdg/autostart/light-locker.desktop.bak`
More info: https://bugs.launchpad.net/ubuntu/+source/light-locker/+bug/1745259

# Links
- https://sevo44.ru/xrdp-terminalnyj-server-linux/
- https://sysadminmosaic.ru/xrdp/xrdp
- [Youtube: A Modern Linux Graphical TERMINAL SERVER | Complete Guide for Remote Access | Any Device, Many Users
](https://www.youtube.com/watch?v=sAllRma_0xc)
- https://www.apalrd.net/posts/2022/xrdp_intro/

