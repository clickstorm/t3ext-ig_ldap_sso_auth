.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt


.. _admin-manual-begroups:
.. _admin-manual-fegroups:

BE_GROUPS and FE_GROUPS
-----------------------

The fourth and sixth tabs can be fill exactly the same way. The only difference between them is that BE\_GROUPS stores
the configurations for the backend LDAP usergroup association and FE\_GROUPS stores the configurations for the frontend
LDAP user group association. You will only fill the sections you need, BE\_GROUPS if you need backend authentication and
FE\_GROUPS if you need frontend authentication. You can skip this entire section if you just want to validate the
authentication and do not want to use groups from LDAP.

- **Base DN:** Full DN path of the directory containing all the groups that are related to your LDAP users and you want
  to use in your TYPO3 website.

  **Example:**

  ::

      ou=groups,dc=example,dc=com

- **Filter:** To be used to add restrictions that allow you to exclude objects from specific properties. The
  syntax used in this field is the standard LDAP search syntax.

  This field should not be left empty although it is not marked as required. Be sure to always double-check your configuration
  using the wizard in the backend module.

  **Example:**

  ::

      (objectClass=posixGroup)

  .. note::
      The string ``{USERDN}`` will be substituted by the Distinguished Name (DN) of the authenticated user, the
      string ``{USERUID}`` will be substituted by the uid attribute of the authenticated user.

  .. hint::
      When using OpenLDAP, the group membership is usually stored within attribute ``memberUid`` of the group itself,
      and not within attribute ``memberOf`` of the user. In order to properly retrieve and associate groups for the
      user, you should use a filter of the form::

          (&(memberUid={USERUID})(objectClass=posixGroup))

  .. warning::
      When using ActiveDirectory, you typically set the option ``Relation between groups and users`` to
      ``User contains the list of its associated groups`` If so, you **must** add a line mapping the "usergroup" for
      your user. This mapping *will not* be actually used by TYPO3 but will let the LDAP engine known which attribute is
      used to evalue the group membership.

      Example::

          usergroup=<memberOf>

      **Important:** This is a user mapping instruction.

      If you forget to do so, every group in LDAP will be imported to TYPO3 **and** your user will be a member of each
      and every one.

- **Mapping:** Used to fetch other attributes form the LDAP server that we would like groups to have. Please see
  syntax and examples in :ref:`admin-manual-beusers`.