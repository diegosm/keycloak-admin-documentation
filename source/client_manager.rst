.. _client_manager:

=============================
Client Manager
=============================

.. _client_manager.representation:

Client Class
###############

The class ``Client`` is a
`Client Representation  <https://www.keycloak.org/docs-api/5.0/rest-api/index.html#_clientrepresentation>`_.
To use Client Manager, you need to pass the Realm that you will work with.

.. rst-class:: table
.. list-table:: for specifying which namespace and source file of Client
    :name: appendixes.annotations.covers.tables.annotations
    :header-rows: 1

    * - Class
      - File
    * - ``KeycloakAdmin\Client\Client``
      - src/Client/Client.php


.. _client_manager.list:

List Clients
##########################

This method returns a collection of clients of specific Realm.

Usage
---------

.. code-block:: php

    public function listClients()
    {
        $collectionOfClients = $this->admin->clients('my-realm')->list();

        foreach ($collectionOfClients as $client) {
            var_dump($client->getClient());
        }
    }



.. _client_manager.save:

Save Client
##########################

This method returns will save a new Client on specific Realm.

Usage
---------

.. code-block:: php

    public function createClient(string $id, string $name)
    {
        $myClient = [
            'id'   => $id,
            'name' => $name
        ];

        $client = $this->admin->clients('my-realm')->createFromArray($myClient)->save();
    }




.. _client_manager.show:

Show Client
##########################

This method returns a Client, you need to pass the parameter realmName and must pass the $idOfClient
is the id field <not the field client id>.

If Client was not found, you will receive an Exception.

Usage
---------

.. code-block:: php

    public function showClient(string $idOfClient) : Client
    {
        return $this->admin->clients('my-realm')->show($idOfClient);
    }


.. _client_manager.update:

Update Client
##########################

This method will update a Client, an instance of Client must be created
before call to update. This expects at least ``id`` to can update.
In this Library, you  can't update the client id.

Usage
---------

.. code-block:: php

    public function update(string $idOfClient, array $params = []) : Client
    {
        $data = [
            'id' => $idOfClient
        ] + $params;

        return $this->admin->clients('my-realm')->createFromArray($data)->update();
    }


.. _client_manager.delete:

Delete Client
##########################

This method will delete a Client, idOfClient must be passed as parameter.
If an error occurs you will receive an ``Exception`` otherwise, this
is a *void* method

Usage
---------

.. code-block:: php

    public function delete(string $idOfClient)
    {
        try {
            $this->admin->clients('my-realm')->delete($idOfClient);
        } catch (\Exception $e) {
            var_dump('cant delete this client, ' . $e->getMessage());
        }
    }




.. _client_manager.credentials:

Client Credentials
##########################

The Clients Manager have a sub manager to control credentials and with this manager you can
get and set new credential for client.

Get Usage
-----------
This method returns an instance of CredentialRepresentation

.. code-block:: php

    public function getCredential(string $idOfClient) : CredentialRepresentation
    {
        return $this->admin
            ->clients('my-realm')
            ->credentials($idOfClient)
            ->get();
    }

Save Usage
-----------
To create new credential for specific client you have two ways, first just call to this method and
it will create random new secret for you, but if you must to specify, see Keycloak to know what you will need
to pass on CredentialRepresentation.

.. code-block:: php

    public function getCredential(string $idOfClient)
    {
        $data = []; // check on Keycloak API

        $credentialRepresentation = $this->admin
            ->clients('my-realm')
            ->credentials($idOfClient)->createFromArray($data)
            ->save();

        // do something cool
    }

Generate Usage
---------------
This method is an alias for Save method.



.. _client_manager.protocol_mappers:

Protocol Mappers
##########################

This is a manager for client protocol mappers manager.
Check :ref:`protocol_mappers`. chapter.

.. code-block:: php

    public function protocolMapperExample(string $idOfClient)
    {
        $collectionOfProtocolMappers = $this->admin
            ->clients('my-realm')
            ->protocolMappers($idOfClient)
            ->list();

        // do something cool
    }
