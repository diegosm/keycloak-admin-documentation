.. _users_manager:

=============================
Users Manager
=============================
.. _users_manager.representation:

User Class
#######################

The class ``User`` is a
`User Representation  <https://www.keycloak.org/docs-api/5.0/rest-api/index.html#_userrepresentation>`_.
To use User Manager, you need to pass the Realm that you will work with.

.. rst-class:: table
.. list-table:: for specifying which namespace and source file of user
    :name: appendixes.annotations.covers.tables.annotations
    :header-rows: 1

    * - Class
      - File
    * - ``KeycloakAdmin\Users\User``
      - src/Users/User.php


.. _users_manager.list:

List Users
##########################

This method returns a collection of Users of specific Realm.

Usage
---------

.. code-block:: php

    public function listUsers()
    {
        $collectionOfUsers = $this->admin
            ->user('my-realm')
            ->list();

        foreach ($collectionOfUsers as $user) {
            var_dump($user->getName());
        }
    }



.. _users_manager.save:

Save User
##########################

This method returns will save a new User on specific Realm.
Must have at least username, in their API this field is optional, but in truth is required.

Usage
---------

.. code-block:: php

    public function createUser(string $id, string $name, string $username)
    {
        $myUser = [
            'id'   => $id,
            'name' => $name,
            'username' => 'myusername'
        ];

        $user = $this->admin->user('my-realm')
            ->createFromArray($myUser)
            ->save();
    }




.. _users_manager.show:

Show User
##########################

This method returns a User, you need to pass the parameter realmName and must pass the $id.
If User was not found, you will receive an Exception.

Usage
---------

.. code-block:: php

    public function showUser(string $id) : Client
    {
        return $this->admin->user('my-realm')
            ->show($id);
    }


.. _users_manager.update:

Update User
##########################

This method will update a User, an instance of User must be created
before call to update. This expects at least ``id`` to can update.
In this Library, you  can't update the User id.

Usage
---------

.. code-block:: php

    public function update(string $id, array $params = []) : Client
    {
        $data = [
            'id' => $id
        ] + $params;

        return $this->admin->user('my-realm')
            ->createFromArray($data)
            ->update();
    }


.. _users_manager.delete:

Delete User
##########################

This method will delete a User, id must be passed as parameter.
If an error occurs you will receive an ``Exception`` otherwise, this
is a *void* method

Usage
---------

.. code-block:: php

    public function delete(string $id)
    {
        try {
            $this->admin->user('my-realm')
            ->delete($id);
        } catch (\Exception $e) {
            var_dump('cant delete this client, ' . $e->getMessage());
        }
    }




.. _users_manager.reset_password:

Reset Password
##########################

This method will reset a User Password, id must be passed as parameter.
If an error occurs you will receive an ``Exception`` otherwise, this
is a *void* method

Usage
---------

.. code-block:: php

    public function changePass(string $id, string $value)
    {
        $json = '{ "type": "password", "temporary": false, "value": "' . $value . '" }';

        try {
            $this->admin->user('my-realm')
            ->resetPassword($id)
            ->createFromJson($json)
            ->save()
        } catch (\Exception $e) {
            var_dump('cant change this user password, ' . $e->getMessage());
        }
    }




.. _users_manager.logout:

Logout
##########################

This method will logout all User sessions. Pass Id as parameter.

Usage
---------

.. code-block:: php

    public function logout(string $id)
    {
        $this->admin->user('my-realm')->logout($id);
    }
