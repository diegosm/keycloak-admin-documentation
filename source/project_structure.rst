.. _project_structure:

=============================
Project Structure
=============================

Almost every resource from API has a structured folder with their representations and managers.

.. _project_structure.resources:

Resources
#######################

All folders, except Utils and Keycloak, are a representation of API resource. Each of this folders
can have one or more managers and their exceptions.

Some of these resources are shared, in example Credentials, so these case it will have only a representation.




.. _project_structure.entities:

KeycloakAdmin Definitions
###########################

As I told before, in our resources we have representation classes.

Example
src/Clients/Client.php
src/Credentials/CredentialRepresentation