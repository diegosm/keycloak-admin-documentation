.. _realm_manager:

=============================
Realm Manager
=============================

.. _realm_manager.representation:

Realm Class
#############

The class ``Realm`` is a
`Realm Representation  <https://www.keycloak.org/docs-api/5.0/rest-api/index.html#_realmrepresentation>`_.

.. rst-class:: table
.. list-table:: for specifying which namespace and source file of Realm
    :name: appendixes.annotations.covers.tables.annotations
    :header-rows: 1

    * - Class
      - File
    * - ``KeycloakAdmin\Realm\Realm``
      - src/Realm/Realm.php


.. _realm_manager.list:

List Realms
##########################

This method returns a collection of realms.

Usage
---------

.. code-block:: php

    public function listRealms()
    {
        $collectionOfRealms = $this->admin->realms()->list();

        foreach ($collectionOfRealms as $realm) {
            var_dump($realm->getRealm());
        }
    }



.. _realm_manager.save:

Save Realm
##########################

This method returns will save a new Realm.

Usage
---------

.. code-block:: php

    public function createRealm(string $name)
    {
        $myRealm = [
            'realm' => $name
        ];

        $realm = $this->admin->realms()->createFromArray($myRealm)->save();
    }




.. _realm_manager.show:

Show Realm
##########################

This method returns a Realm, realmName must be passed as parameter.
If Realm was not found, you will receive an Exception.

Usage
---------

.. code-block:: php

    public function showRealm(string $realmName) : Realm
    {
        return $this->admin->realms()->show($realmName);
    }


.. _realm_manager.update:

Update Realm
##########################

This method will update a Realm, an instance of Realm must be created
before call to update. This expects at least ``realm`` to can update.
In this Library, you  can't update the realm name.

Usage
---------

.. code-block:: php

    public function update(string $realmName, array $params = []) : Realm
    {
        $data = [
            'realm' => $realmName
        ] + $params;

        return $this->admin->realms()->createFromArray($data)->update();
    }


.. _realm_manager.delete:

Delete Realm
##########################

This method will delete a Realm, realmName must be passed as parameter.
If an error occurs you will receive an ``Exception`` otherwise, this
is a *void* method

Usage
---------

.. code-block:: php

    public function delete(string $realmName)
    {
        try {
            $this->admin->realms()->delete($realmName);
        } catch (\Exception $e) {
            var_dump('cant delete this realm, ' . $e->getMessage());
        }
    }

