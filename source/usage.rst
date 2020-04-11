.. _usage:

=============================
Basic Usage
=============================

.. _usage.factory:

KeycloakAdmin Factory
#######################

To make a new instance of our library, simply use our factory, with 3 main parameters
username, secret and base url of your keycloak admin client. This will return a
KeycloakAdminManager

`Remember to first create a admin client manager on master Realm`

.. code-block:: php

    use KeycloakAdmin\Factories\KeycloakAdminFactory;

    abstract class MyKeycloakAdminBase
    {
        /** @Var KeycloakAdmin */
        protected $admin;

        public function __construct()
        {
            $this->admin = KeycloakAdminFactory::create(
                'manager-cli-on-realm-master',
                '28523bba-03s8-438a-8xf0-c8837a972ad7',
                'http://keycloak:8080/auth'
            );
        }
    }

With this approach you can easily extend this abstract class to implement
your operations, like create new Realm for example.


.. code-block:: php

    use KeycloakAdmin\Factories\KeycloakAdminFactory;

    class CreateRealm extends
    {
        /**
         * Json example {"realm": "my-first-realm", "notBefore": 1000}
         */
        public function create(string $json)
        {
            $this->admin->realm()->createFromJson($json)->save();
        }
    }



.. _usage.creating_entities:

Creating entities to save or update resources
###############################################

Each resource uses an entity object to save or update resources.
To create these entities or Representations(as Keycloak Admin REST API named) you
have two ways.

As you saw on previous example, you can use createFromJson and pass a
JSON representation of this entity that you're trying to create.

Or if you prefer, you can use createFromArray and pass an array representation
of this entity.

