# bitrix-autoloader

Автозагрузка классов.

Больше не придется писать `CModule::IncludeModule('iblock');` в каждом компоненте или скрипте.

Инициализация автолоадера происходит при создании нового экземпляра класса \Eugenezadorin\Bitrix\Autoloader() в файле init.php.

Большинство стандартных модулей, указанных в документации, будут подключаться автоматически. Это реализовано за счет «таблицы» соответствий между названиями классов и модулями. Например:

    '/^CIBlock/' => 'iblock'
    
Данное выражение указывает автолоадеру, что все классы, начинающиеся на 'CIBlock' относятся к модулю информационных блоков. «Таблица» соответствий захардкожена в классе \Eugenezadorin\Bitrix\Autoloader(), и может быть расширена методом `addClassMapItem`. Пример:

    $autoloader = new \Eugenezadorin\Bitrix\Autoloader();
    $autoloader->addClassMapItem('/^CFooBar/', 'foobar');
    
Теперь все методы классов, начинающихся на 'CFooBar' будут работать без отдельного подключения модуля 'foobar'.

Автолоадер подключает также все пользовательские классы, расположенные в папке /local/classes. Каждый класс должен располагаться в отдельном файле, имя которого должно совпадать с названием класса. Например, класс UserHandlers должен быть расположен по адресу `/local/classes/UserHandlers.php`.

Если нужно задать дополнительную директорию, в которой хранятся пользовательские классы, можно воспользоваться методом `addAutoloadPath`. Пример:

    $autoloader = new \Eugenezadorin\Bitrix\Autoloader();
    $autoloader->addAutoloadPath('/includes/my/classes/');
    
Путь указывается от корня сайта.

## Установка с помощью Composer

Страница проекта на packagist: [https://packagist.org/packages/eugenezadorin/bitrix-autoloader](https://packagist.org/packages/eugenezadorin/bitrix-autoloader)

Для быстрой установки достаточно вписать следующую зависимость в composer.json:

	"require" : {"eugenezadorin/bitrix-autoloader": "dev-master"}
