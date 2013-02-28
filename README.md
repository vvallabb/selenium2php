Selenium2php
==========================

###Description
Converts HTML text of Selenium test case recorded from Selenium IDE into
PHP code for PHPUnit_Extensions_SeleniumTestCase as TestCase file.

###Usage
    selenium2php [switches] Test.html [Test.php]
    selenium2php [switches] <directory>
    
    --dest=<path>                  Destination folder.
    --php-prefix=<string>          Add prefix to php filenames.
    --php-postfix=<string>         Add postfix to php filenames.
    --browser=<browsers string>    Set browser for tests.
    --browser-url=<url>            Set URL for tests.
    --remote-host=<host>           Set Selenium server address for tests.
    --remote-port=<port>           Set Selenium server port for tests.
    -r|--recursive                 Use subdirectories for converting.
    --class-prefix=<prefix>        Set TestCase class prefix.
    --use-hash-postfix             Add hash part to output filename
    --files-pattern=<pattern>      Glob pattern for input test files (*.html).
    --output-tpl=<file>            Template for result file. See TestExampleTpl.

###Example
You have google.html recorded in Selenium IDE:

    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
    <head profile="http://selenium-ide.openqa.org/profiles/test-case">
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <link rel="selenium.base" href="https://www.google.ru/" />
    <title>google</title>
    </head>
    <body>
    <table cellpadding="1" cellspacing="1" border="1">
    <thead>
    <tr><td rowspan="1" colspan="3">google</td></tr>
    </thead><tbody>
    <tr>
            <td>open</td>
            <td>/</td>
            <td></td>
    </tr>
    <tr>
            <td>type</td>
            <td>id=gbqfq</td>
            <td>github</td>
    </tr>
    <tr>
            <td>waitForElementPresent</td>
            <td>id=res</td>
            <td></td>
    </tr>
    <tr>
            <td>assertTextPresent</td>
            <td>Build software better, together</td>
            <td></td>
    </tr>
    </tbody></table>
    </body>
    </html>

You run

    php selenium2php.php google.html

And you get GoogleTest.php

    <?php
    /*
    * Autogenerated from Selenium html test case by Selenium2php.
    * 2013-02-28 12:26:53
    */
    class GoogleTest extends PHPUnit_Extensions_SeleniumTestCase{
        function setUp(){
            $this->setBrowser("*firefox");
            $this->setBrowserUrl("https://www.google.ru/");
        }
        function testGoogle(){
            $this->open("/");
            $this->type("id=gbqfq", "github");
            for ($second = 0; ; $second++) {
                if ($second >= 60) $this->fail("timeout");
                try {
                    if ($this->isElementPresent("id=res")) break;
                } catch (Exception $e) {}
                sleep(1);
            }
            $this->assertTrue($this->isTextPresent("Build software better, together"));
        }
    }    

###License
    Copyright 2013 Rnix Valentine
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
    http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

