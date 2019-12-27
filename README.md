## **Вариант использования**

- Ставим sonar lint плагин для шторма (File→Settings→Plugins→Marketplace), отключаем бесполезную инспекцию literal to constant,
- Настраиваем phpcs для работы, как psr12 инспекция шторма (weak warning):
    - Установка в систему

            composer global require "squizlabs/php_codesniffer=*"

    - Настраиваем в шторме: 
    Сначала подключаем тулзу: Settings→Languages & Frameworks→PHP→Quality Tools→PHP_CodeSniffer. Указываем путь /home/{user}/.composer/vendor/bin/phpcs
    После настраиваем инспекцию: Settings→Editor→Inspections→PHP→Quality Tools→PHP CS Fixer validation.
    - фиксер из этого же пакета не ставим, вместо этого...
- Для рефакторинга применяем php-cs-fixer с кастомными правилами
    - Установка в систему

            composer global require friendsofphp/php-cs-fixer

    - Настройка правил
    Качаем наш код-стайл - [https://github.com/timofey-n/zimalab-coding-style](https://github.com/timofey-n/zimalab-coding-style)
    - Настройка в шторме (необязательно, если применяем standalone фикс): Подключаем тулзу по аналогии с PHP_CS. Подключаем инспекцию, указываем "Custom" ruleset, указываем путь до скаченного php_cs файла с code style.
    - Применение фиксера для фикса всего проекта (standalone fix):
    Нужно убедиться, что все изменения закоммитаны. Выполняем команду в корне проекта:

            {/path/to/}php-cs-fixer fix --config={/absolute/path/to/}php-cs-fixer-zimalab-coding-style.php_cs

        После всё проверяем и коммитаем.

    - Применение фикса на коммит (пока с этим проблемы, т.к. шторм применяет все доступные инспекции, не только наши. Как разберёмся - пункт дополнится)
    - Статический анализ всего проекта штормом (sonarlint+phpcs+php-cs-fixer+phpstorm)
    Это тоже очень полезно делать. Делается тут: Code→Inspect Code→Whole project. Кэш и прочие левые папки должны быть помечены, как **Excluded**.

