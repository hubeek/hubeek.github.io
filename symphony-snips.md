# Symphony snips

_Status: Published_
_Created: 2016-12-23 12:39:17_
_Tags: php symphony_

timezone
in app kernel.php
<code>
public function __construct($environment, $debug)
{
    date_default_timezone_set('Europe/Amsterdam');
    parent::__construct($environment, $debug);
}
</code>

server:
php bin/console server:run

php bin/console generate:bundle

composer require knplabs/knp-menu-bundle dev-master


bin/console doctrine:database:create
( drop:
bin/console doctrine:database:drop --force
)

bin/console doctrine:generate:entity
bin/console doctrine:schema:update --force