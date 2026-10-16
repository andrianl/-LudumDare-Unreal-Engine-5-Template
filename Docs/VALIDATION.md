# Перевірка 2026-10-16

Локальний рушій: UE 5.8.1, Linux, source tree `/home/nobarapc/Dev/UnrealEngine`.

- Створення Startup.umap через LevelEditorSubsystem: успішно.
- Повторне завантаження карти: успішно.
- Перевірка значень Forward Shading, SMAA (5), Bloom, Nanite, GI та ray tracing: успішно.
- Перемикання PostProcessQuality і AntiAliasingQuality 0–4: Bloom quality 3;
  SMAA quality 0 на Low і 1 на інших рівнях. Усі assertions пройдені.
- `Tools/package.py --dry-run`: коректна команда Linux Shipping BuildCookRun.
- Фінальний Python commandlet: exit code 0, 0 errors, 3 warnings.
  Попередження стосуються sandbox: network monitoring socket та запису EditorSettings.ini
  у read-only каталог рушія. Попереджень про ACL assets після виправлення немає.
- Перша спроба з типовим Zen DDC не завершилась успішно через недоступний для запису
  глобальний кеш. Повторний запуск використовував локальний файловий DDC у /tmp.

Перевірка виконана з NullRHI. Це не GPU-тест, не cook, не Shipping build і не вимірювання
розміру готової гри. DX11, Vulkan та Metal рендер, FPS і пакування на кожній ОС ще не перевірені.

Для повторення в цьому sandbox до команди з README додайте:
`'-DDC=(Local)' -LocalDataCachePath=/tmp/lowend58-ddc`.
Це локальна опція перевірки, вона не нав'язана проєкту.
