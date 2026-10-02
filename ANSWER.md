# Домашнее задание к занятию 4 «Работа с roles»

## Репозитории

1. **Роль Vector:** https://github.com/michaelkoch51/vector-role
2. **Роль Lighthouse:** https://github.com/michaelkoch51/lighthouse-role
3. **Playbook:** https://github.com/michaelkoch51/work-with-roles

## Что сделано

- Созданы две собственные роли: `vector-role` и `lighthouse-role`.
  Каждая размечена тегом `v1.0.0`.
- Роль `vector-role` устанавливает Vector из локального архива,
  который копируется с control-node — работает без интернета
  на целевом хосте (актуально из-за инфраструктурной проблемы с NAT).
- Роль `lighthouse-role` разворачивает Lighthouse + nginx,
  архив также копируется с control-node.
- Внешняя роль ClickHouse подключается из `AlexeySetevoi/ansible-clickhouse`
  (версия 1.13).
- Написан `requirements.yml`, объединяющий все три роли.
- Playbook `site.yml` переведён на использование ролей.
- Проверка: `ansible-playbook -i prod.yml site.yml --syntax-check`
  проходит без ошибок.

## Структура репозитория с playbook

- `site.yml` — playbook.
- `requirements.yml` — список ролей.
- `prod.yml` — inventory.
- `ansible.cfg` — конфигурация Ansible.

## Особенности

Из-за инфраструктурной проблемы (отсутствие исходящего интернета
у одной из ВМ в Yandex Cloud) роль Vector реализована в offline-варианте:
архив `vector-0.34.1-x86_64-unknown-linux-gnu.tar.gz` заранее скачивается
на control-node и копируется на целевой хост через SSH. Это позволило
обойти ограничение и сохранить идемпотентность роли.

## Как воспроизвести

1. Скопировать в `files/` архивы (см. `README.md`).
2. `ansible-galaxy role install -r requirements.yml -p roles`
3. `ansible-playbook -i prod.yml site.yml`
