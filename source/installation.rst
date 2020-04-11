.. _installation:

=============================
Installing PHP Keycloak Admin
=============================

.. _installation.requirements:

Requirements
############

PHP Keycloak Admin |version| requires PHP 7.2; using the latest version of PHP is highly
recommended.

PHP Keycloak Admin requires the `json <http://php.net/manual/en/json.installation.php>`_
extension, which are normally enabled by default.

Keycloak Admin also requires the
`guzzle <http://docs.guzzlephp.org/en/stable/>`_,
`jms/serializer <https://jmsyst.com/libs/serializer>`_,
composer packages.

.. _installation.composer:

Composer
########

Simply add a (development-time) dependency on
``phpunit/phpunit`` to your project's
``composer.json`` file if you use `Composer <https://getcomposer.org/>`_ to manage the
dependencies of your project:

.. parsed-literal::

    composer require diegosm/keycloak-admin ^\ |version|
