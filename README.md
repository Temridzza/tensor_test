# Тестовое задание: Foreman и Ansible

## 1. Развёртывание Foreman

Foreman развёрнут в виртуальной машине и доступен через веб-интерфейс.

**Скриншот:** главная страница Foreman или страница с версией
установленной системы.

![Foreman](screenshots/01-foreman.png)

------------------------------------------------------------------------

## 2. Регистрация управляемого хоста

В Foreman зарегистрирован хост `server2`, который используется для
проверки конфигурации и выполнения Ansible-роли.

**Скриншот:** страница `Hosts → All Hosts` или карточка хоста `server2`,
где видны его имя и основные параметры.

![Managed host server2](screenshots/02-managed-host.png)

------------------------------------------------------------------------

## 3. Host Group и Provisioning Template для настройки NTP

Создана Host Group для назначения общих параметров хостам. Для группы
необходимо назначить Provisioning Template, который выполняет настройку
NTP при установке операционной системы.

**Скриншот 1:** страница Host Group с её настройками.

![Host Group](screenshots/03-hostgroup.png)

**Скриншот 2:** Provisioning Template с фрагментом, который настраивает
NTP, и/или страница Host Group, где этот шаблон назначен.

![NTP provisioning template](screenshots/04-ntp-template.png)

> Перед сдачей убедитесь, что шаблон действительно настроен на
> применение при установке ОС и назначен нужной Host Group. Само наличие
> Host Group не подтверждает выполнение этого требования.

------------------------------------------------------------------------

## 4. Интеграция Ansible и применение роли через Host Group

В Foreman настроена интеграция с Ansible. Создана роль
`disable_root_ssh`, которая запрещает вход пользователя `root` по SSH, и
роль назначена Host Group.

**Скриншот 1:** страница роли `disable_root_ssh` или её задачи, где
задаётся `PermitRootLogin no`.

![Ansible role](screenshots/05-ansible-role.png)

**Скриншот 2:** Host Group с назначенной ролью `disable_root_ssh`.

![Role assigned to Host Group](screenshots/06-role-assigned.png)

**Скриншот 3:** успешное выполнение задания Ansible для хоста `server2`
в Foreman.

![Successful Ansible job](screenshots/07-ansible-success.png)

**Скриншот 4 (дополнительно):** проверка результата на `server2`:

``` bash
sudo sshd -T | grep permitrootlogin
```

Ожидаемый вывод:

``` text
permitrootlogin no
```

![SSH root login verification](screenshots/08-root-ssh-check.png)

------------------------------------------------------------------------
