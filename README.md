# Ansible HW 04 — работа с roles

Домашнее задание к занятию 4 «Работа с roles».

## Состав

- `site.yml` — playbook, использующий роли.
- `requirements.yml` — список ролей (ClickHouse + Vector + Lighthouse).
- `prod.yml` — inventory.
- `ansible.cfg` — конфигурация Ansible.

## Роли

- [vector-role](https://github.com/michaelkoch51/vector-role) — установка Vector.
- [lighthouse-role](https://github.com/michaelkoch51/lighthouse-role) — развёртывание Lighthouse + nginx.
- [clickhouse](https://github.com/AlexeySetevoi/ansible-clickhouse) — внешняя роль (1.13).

## Как запустить

1. Скачать архив Vector и положить в files/:

   curl -L -o files/vector-0.34.1-x86_64-unknown-linux-gnu.tar.gz https://packages.timber.io/vector/0.34.1/vector-0.34.1-x86_64-unknown-linux-gnu.tar.gz

2. Скачать архив Lighthouse и положить в files/:

   curl -L -o files/lighthouse-master.zip https://github.com/VKCOM/lighthouse/archive/refs/heads/master.zip

3. Установить роли:

   ansible-galaxy role install -r requirements.yml -p roles

4. Запустить playbook:

   ansible-playbook -i prod.yml site.yml
