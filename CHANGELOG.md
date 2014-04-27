# Different from original


* 複数データベース接続する際のテストの簡易化

=> CIUnitTestCase.php
=> Fixture.php

An associative array of table names. The order of the fixtures
determines the loading and unloading sequence of the fixtures. This is 
to help account for foreign key restraints in databases.

$db_tablesプロパティを追加。各データベースの各テーブル毎に
フィクスチャーをロードする機能を追加。


For example:
$db_tables = array(
    'master' => array(
        'group' => 'group',
        'user' => 'user',
        'user_group' => 'user_group'
        'table_a' => 'table_a_01'
    ),
    'user' => array(
        'user_basic' => 'user_basic'
    )
);

Note: To test different data scenarios for a single database, create
different fixtures.

For example:
$db_tables = array(
    'master' => array(
        'table_a' => 'table_a_02'
    )
);

=> CIUnitTestCase.php

CIUnit_TestCase#connect($db_name)
を追加。テストケースにおいて、現在接続しているデータベースの切り替えを行なう。


* 複数データベースのフィクスチャーを生成可能に

=> Generate.php

Usage:
    php generate.php fixtures <options>
Options:
    -d  database of which fixtures should be created <default: default>
    -f  tables of which fixtures should be created (-f table1 -f table2 etc)
         omitting the -f option, selects all tables in the database.
    -n  number of rows in fixtures <default: 5>
    -o  output directory