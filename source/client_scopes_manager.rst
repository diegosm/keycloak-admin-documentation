.. _client_scopes_manager:

=============================
Client Scopes Manager
=============================
.. _client_scope_manager.representation:

Client Scope Class
#######################

The class ``ClientScope`` is a
`Client Scope Representation  <https://www.keycloak.org/docs-api/5.0/rest-api/index.html#_clientscoperepresentation>`_.
To use Client Scope Manager, you need to pass the Realm that you will work with.

.. rst-class:: table
.. list-table:: for specifying which namespace and source file of Client scope
    :name: appendixes.annotations.covers.tables.annotations
    :header-rows: 1

    * - Class
      - File
    * - ``KeycloakAdmin\ClientScopes\ClientScope``
      - src/ClientScopes/ClientScope.php


.. _client_scope_manager.list:

List Client Scopes
##########################

This method returns a collection of client scopes of specific Realm.

Usage
---------

.. code-block:: php

    public function listClientScopes()
    {
        $collectionOfClientScopes = $this->admin
            ->clientScope('my-realm')
            ->list();

        foreach ($collectionOfClientScopes as $scope) {
            var_dump($scope->getAttributes());
        }
    }



.. _client_scope_manager.save:

Save Client Scope
##########################

This method returns will save a new Client Scope on specific Realm.

Usage
---------

.. code-block:: php

    public function createClientScope(string $id, string $name)
    {
        $myClientScope = [
            'id'   => $id,
            'name' => $name
        ];

        $clientScope = $this->admin->clientScope('my-realm')
            ->createFromArray($myClientScope)
            ->save();
    }




.. _client_scope_manager.show:

Show Client Scope
##########################

This method returns a Client Scope, you need to pass the parameter realmName and must pass the $id.
If Client Scope was not found, you will receive an Exception.

Usage
---------

.. code-block:: php

    public function showClientScope(string $id) : Client
    {
        return $this->admin->clientScope('my-realm')
            ->show($id);
    }


.. _client_scope_manager.update:

Update Client Scope
##########################

This method will update a Client Scope, an instance of Client Scope must be created
before call to update. This expects at least ``id`` to can update.
In this Library, you  can't update the client scope id.

Usage
---------

.. code-block:: php

    public function update(string $id, array $params = []) : Client
    {
        $data = [
            'id' => $id
        ] + $params;

        return $this->admin->clientScope('my-realm')
            ->createFromArray($data)
            ->update();
    }


.. _client_scope_manager.delete:

Delete Client Scope
##########################

This method will delete a Client Scope, id must be passed as parameter.
If an error occurs you will receive an ``Exception`` otherwise, this
is a *void* method

Usage
---------

.. code-block:: php

    public function delete(string $id)
    {
        try {
            $this->admin->clientScope('my-realm')
            ->delete($id);
        } catch (\Exception $e) {
            var_dump('cant delete this client, ' . $e->getMessage());
        }
    }


.. _client_scope_manager.protocol_mappers:

Protocol Mappers
##########################

This is a manager for client protocol mappers manager.
Check :ref:`protocol_mappers`. chapter.

.. code-block:: php

    public function protocolMapperExample(string $id)
    {
        $collectionOfProtocolMappers = $this->admin
            ->clientScope('my-realm')
            ->protocolMappers($id)
            ->list();

        // do something cool
    }
