:orphan:

.. _citrix_adc_appfw_confidfield_module:

citrix_adc_appfw_confidfield - Configuration for configured confidential form fields resource.
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. versionadded:: 2.9

.. contents::
   :local:
   :depth: 2

Synopsis
--------
- Configuration for configured confidential form fields resource.




Parameters
----------

.. list-table::
    :widths: 10 10 60
    :header-rows: 1

    * - Parameter
      - Choices/Defaults
      - Comment
    * - comment

        *(str)*
      -
      - Any comments to preserve information about the form field designation.
    * - disabled

        *(bool)*
      - Default:

        *False*
      - When set to ``true`` the state will be set to ``disabled``.

        When set to ``false`` the state will be set to ``enabled``.
    * - fieldname

        *(str)*
      -
      - Name of the form field to designate as confidential.

        Minimum length =  1
    * - instance_ip

        *(added in 2.6.0)*
      -
      - The target Netscaler instance ip address to which all underlying NITRO API calls will be proxied to.

        It is meaningful only when having set ``mas_proxy_call`` to ``true``
    * - isregex

        *(str)*
      - Choices:

          - REGEX
          - NOTREGEX
      - Method of specifying the form field name. Available settings function as follows:

        * REGEX. Form field is a regular expression.

        * NOTREGEX. Form field is a literal string.
    * - mas_proxy_call

        *(bool)*

        *(added in 2.6.0)*
      - Default:

        *False*
      - If true the underlying NITRO API calls made by the module will be proxied through a MAS node to the target Netscaler instance.

        When true you must also define the following options: ``nitro_auth_token``, ``instance_ip``.
    * - nitro_auth_token

        *(added in 2.6.0)*
      -
      - The authentication token provided by a login operation.
    * - nitro_pass
      -
      - The password with which to authenticate to the netscaler node.
    * - nitro_protocol
      - Choices:

          - http (*default*)
          - https
      - Which protocol to use when accessing the nitro API objects.
    * - nitro_timeout
      - Default:

        *310*
      - Time in seconds until a timeout error is thrown when establishing a new session with Netscaler
    * - nitro_user
      -
      - The username with which to authenticate to the netscaler node.
    * - nsip
      -
      - The ip address of the netscaler appliance where the nitro API calls will be made.

        The port can be specified with the colon (:). E.g. 192.168.1.1:555.
    * - save_config

        *(bool)*
      - Default:

        *True*
      - If true the module will save the configuration on the netscaler node if it makes any changes.

        The module will not save the configuration on the netscaler node if it made no changes.
    * - state
      - Choices:

          - present (*default*)
          - absent
      - The state of the resource being configured by the module on the netscaler node.

        When present the resource will be created if needed and configured according to the module's parameters.

        When absent the resource will be deleted from the netscaler node.
    * - url

        *(str)*
      -
      - URL of the web page that contains the web form.

        Minimum length =  1
    * - validate_certs
      - Default:

        *yes*
      - If ``no``, SSL certificates will not be validated. This should only be used on personally controlled sites using self-signed certificates.



Examples
--------

.. code-block:: yaml+jinja
    
    - hosts: citrix_adc
    
      gather_facts: False
      tasks:
        - name: Setup confidential field id
          delegate_to: localhost
          citrix_adc_appfw_confidfield:
            nitro_user: nsroot
            nitro_pass: nsroot
            nsip: 192.168.1.2
            state: present
            fieldname: confidfield_integration_test
            url: 'HTTP.REQ.HOSTNAME.DOMAIN.EQ("blog.example.com")'
            isregex: REGEX
            comment: 'conf id field comment'


Return Values
-------------
.. list-table::
    :widths: 10 10 60
    :header-rows: 1

    * - Key
      - Returned
      - Description
    * - loglines

        *(list)*
      - always
      - list of logged messages by the module

        **Sample:**

        ['message 1', 'message 2']
    * - msg

        *(str)*
      - failure
      - Message detailing the failure reason

        **Sample:**

        Action does not exist
