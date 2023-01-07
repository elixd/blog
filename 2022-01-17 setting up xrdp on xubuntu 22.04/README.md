# Активировать русскую раскладку при подключении и переродключении по RDP
'sudo nano /etc/xrdp/xrdp_keyboard.ini'

'''
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
'''

# Избавиться от запроса паролья при каждом запуске браузера
'sudo nano /etc/pam.d/xrdp-sesman'

Заменить на:
'''
#%PAM-1.0
auth    requisite       pam_nologin.so
auth    sufficient      pam_succeed_if.so user ingroup nopasswdlogin
@include common-auth
auth    optional        pam_gnome_keyring.so
auth    optional        pam_kwallet.so
@include common-account
session [success=ok ignore=ignore module_unknown=ignore default=bad] pam_selinux.so close
session required        pam_limits.so
@include common-session
session [success=ok ignore=ignore module_unknown=ignore default=bad] pam_selinux.so open
session optional        pam_gnome_keyring.so auto_start
session optional        pam_kwallet.so auto_start
session required        pam_env.so readenv=1
session required        pam_env.so readenv=1 user_readenv=1 envfile=/etc/default/locale
@include common-password
'''
