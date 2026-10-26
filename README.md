# laminas-db

A fork of [`laminas/laminas-db`](https://github.com/laminas/laminas-db), published as `scoumbourdis/laminas-db`.

**Why a fork?** `laminas/laminas-db` is in security-only maintenance mode, and support for a new PHP version often comes months after that PHP version is released. With PHP 8.4 this blocked us: the code worked on PHP 8.4, but the official package did not allow it in its `composer.json`, because its pipeline failed on the Microsoft SQL Server driver, which did not support PHP 8.4 yet (see [laminas/laminas-db PR #312](https://github.com/laminas/laminas-db/pull/312)). So we released this fork with PHP 8.4 allowed.

**The code is untouched.** We keep the code exactly as the official package. Only `composer.json` is different (the package name, and when needed the PHP versions). This makes it easy to follow the official releases and to see every change.

**Why we keep it.** When PHP 8.6, 8.7 and later versions are released, we can allow them here first, as soon as the code works on them, without waiting for an official release. When the official package catches up, we merge its release (for example 2.22.0, which added PHP 8.5).

[![Build Status](https://github.com/laminas/laminas-db/actions/workflows/continuous-integration.yml/badge.svg)](https://github.com/laminas/laminas-db/actions/workflows/continuous-integration.yml)

> ## 🇷🇺 Русским гражданам
>
> Мы, участники Laminas, родились и живем в разных странах. У многих из нас есть друзья, родственники и коллеги как в России, так и в Украине. Некоторые из нас родились в России. Некоторые из нас живут в России. У некоторых бабушки и дедушки сражались с фашистами во Второй мировой войне. Здесь никто не поддерживает фашизм.
>
> У одного из нас есть украинская родственница, которая спаслась из дома вместе с сыном. Поезд задержался из-за бомбежки на дороге впереди. У нас есть друзья, которые прячутся в бомбоубежищах. Мы с тревогой ждем весточки от них после воздушных налетов, которые беспорядочно наносят удары и попадают по больницам, школам, детским садам и домам. Мы не берем это из каких-либо СМИ. Мы наблюдаем это напрямую.
>
> Вы доверяете нам достаточно, чтоб использовать наши программы, и мы просим вас довериться нам вновь. Мы нуждаемся в помощи. Выходите и протестуйте против этой бесполезной войны. Остановите кровопролитие. Скажите "Нет войне!"
>
> ## 🇺🇸 To Citizens of Russia
>
> We at Laminas come from all over the world. Many of us have friends, family and colleagues in both Russia and Ukraine. Some of us were born in Russia. Some of us currently live in Russia. Some have grandparents who fought Nazis in World War II. Nobody here supports fascism.
>
> One team member has a Ukrainian relative who fled her home with her son. The train was delayed due to bombing on the road ahead. We have friends who are hiding in bomb shelters. We anxiously follow up on them after the air raids, which indiscriminately fire at hospitals, schools, kindergartens and houses. We're not taking this from any media. These are our actual experiences.
>
> You trust us enough to use our software. We ask that you trust us to say the truth on this. We need your help. Go out and protest this unnecessary war. Stop the bloodshed. Say "stop the war!"

> [!CAUTION]
> This package is considered feature-complete, and is now in **security-only** maintenance mode, following a [decision by the Technical Steering Committee](https://github.com/laminas/technical-steering-committee/blob/main/meetings/minutes/2022-02-07-TSC-Minutes.md#is-laminas-db-abandoned).
> If you have a security issue, please [follow our security reporting guidelines](https://getlaminas.org/security/).
> If you wish to take on the role of maintainer, please [nominate yourself](https://github.com/laminas/technical-steering-committee/issues/new?assignees=&labels=Nomination&template=Maintainer_Nomination.md&title=%5BNOMINATION%5D%5BMAINTAINER%5D%3A+%7Bname+of+person+being+nominated%7D)

`Laminas\Db` is a component that abstract the access to a Database using an object
oriented API to build the queries. `Laminas\Db` consumes different storage adapters
to access different database vendors such as MySQL, PostgreSQL, Oracle, IBM DB2,
Microsoft Sql Server, PDO, etc.

## Contributing

Please be sure to read the [contributor's guide](https://github.com/laminas/.github/blob/main/CONTRIBUTING.md) for general information on contributing.
This section outlines specifics for laminas-db.

### Test suites

The `phpunit.xml.dist` file defines two test suites, "unit test" and "integration test".
You can run one or the other using the `--testsuite` option to `phpunit`:

```bash
$ ./vendor/bin/phpunit --testsuite "unit test" # unit tests only
$ ./vendor/bin/phpunit --testsuite "integration test" # integration tests only
```

Unit tests do not require additional functionality beyond having the appropriate database extensions present and loaded in your PHP binary.

### Integration tests

To run the integration tests, you need databases.
The repository includes a `Vagrantfile` which allows you to fire up a [vagrant box](https://app.vagrantup.com) with several of our target databases, including:

- MySQL
- PostgreSQL
- SQL Server

To start up vagrant:

```bash
$ vagrant up
```

Copy `phpunit.xml.dist` to `phpunit.xml`, and change the following ENV var declaration values to "true":

- TESTS_LAMINAS_DB_ADAPTER_DRIVER_MYSQL
- TESTS_LAMINAS_DB_ADAPTER_DRIVER_SQLSRV
- TESTS_LAMINAS_DB_ADAPTER_DRIVER_PGSQL
- TESTS_LAMINAS_DB_ADAPTER_DRIVER_SQLITE_MEMORY

From there, you can run the integration tests:

```bash
$ ./vendor/bin/phpunit --testsuite "integration test"
```

-----

- File issues at https://github.com/laminas/laminas-db/issues
- Documentation is at https://docs.laminas.dev/laminas-db/
