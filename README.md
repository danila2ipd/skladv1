# 🏗️ СтройСклад — Система учёта материалов

<div align="center">

![WPF](https://img.shields.io/badge/WPF-.NET%204.8-blue?style=for-the-badge&logo=windows)
![C#](https://img.shields.io/badge/C%23-7.3-purple?style=for-the-badge&logo=csharp)
![SQL Server](https://img.shields.io/badge/SQL%20Server-Express-red?style=for-the-badge&logo=microsoftsqlserver)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

**Десктопное приложение для автоматизации складского учёта строительной компании**

[📦 Возможности](#-возможности) • [🖥️ Скриншоты](#️-интерфейс) • [🚀 Установка](#-установка) • [🗄️ База данных](#️-база-данных) • [👥 Роли](#-роли-пользователей)

</div>

---

## 📦 Возможности

| Модуль | Описание |
|--------|----------|
| 📊 **Дашборд** | KPI-карточки: остатки, операции, поступления и выдача за месяц |
| 🧱 **Остатки** | Полный список материалов с поиском и статусом запаса |
| 🔄 **Операции** | Журнал всех складских движений с фильтрацией по дате |
| 📋 **Материалы** | Справочник номенклатуры — полный CRUD |
| 🏭 **Поставщики** | Реестр поставщиков с контактными данными |
| 🔔 **Уведомления** | Позиции ниже минимального остатка |
| 📄 **Отчёты** | Генерация Word и Excel (4 типа отчётов) |
| 👤 **Пользователи** | Управление учётными записями и ролями |

---

## 🖥️ Интерфейс

<table>
  <tr>
    <td align="center"><b>🔐 Авторизация</b></td>
    <td align="center"><b>📊 Дашборд</b></td>
  </tr>
  <tr>
    <td>Тёмная тема · SHA-256 · CAPTCHA при регистрации</td>
    <td>6 KPI-карточек · таблица критичных позиций</td>
  </tr>
  <tr>
    <td align="center"><b>📦 Остатки</b></td>
    <td align="center"><b>⚙️ Админ-панель</b></td>
  </tr>
  <tr>
    <td>Поиск в реальном времени · бейджи статуса</td>
    <td>Управление пользователями · отчёты · материалы</td>
  </tr>
</table>

---

## 🚀 Установка

### Требования

- Windows 10 / 11
- [.NET Framework 4.8](https://dotnet.microsoft.com/download/dotnet-framework/net48)
- [SQL Server Express](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) (бесплатно)
- Visual Studio 2022

### Шаги

```bash
# 1. Клонируй репозиторий
git clone https://github.com/your-username/ConstructionWarehouse.git
cd ConstructionWarehouse
```

```bash
# 2. Восстанови NuGet-пакеты
# В Visual Studio: правой кнопкой по Solution → Restore NuGet Packages
```

```sql
-- 3. Создай базу данных
-- Открой SQL Server Management Studio
-- Выполни скрипт: Database/WarehouseDB.sql
```

```xml
<!-- 4. Настрой строку подключения в App.config -->
<connectionStrings>
  <add name="WarehouseDB"
       connectionString="Server=ИМЯ_СЕРВЕРА\SQLEXPRESS;
                         Database=ConstructionWarehouse;
                         Integrated Security=True;"
       providerName="System.Data.SqlClient"/>
</connectionStrings>
```

```bash
# 5. Запусти проект (F5 в Visual Studio)
```

### Учётные данные по умолчанию

| Логин | Пароль | Роль |
|-------|--------|------|
| `admin` | `admin123` | Администратор |

---

## 🗄️ База данных

```
ConstructionWarehouse
├── 📋 Categories        — категории материалов
├── 📏 Units             — единицы измерения
├── 🏭 Suppliers         — поставщики
├── 👷 Employees         — сотрудники
├── 🏗️  Projects          — строительные объекты
├── 🧱 Materials         — номенклатура склада
├── 🔗 MaterialSuppliers — связь материалов и поставщиков
├── 🔄 StockTransactions — складские операции
└── 👤 Users             — пользователи системы
```

**Объекты БД:**
- `vw_StockLevels` — представление остатков со статусами
- `vw_TransactionLog` — журнал операций с JOIN на справочники
- `trg_UpdateStock` — триггер автоматического пересчёта остатков
- `sp_GetLowStockMaterials` — позиции ниже минимума
- `sp_GetMaterialTurnover` — оборот материала за период

---

## 👥 Роли пользователей

| Функция | 🔴 Администратор | 🔵 Менеджер | 🟢 Кладовщик |
|---------|:---:|:---:|:---:|
| Просмотр остатков и операций | ✅ | ✅ | ✅ |
| Создание складских операций | ✅ | ✅ | ✅ |
| Редактирование материалов | ✅ | ✅ | ❌ |
| Управление поставщиками | ✅ | ✅ | ❌ |
| Активация пользователей | ✅ | ✅ | ❌ |
| Генерация отчётов Word/Excel | ✅ | ✅ | ❌ |
| Управление пользователями | ✅ | ❌ | ❌ |
| Удаление данных | ✅ | ❌ | ❌ |
| Админ-панель | ✅ | ❌ | ❌ |

---

## 🛠️ Технологии

<div align="center">

| Слой | Технология |
|------|-----------|
| **Язык** | C# 7.3 |
| **UI** | WPF + XAML (.NET Framework 4.8) |
| **База данных** | Microsoft SQL Server Express |
| **Доступ к данным** | ADO.NET (SqlConnection, SqlCommand) |
| **Отчёты Word** | DocumentFormat.OpenXml |
| **Отчёты Excel** | ClosedXML |
| **CAPTCHA** | EasyCaptcha.Wpf |
| **Безопасность** | SHA-256 (System.Security.Cryptography) |

</div>

---

## 📄 Генерация отчётов

Система поддерживает **4 типа отчётов** в **2 форматах**:

```
📦 Остатки на складе   →  Word (.docx) / Excel (.xlsx)
🔄 Журнал операций     →  Word (.docx) / Excel (.xlsx)
🔔 Низкий запас        →  Word (.docx) / Excel (.xlsx)
📋 Сводный отчёт       →  Word (.docx) / Excel (.xlsx — 4 листа)
```

Сводный Excel-отчёт включает листы: **Сводка** (KPI) · **Остатки** · **Операции** · **Низкий запас**

---

## 🔒 Безопасность

- 🔑 Пароли хранятся исключительно в виде **SHA-256 хеша**
- 🤖 **CAPTCHA** при регистрации новых пользователей
- 👁️ **Ролевая модель** — каждая функция проверяет права до выполнения
- 🛡️ Все SQL-запросы **параметризованы** (защита от SQL-инъекций)
- 📝 Логирование критических операций

---

## 📁 Структура проекта

```
ConstructionWarehouse/
├── 📄 App.xaml / App.xaml.cs          — точка входа, управление окнами
├── 🔐 LoginWindow.xaml/.cs            — авторизация
├── 📝 RegisterWindow.xaml/.cs         — регистрация с CAPTCHA
├── 🏠 MainWindow.xaml/.cs             — главное окно
├── ⚙️  AdminWindow.xaml/.cs            — панель администратора
├── 📋 ManagerWindow.xaml/.cs          — панель менеджера
├── 🧱 MaterialWindow.xaml/.cs         — редактирование материала
├── 🏭 SupplierWindow.xaml/.cs         — редактирование поставщика
├── 🔄 TransactionWindow.xaml/.cs      — новая складская операция
├── 👤 UserEditWindow.xaml/.cs         — редактирование пользователя
├── 🗄️  DB.cs                           — слой доступа к данным
├── 👤 UserModel.cs                    — модель пользователя
├── 🔑 Session.cs                      — текущая сессия
├── ⚙️  App.config                      — строка подключения к БД
└── 📦 packages.config                 — NuGet-зависимости
```

---

## 🤝 Лицензия

Распространяется под лицензией **MIT**. Подробнее см. файл [LICENSE](LICENSE).

---

<div align="center">

Сделано с ❤️ на C# + WPF

</div>
