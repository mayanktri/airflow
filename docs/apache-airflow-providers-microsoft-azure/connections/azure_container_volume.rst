 .. Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

 ..   http://www.apache.org/licenses/LICENSE-2.0

 .. Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.



.. _howto/connection:azure_container_volume:

Microsoft Azure Container Volume Connection
===========================================

The Microsoft Azure Container Volume connection type enables the Azure Container Volume Integrations.

Authenticating to Azure Container Volume
----------------------------------------

There are four ways to connect to Azure Container Volume using Airflow.

1. Use `token credentials
   <https://docs.microsoft.com/en-us/azure/developer/python/azure-sdk-authenticate?tabs=cmd#authenticate-with-token-credentials>`_
   i.e. add specific credentials (client_id, secret) and subscription id to the Airflow connection.
2. Use a `Connection String
   <https://docs.microsoft.com/en-us/azure/data-explorer/kusto/api/connection-strings/storage>`_
   i.e. add connection string to ``connection_string`` in the Airflow connection.

Only one authorization method can be used at a time. If you need to manage multiple credentials or keys then you should
configure multiple connections.

Default Connection IDs
----------------------

All hooks and operators related to Azure Container Volume use ``azure_container_volume_default`` by default.

Configuring the Connection
--------------------------

Login (optional)
    Specify the login used for azure blob storage. For use with Shared Key Credential and SAS Token authentication.

Password (optional)
    Specify the password used for azure blob storage. For use with
    Active Directory (token credential) and shared key authentication.

Host (optional)
    Specify the account url for anonymous public read, Active Directory, shared access key authentication.

Extra (optional)
    Specify the extra parameters (as json dictionary) that can be used in Azure connection.
    The following parameters are all optional:

    * ``connection_string``: Connection string for use with connection string authentication.
    * ``subscription_id``: The ID of the subscription used for the initial connection. This is needed for Azure Active Directory (Azure AD) authentication.
    * ``resource_group``: Azure Resource Group Name under which the desired Azure file volume resides. This is needed for Azure Active Directory (Azure AD) authentication.

When specifying the connection in environment variable you should specify
it using URI syntax.

Note that all components of the URI should be URL-encoded.

For example connect with token credentials:

.. code-block:: bash

   export AIRFLOW_CONN_WASP_DEFAULT='azure_container_volume://blob%20username:blob%20password@myblob.com'
