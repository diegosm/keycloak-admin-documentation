.. _roles_manager:

=============================
Roles Manager
=============================
.. _roles_manager.representation:

Role Class
#######################

The class ``Role`` is a
`Role Representation  <https://www.keycloak.org/docs-api/5.0/rest-api/index.html#_rolerepresentation>`_.
To use Role Manager, you need to pass the Realm that you will work with. You can also manager Client Roles too,
check Client documentation.

.. rst-class:: table
.. list-table:: for specifying which namespace and source file of Role scope
    :name: appendixes.annotations.covers.tables.annotations
    :header-rows: 1

    * - Class
      - File
    * - ``KeycloakAdmin\Roles\Role``
      - src/Roles/Role.php


.. _roles_manager.list:

List Roles
##########################

This method returns a collection of Roles of specific Realm.

Usage
---------

.. code-block:: php

    public function listRoles()
    {
        $collectionOfRoles = $this->admin
            ->role('my-realm')
            ->list();

        foreach ($collectionOfRoles as $role) {
            var_dump($role->getName());
        }
    }



.. _roles_manager.save:

Save Role
##########################

This method returns will save a new Role on specific Realm.

Usage
---------

.. code-block:: php

    public function createRole(string $id, string $name)
    {
        $myRole = [
            'id'   => $id,
            'name' => $name
        ];

        $role = $this->admin->role('my-realm')
            ->createFromArray($myRole)
            ->save();
    }




.. _roles_manager.show:

Show Role
##########################

This method returns a Role, you need to pass the parameter realmName and must pass the $id.
If Role was not found, you will receive an Exception.

Usage
---------

.. code-block:: php

    public function showRole(string $id) : Client
    {
        return $this->admin->role('my-realm')
            ->show($id);
    }


.. _roles_manager.update:

Update Role
##########################

This method will update a Role, an instance of Role must be created
before call to update. This expects at least ``id`` to can update.
In this Library, you  can't update the Role id.

Usage
---------

.. code-block:: php

    public function update(string $id, array $params = []) : Client
    {
        $data = [
            'id' => $id
        ] + $params;

        return $this->admin->role('my-realm')
            ->createFromArray($data)
            ->update();
    }


.. _roles_manager.delete:

Delete Role
##########################

This method will delete a Role, id must be passed as parameter.
If an error occurs you will receive an ``Exception`` otherwise, this
is a *void* method

Usage
---------

.. code-block:: php

    public function delete(string $id)
    {
        try {
            $this->admin->role('my-realm')
            ->delete($id);
        } catch (\Exception $e) {
            var_dump('cant delete this client, ' . $e->getMessage());
        }
    }
