# 🧩 ExternalPluginsLoader for Vencord

**ExternalPluginsLoader** — это пользовательский плагин для [Vencord](https://github.com), который добавляет систему загрузки внешних `.js`-плагинов на лету (по аналогии с `Local Themes` и `QuickCSS`), без необходимости каждый раз пересобирать Vencord.

👤 **Автор:** `𝓈𝓌ℯℯ𝓉𝓎 𝓁𝒾𝓉𝓉𝓁ℯ 𝒷𝒶𝒷𝓎` (`@myloveitskirill` / ID: `1399448306194714786`)

---

## ✨ Возможности

- **Отдельная вкладка `External Plugins` в настройках Vencord** — интерфейс в стиле *Local Themes* с карточками модов, описанием, именем автора и переключателями `Вкл / Выкл`.
- **Автоматическое создание папки** — плагин сам находит и создаёт директорию `AppData\Roaming\Vencord\plugins` (или любую другую указанную в настройках).
- **Встроенный редактор `QuickPlugin`** — пиши, тестируй и запускай свой JavaScript-код прямо внутри Discord по кнопке **Edit QuickPlugin** -> **Save & Run QuickPlugin**.
- **Горячая перезагрузка** — добавляй новые `.js` файлы в папку и подгружай их нажатием **Load missing Plugins** без перезапуска клиента.

---

## 📦 Установка (как `userplugin`)

> ⚠️ Плагин использует `native.ts` (IPC-мост главного процесса Electron) для чтения папки с плагинами, поэтому требует полной сборки Vencord.

1. Склонируйте исходники Vencord (если ещё не скачаны):
   ```bash
   git clone https://github.com.git
   cd Vencord
   ```
2. Скопируйте папку `externalPluginsLoader` (с файлами `index.tsx` и `native.ts`) в директорию:
   ```text
   src/userplugins/externalPluginsLoader/
   ```
3. Установите зависимости, соберите Vencord и выполните инжект:
   ```bash
   pnpm install
   pnpm build
   pnpm inject
   ```
4. **Полностью перезапустите Discord** (выйдите через значок в трее) и включите **ExternalPluginsLoader** в разделе **Настройки → Vencord → Plugins**.

---

## 🛠 Как создавать внешние `.js` плагины

Откройте **Настройки → Vencord → External Plugins**, нажмите **Open Plugins Folder** и создайте любой `.js` файл (например, `MyPlugin.js`).

### Базовый шаблон плагина:

```javascript
module.exports = {
    name: "MyCustomPlugin",
    author: "YourNickname",
    description: "Описание работы моего плагина",

    start() {
        // Код, который выполнится при включении тумблера или запуске Discord
        console.log("[MyCustomPlugin] Запущен!", Vencord);
    },

    stop() {
        // Очистка стилей, кнопок и слушателей событий при выключении тумблера
        console.log("[MyCustomPlugin] Выключен!");
    }
};
```

После сохранения файла нажмите **Load missing Plugins** во вкладке *External Plugins*, чтобы карточка появилась в списке.

---

## ⚠️ Дисклеймер

Плагин предназначен исключительно для локальной кастомизации клиента и запуска собственных утилит. Используйте только проверенные `.js` скрипты из надёжных источников, так как внешний код имеет доступ к среде выполнения клиента.
