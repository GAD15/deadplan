# DeadPlan

Форк Vikunja для планирования разработки DeadZone. Изменения брендинга внесены 14 октября 2026 года; исходная версия — тег `v2.7.0`. Лицензия и авторство исходного проекта сохранены.

## Исходники и рабочая установка

- Форк: https://github.com/GAD15/deadplan; рабочая ветка `deadplan`, `main` сохраняет исходную ветку upstream.
- Сайт: https://plan.deadzone.space/.
- Интерфейс: `frontend/`, Vue 3 и TypeScript. Устанавливать зависимости через pnpm 11.27.0 с Node.js 24 или новее.
- Сервер: официальный контейнер Vikunja 2.7.0, SQLite. В этой версии форка backend не менялся.
- Готовый frontend nginx читает из `/var/www/deadplan/current`; `/api/` и `/dav/` проксируются в существующий контейнер. Это не требует перезапуска backend или игрового сервера.
- Эксплуатация и резервные копии: `/opt/deadzone-plan/README.md` на хосте. Секреты, БД и вложения в этот репозиторий не добавлять.

## Где менять брендинг

| Область | Исходники |
| --- | --- |
| Экран входа и шапка | `frontend/src/components/home/Logo.vue`, `frontend/src/assets/logo*.svg` |
| Название вкладки | `frontend/index.html`, `frontend/src/helpers/setTitle.ts`, `frontend/src/composables/useTitle.ts` |
| Установленное веб-приложение | Manifest в `frontend/vite.config.ts`, `frontend/public/favicon.ico`, `frontend/public/images/icons/` |
| Тексты интерфейса | `frontend/src/i18n/lang/*.json`; имена ключей, placeholders и технические идентификаторы сохранять |
| Версия и исходники | `frontend/src/version.json`, `frontend/src/views/About.vue` |

Ссылка «При поддержке Vikunja» сохраняет указание исходного проекта. Ссылки на документацию Vikunja относятся к совместимым API и функциям. Названия внешних продуктов Vikunja Cloud/Pro и форматов импорта не переименовывать в технических идентификаторах.

## Сборка и проверка

```bash
cd frontend
pnpm install --frozen-lockfile
pnpm lint:fix
pnpm build
```

Проверять экран входа, шапку, название вкладки, русский и английский интерфейсы, manifest и иконки. Проверить, что вход и чтение доски работают с API 2.7.0. При изменении архитектуры обновлять этот документ и связанную карту DeadZone. Обновление frontend не разрешает миграцию БД, обновление backend или рестарт игровых сервисов.
