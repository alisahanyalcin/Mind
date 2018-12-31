
# What is Mind?

In projects developed with `PHP` and `MySQL`; Database and route operations, `$_GET`, `$_POST`, `$_FILES` requests, PHP code framework that simplifies the management of various control layers such as `Model`, `View`, `Controller`, `Middleware`.

To create new design patterns and frameworks, Mind offers great tools. Because it is easy to create a custom design pattern for your needs, the features that will always remain small remain small. It enables controlled and safe growth for a growing project.

---------- 

## Download

You can download the Mind class from [GitHub page](https://github.com/aliyilmaz/Mind/archive/master.zip) or proceed to the next step by running the `composer require mind/mind` command from the command client.

---------- 

## Database settings

To use the class, you must define the database information in the `Mind.php` file or when calling the class.

#### Example

    private $host        = 'localhost';
    private $dbname      = 'mydb';
    private $username    = 'root';
    private $password    = '';
    
or

    $conf = array(
        'host'      =>  'localhost',
        'dbname'    =>  'mydb',
        'username'  =>  'root',
        'password'  =>  ''
    );
    $Mind = new Mind($conf);

----------

## Installation

After adding `Mind.php` to the project with a method like `require_once`, it is possible to get the class ready for use with the command `extends` or `new Mind()`.

#### Example

    require_once('./Mind.php');
    use Mind\Mind;
    $Mind = new Mind();

or

    require_once('./Mind.php');
    class ClassName extends Mind\Mind{
    
    }

----------

## Session settings

This is the part used to customize or close sessions created for users. To close sessions, simply set the session_status parameter to `false`. To change the folder path where the sessions are stored, the `path` parameter must be updated. To keep sessions on the specified path, the `path_status` parameter must be set to `true`. By default, the server is configured according to the session settings.

#### Example

    private $sessset    = array(
        'path'              =>  './session/',
        'path_status'       =>  false,
        'status_session'    =>  true
    );

----------


## Time zones settings

It is possible to personalize the time zone to mark the content with the correct time zone. By default `Europe/Istanbul` is defined. The `public` property is defined to allow access from outside the class. See the [List of Supported Timezones](https://secure.php.net/manual/en/timezones.php) section.

**Info:** Servers that are not as personalized as required may use different time periods from the project timeframe. Editing in this section allows you to have the correct timestamp on different servers. 

#### Example

    public $timezone    = 'Europe/Istanbul';

----------

## Active Methods

Methods that meet requirements such as session management, database connectivity, `$_GET`, `$_POST`, and `$_FILES` requests are enabled by running the `__construct()` method in the `Mind.php` file.

-   [session_check()](#session_check)
-   [connection()](#connection)
-   [request()](#request)

----------

## Active variables

##### private $ conn

The database connection is held in `$this->conn`. To prevent access from outside the class `private` property is defined.

##### public $ post

The `$_GET`,`$_POST` and `$_FILES` requests made in the project where the class is included are kept in `$this-> post`. To allow access from outside the classroom, the `public` property is defined.

##### public $ baseurl

The path of the folder where `Mind.php` is located is kept in `$this->baseurl`, and `public` is defined to allow access from outside the class.

----------

## Methods

##### Database

-   [connection](#connection)
-   [prepare](#prepare)
-   [cGeneration](#cGeneration)
-   [pGeneration](#pGeneration)
-   [createdb](#createdb)
-   [createtable](#createtable)
-   [createcolumn](#createcolumn)
-   [deletedb](#deletedb)
-   [deletetable](#deletetable)
-   [deletecolumn](#deletecolumn)
-   [cleardb](#cleardb)
-   [cleartable](#cleartable)
-   [clearcolumn](#clearcolumn)
-   [insert](#insert)
-   [update](#update)
-   [delete](#delete)
-   [get](#get)
-   [do_have](#do_have)
-   [newid](#newid)
-   [increments](#increments)

##### Validator

-   [is_db](#is_db)
-   [is_table](#is_table)
-   [is_column](#is_column)
-   [is_phone](#is_phone)
-   [is_date](#is_date)
-   [is_email](#is_email)
-   [is_type](#is_type)
-   [is_size](#is_size)
-   [is_color](#is_color)
-   [is_url](#is_url)
-   [is_json](#is_json)

##### Helper

-   [info](#info)
-   [filter](#filter)
-   [request](#request)
-   [redirect](#redirect)
-   [mindload](#mindload)
-   [permalink](#permalink)
-   [timezones](#timezones)
-   [session_check](#session_check)

##### System

-   [route](#route)
-   [write](#write)
-   [upload](#upload)
-   [get_contents](#get_contents)

----------

## connection()

It is used to provide database connection in the light of the information specified in the [installation](#installation) phase. It was run in `__construct()` method in `Mind.php` file.

----------

## prepare()

It is used to run SQL queries, it has `public` definition to send `SQL` query from outside the class. The `SQL` query can be sent as `string`.
   
##### Example

    $Mind->prepare($sql);

----------

## cGeneration()
This function is used to create the syntax of the `sql`, which should be written when creating a database table or column. The syntax of `sql` is generated by the interpretation of the schema that is sent to the `createtable` and `createcolumn` methods.

----------

## pGeneration()
This function is used to parse the parameterized address sent to `route` and `mindload`.

----------

## createdb()

Used to create new one or more databases. `mydb0` and` mydb1` represent the database names. Database creation occurs when the database names to be created are sent as `string` or `array`. If the operation is successful, `true`, otherwise `false` is returned.

##### Example

    $this->createdb('mydb0');

or

    $this->createdb(array('mydb0','mydb1'));
    
----------
    
## createtable()

Used to create a new database table. If the operation is successful, `true`, otherwise `false` is returned.

##### Features

-   int - (`int`)
-   decimal - (`decimal`)
-   string - (`varchar`)
-   small - (`text`)
-   medium - (`mediumtext`)
-   large - (`longtext`)
-   increments - (`auto_increment`)

##### Example

    $scheme = array(
        'id:increments',
        'username:small',
        'password',
        'address:medium',
        'about:large',
        'amount:decimal:6,2',
        'title:string:120',
        'age:int'
    );
    $this->createtable('phonebook', $scheme);
    
****Info:**** For more information about creating a column, see the [createcolumn](#createcolumn) method.
