.. _protocol_mappers:

=============================
Protocol Mappers Manager
=============================
.. _protocol_mappers.representation:

Protocol Mapper Class
#######################

The class ``Protocol Mapper`` is a
`Protocol Mapper Representation  <https://www.keycloak.org/docs-api/5.0/rest-api/index.html#_protocolmapperrepresentation>`_.
To use Protocol Mapper Manager, you need to pass the Realm that you will work with.
We two protocol mappers managers currently, one on Protocol MappersManager and other at Protocol MapperScopesManager.

.. rst-class:: table
.. list-table:: for specifying which namespace and source file of protocol mapper
    :name: appendixes.annotations.covers.tables.annotations
    :header-rows: 1

    * - Class
      - File
    * - ``KeycloakAdmin\ProtocolMappers\ProtocolMapper``
      - src/ProtocolMappers/ProtocolMapper.php




.. _protocol_mappers.list:

List Protocol Mappers
##########################

This method returns a collection of Protocol Mappers of specific client (client scope or client).

Usage
---------

.. code-block:: php

    public function listProtocolMappers()
    {
        $collectionOfProtocolMappers = $this->admin
            ->client('my-realm')
            ->protocolMappers('myClientId')
            ->list();

        foreach ($collectionOfProtocol Mappers as $realm) {
            var_dump($realm->getProtocol Mapper());
        }
    }



.. _protocol_mappers.save:

Save Protocol Mapper
##########################

This method returns will save a new Protocol Mapper on specific client (Client scope or client).

Usage
---------

.. code-block:: php

    public function createProtocolMapper(string $id, string $name)
    {
        $data = [
            'id'   => $id,
            'name' => $name
        ];

        $realm = $this->admin
            ->client('my-realm')
            ->protocolMappers('myClientId')
            ->createFromArray($data)
            ->save();
    }




.. _protocol_mappers.show:

Show Protocol Mapper
##########################

This method returns a Protocol Mapper, you need to pass the parameter realmName, id of client
and must pass the $id of Protocol Mapper.

If Protocol Mapper was not found, you will receive an Exception.

Usage
---------

.. code-block:: php

    public function showProtocolMapper(string $id) : ProtocolMapper
    {
        return $this->admin
            ->client('myRealm')
            ->protocolMappers('myClientId')
            ->show($id);
    }


.. _protocol_mappers.update:

Update Protocol Mapper
##########################

This method will update a Protocol Mapper, an instance of Protocol Mapper must be created
before call to update. This expects at least ``id`` to can update.
In this Library, you  can't update the Protocol Mapper id.

Usage
---------

.. code-block:: php

    public function update(string $id, array $params = []) : Protocol Mapper
    {
        $data = [
            'id' => $id
        ] + $params;

        return $this->admin-
            ->client('myRealm')
            ->protocolMappers('myClientId')
            ->createFromArray($data)
            ->update();
    }


.. _protocol_mappers.delete:

Delete Protocol Mapper
##########################

This method will delete a Protocol Mapper, idOfProtocol Mapper must be passed as parameter.
If an error occurs you will receive an ``Exception`` otherwise, this
is a *void* method

Usage
---------

.. code-block:: php

    public function delete(string $id)
    {
        try {
            $this->admin
                ->client('myRealm')
                ->protocolMappers('myClientId')
                ->delete($id);
        } catch (\Exception $e) {
            var_dump('cant delete this Protocol Mapper, ' . $e->getMessage());
        }
    }

