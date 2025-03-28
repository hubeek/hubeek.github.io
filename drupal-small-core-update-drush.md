# Drupal small core update drush

_Status: Published_
_Created: 2017-02-03 02:30:16_
_Tags: php bash python cli drush_

<b>sudo apt-get update</b>

put in maintenance mode:
<b>drush vset --exact maintenance_mode 1 drush cache-clear all</b>
update:
<b>drush pm-update drupal</b>
update modules:
<b>drush up</b>
update specific module:
<b>drush up [module]</b>
put out of maintenance mode:
<b>drush vset --exact maintenance_mode 0 drush cache-clear all </b>