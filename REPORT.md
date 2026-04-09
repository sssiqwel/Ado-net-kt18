# Отчет по заданию (кт18)

## Цель
Реализовать страницу с динамическим графиком продаж в отдельной сборке (Razor Class Library), подключить её к приложению, добавить навигацию и проверить запуск.

## Выполненные задачи по ТЗ

1. **Создана новая сборка `SalesChartComponent`**
   - Проект библиотеки Razor Class Library: [SalesChartComponent/SalesChartComponent.csproj](SalesChartComponent/SalesChartComponent.csproj)

2. **Добавлены функции для отрисовки графика**
   - Компонент графика: [SalesChartComponent/SalesChartComponent.razor](SalesChartComponent/SalesChartComponent.razor)
   - Стили графика: [SalesChartComponent/SalesChartComponent.razor.css](SalesChartComponent/SalesChartComponent.razor.css)
   - Реализованы:
     - генерация стартовых данных по месяцам;
     - динамическое обновление значений каждые 2 секунды;
     - построение линии (`polyline`), заливки под кривой (`polygon` + градиент), координат точек;
     - оси, горизонтальная сетка, подписи по оси Y (тысячи единиц) и по оси X (месяцы);
     - подписи осей выводятся через `foreignObject` + HTML, потому что в Razor зарезервирован тег `<text>` (его нельзя использовать для SVG-текста без обходных приёмов);
     - все координаты и атрибут `points` форматируются через `CultureInfo.InvariantCulture` (точка в дробях), иначе при локали `ru-RU` SVG «ломает» числа с запятой и линия превращается в хаос.

3. **Подключение отдельной сборки с компонентом и страницей**
   - Ссылка на библиотеку в основном проекте: [SalesDashboard.csproj](SalesDashboard.csproj) (`ProjectReference` на `SalesChartComponent`).
   - Регистрация маршрутов из RCL: [App.razor](App.razor) — параметр `AdditionalAssemblies` с сборкой `SalesChartComponent`, чтобы страница `/sales-chart` из библиотеки находилась роутером.

4. **Создана страница с графиком продаж**
   - Страница маршрута: [SalesChartComponent/Pages/SalesChartPage.razor](SalesChartComponent/Pages/SalesChartPage.razor)
   - Маршрут страницы: `/sales-chart`

5. **Добавлена навигация в `NavMenu`**
   - Пункт меню `Sales chart`:
     - [Layout/NavMenu.razor](Layout/NavMenu.razor)

6. **Запуск и проверка работы**
   - Сборка выполнена успешно: `dotnet build`
   - Приложение успешно стартует: `dotnet run --no-build`
   - Адрес запуска: `http://localhost:5062`

## Скриншоты для отчета

Сделайте и добавьте в отчет минимум 4 скриншота:

1. Главная страница приложения (до перехода на график).
2. Меню с пунктом `Sales chart`.
3. Страница `/sales-chart` с отображенным графиком.
4. Повторный кадр той же страницы через 2-3 секунды, чтобы показать динамическое обновление значений.

Рекомендуемые имена файлов:
- `01-home.png`
- `02-nav-sales-chart.png`
- `03-sales-chart-initial.png`
- `04-sales-chart-updated.png`

## Команды проверки

```powershell
dotnet restore
dotnet build
dotnet run
```
