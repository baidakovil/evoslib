# Библиотека BIM-компонентов


<div style="max-width: 60%;">
<p>Библиотека BIM-компонентов <i>evoslib</i> это удобное хранилище элементов, предназначенных для использования в программном комплексе <b>nanoCAD BIM Вентиляция</b>.</p>

<p>BIM-компонент — это zip-архив, содержащий структуру файлов и папок, загружаемых в программу. В программе BIM-компонент представляет модель реального оборудования или является элементом оформления (Текстовая выноска).</p>

<p>Подобно тому, как библиотека бумажных книг хранит не только книги, но и другую полезную информацию о них, такую как год издания, номер в каталоге и проч., библиотека BIM-компонентов хранит дополнительную информацию о BIM-компоненте:
</p>
</div>
<div style="max-width: 70%;">

| Понятное описание                                | Тип данных                                                                                  | Пример                                                                                                                                                                          |   |   |   |
|--------------------------------------------------|---------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|---|---|
| Уникальный номер BIM-компонента                  | Целое число                                                                                 | 2                                                                                                                                                                               |   |   |   |
| Категория                                        | Текст из списка                                                                             | Воздухораспределители                                                                                                                                                           |   |   |   |
| Подкатегория                                     | Текст из списка                                                                             | Решетка                                                                                                                                                                         |   |   |   |
| Дополнительная характеристика                    | Текст из списка                                                                             | жалюзийная                                                                                                                                                                      |   |   |   |
| Тип графики                                      | Текст из списка                                                                             | Параметрическая                                                                                                                                                                 |   |   |   |
| Форма подключаемого воздуховода или трубопровода | Текст из списка                                                                             | Прямоугольный                                                                                                                                                                   |   |   |   |
| Доступные в BIM-компоненте типоразмеры           | Текст в формате `красные: 100x100...300x300; белые: 100, 125, 630` или просто через запятую | 200x200, 300x300                                                                                                                                                                |   |   |   |
| Описание BIM-компонента                          | Текст                                                                                       | В параметрической dwg-графике реализована возможность поворота угла ламелей по параметру. Этот параметр при необходимости может быть вынесен в параметры nanoCAD BIM Вентиляция |   |   |   |
| Версия                                           | Целое число                                                                                 | 2                                                                                                                                                                               |   |   |   |
| История изменений версий                         | Текст в формате `v1: бла-бла; v2: фу-бар`                                                   | v2: добавлены новые типоразмеры                                                                                                                                                 |   |   |   |
| Материал, из которого изготовлено оборудование   | Список[Пара[текст-булева переменная]]                                                       | {Алюминий: Да, Оцинкованная сталь: Нет, ...}                                                                                                                                    |   |   |   |
| Ссылка на сайт производителя                     | Текст                                                                                       | http://vo.ru                                                                                                                                                                    |   |   |   |

</div>

Эти типы данных приняты условно, а не технически, т.е. в принципе в каждое поле может быть введен любой представимый в виде текста значение. Но тогда правильная работа веб-интерфейса не гарантируется. 

## Содержание

1. [Цель создания библиотеки](#цель-создания-библиотеки)
2. [Доступ к библиотеке](#доступ-к-библиотеке)
3. [Структура проекта](#структура-проекта)
   - [Файлы веб-страницы библиотеки](#файлы-веб-страницы-библиотеки)
     - [index.html](#indexhtml)
     - [jsscripts](#jsscripts)
       - [main.js](#mainjs)
       - [components.js](#componentsjs)
       - [filters.js](#filtersjs)
4. [Описание python-скриптов](#Описание-python-скриптов)
5. [Проблемы проекта](#Проблемы-проекта)
6. [Дорожная карта](#Дорожная-карта)


<img src="./git/readme/base.png" alt="Библиотека компонентов" style="width: 60%;"></img>


# Цель создания библиотеки:

- собрать BIM-компоненты из разных источников в одном месте для получения актуальной информации о их наличии
- дать возможность быстрой фильтрации BIM-компонентов по различным параметрам для удобства их поиска
- проводить версионирование BIM-компонентов


# Доступ к библиотеке

Библиотека компонентов доступна на GitHub Pages по адресу: [https://nanoib.github.io/evoslib/](https://nanoib.github.io/evoslib/).

GitHub Pages — это сервис, предоставляемый GitHub для хостинга статических веб-страниц прямо из репозиториев GitHub.


# Структура проекта

Проект организован в несколько основных директорий и файлов:
## Файлы веб-страницы библиотеки

- **index.html**: Файл с разметкой веб-страницы проекта. Размещает основные элементы веб-страницы: заголовок, шапка, боковая секция фильтра, сетка BIM-компонентов. Хранит теги для поисковика. Загружает файлы JavaScript.
- **jsscripts**: папка с JavaScript-скриптами. Они улучшают веб-интерфейс и предоставляют дополнительную функциональность.

    ### **main.js**
    Этот модуль отвечает за инициализацию веб-приложения. Он устанавливает глобальные переменные фильтров и загружает данные BIM-компонентов из файла `Base.json`. После загрузки данных он инициализирует фильтры и отображает BIM-компоненты.

    ### **components.js**
    Этот модуль обрабатывает отображение BIM-компонентов на веб-странице. Он создает необходимые HTML-элементы (плитки) для каждого BIM-компонента и добавляет их в сетку компонентов. Также он устанавливает обработчики событий для открытия модального окна при клике на BIM-компонент.

    Текст в плитке имеет дополнительное правило отображения:
    - если *Дополнительная характеристика* (`component.surname`) для BIM-компонента не определена, то она не отображается; отделяющий это поле пробел в этом случае тоже не отображается 

    ### **filters.js**
    Этот модуль управляет функциональностью фильтров. Он инициализирует фильтры на основе данных BIM-компонентов, и отображает их по разделам фильтрации, прописанным в коде: "Техническая категория", "Производитель", "Тип графики" и "Форма". Также он применяет фильтры к данным BIM-компонентов и обновляет отображаемые компоненты соответственно. Кроме того, он предоставляет функцию сброса для очистки всех фильтров.

    - Фильтры внутри каждой из категорий работают по принципу ИЛИ (т.е. выбрав двух производителей, вы увидите BIM-компоненты каждого из двух производителей), а фильтры различных категорий работают по принципу И (т.е. добавив к тем фильтрам по производителям еще и фильтры из других категорий, например "Тип графики" = *Параметрическая графика* и "Форма" = *Круглый*, вы увидите только круглые и параметрические BIM-компоненты именно этих производителей).

    - Как было упомянуто, разделы фильтрации прописаны в коде. Однако сами категории фильтрации (прописанные рядом с чекбоксами) создаются динамически на основании данных в базе. Эти категории и подкатегории динамически (то есть прямо при открытии страницы, во время работы скрипта) создаются скриптом `filters.js` на основании данных из `Base.json`. 

        Таким образом, например, для создания новой категории оборудования *Изоляция воздуховодов* с подкатегориями *Трубчатая изоляция* и *Листовая изоляция*, администратору базы данных достаточно добавить в файл `Base.xlsx` две новых строчки с данными новых компонентов: столбец `siteCategory` у обоих должен быть заполнен *Изоляция воздуховодов*, а столбец `technicalCategory` заполнен *Трубчатая изоляция* для первого и *Листовая изоляция* для второго компонента. Далее разместить в папке **im** изображения для компонентов и запустить скрипт **xlsxtojson.py**. 

        И все!

    ### **modal.js**
    Этот модуль управляет функциональностью модального окна. Он определяет функцию *openModal*, которая заполняет модальное окно деталями выбранного BIM-компонента и отображает его. Модальное окно включает информацию, такую как изображение BIM-компонента, техническая категория, дополнительные характеристики и описание.

    - Текст в модальном окне имеет дополнительные правила отображения:
        - если *Типоразмеры* содержат точку с запятой `;`, текст после нее переносится на новую строку
        - если *Форма* или *Типоразмеры* имеют в xlsx/json значение *Не применимо*, то эти поля не отображаются

    ### **.nojekyll**
    Файл `.nojekyll` используется для отключения обработки Jekyll на GitHub Pages, что позволяет использовать произвольные файлы и директории. Не ясно, почему это необходимо, но без этого файла скрипт не мог прочитать файл `Base.json`. 

- **styles.css**: CSS-стили, применяемые к веб-интерфейсу библиотеки. Обеспечивают визуально привлекательный вид.

## Хранение и подготовка данных

### **db**
Содержит файлы данных: `Base.json`, `Base.xlsx`. Эти файлы являются источниками данных для проекта. 

В `Base.xlsx` администратор библиотеки вносит данные, получаемые от производителей оборудования: названия BIM-компонентов, их категорию, типоразмеры и другую информацию о них, а также имена скриншотов.
Из `Base.json` происходит чтение данных при отрисовке веб-страницы. 

### **im**
Содержит изображения BIM-компонентов. Это скриншоты из программы.

### **pyscripts**
Содержит Python-скрипты, помогающие администрировать базу данных. Каждый скрипт со вспомогательными файлами находится в своей папке: `cropwhite`, `rename`, и `xlsxtojson`.


# Описание python-скриптов
- **cropwhite**: Скрипт `cropwhite.py` предназначен для обработки изображений компонентов. Он выполняет обрезку скриншотов, удаляя лишние белые поля вокруг компонентов, и добавляет белую границу заданного размера для достижения нужного соотношения сторон изображений. Это помогает стандартизировать внешний вид изображений компонентов в библиотеке.
- **rename**: Скрипт `rename.py` используется для переименования файлов изображений компонентов. Эта необходимость возникает в связи с необходимостью ручного создания скриншотов (при этом трудно проконтролировать консистентность), но желанием иметь унифицированные имена изображений. В данный момент унифицированный код изображений задается в `Base.xlsx`, далее вручную переносится в текстовый файл перед запуском `rename.py`.
- **xlsxtojson**: Скрипт `xlsxtojson.py` преобразует данные из Excel файла (`Base.xlsx`) в формат JSON (`Base.json`). Это необходимо для того, чтобы данные о компонентах могли быть легко использованы JavaScript.

Все скрипты можно запускать двойным кликом из Проводника Windows.

# Проблемы проекта
Проект имеет недостатки, которые могут повлиять на его эффективность и удобство использования:

- **Проблемы при большом количестве компонентов**: При многократном увеличении количества компонентов в библиотеке, производительность скриптов может значительно снизиться, браузер будет тормозить, а страницей будет неудобно пользоваться. Это может привести к замедлению работы веб-интерфейса и ухудшению пользовательского опыта.

- **Отсутствие ссылок на скачивание каждого компонента индивидуально**: В проекте нет возможности скачивания отдельных компонентов напрямую с веб-страницы. Потому что эти отдельные компоненты вообще отдельно-то еще и не подготовлены.

Имеются планы на исправление недостатков.

## Дорожная карта

Проект не имеет дорожной карты.