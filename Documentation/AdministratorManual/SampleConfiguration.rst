.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../Includes.txt


.. _admin-manual-sample:

Sample Configuration
--------------------

`Forum Systems <http://www.forumsys.com>`_ is providing a free online LDAP test server that you can use for testing.
If all you need is to test connectivity and do a proof of concept of connecting TYPO3 with an LDAP server, this is the
right place to eliminate the need to download, install and configure an LDAP server just for testing.
`read more <http://www.forumsys.com/tutorials/integration-how-to/ldap/online-ldap-test-server/>`_.


.. only:: html

	**Sections:**

	.. contents::
		:local:
		:depth: 1


.. _admin-manual-sample-ldap:

LDAP
^^^^

=================================== ===========================================
Option                              Value
=================================== ===========================================
Server Type                         OpenLDAP
Host                                ldap.forumsys.com
Port                                389
Bind DN                             cn=read-only-admin,dc=example,dc=com
Password                            password
Relation between groups and users   Group contains the list of its members
=================================== ===========================================


.. _admin-manual-sample-beusers:

BE_USERS
^^^^^^^^

=================================== ===========================================
Option                              Value
=================================== ===========================================
Base DN                             dc=example,dc=com
Filter                              (uid={USERNAME})
Mapping                             | email = <mail>
                                    | realName = <cn>
                                    | tstamp = {DATE}
                                    | *admin = 1*
=================================== ===========================================

.. warning::
	In this example, the last mapping line will automatically promote every LDAP user as TYPO3 administrator. This
	should of course be enabled only for quick testing without having to bother with available modules.


.. _admin-manual-sample-begroups:

BE_GROUPS
^^^^^^^^^

=================================== ===========================================
Option                              Value
=================================== ===========================================
Base DN                             dc=example,dc=com
Filter                              (&(uniqueMember={USERDN})(ou=*))
Mapping                             | title = <cn>
                                    | tstamp = {DATE}
=================================== ===========================================


.. _admin-manual-sample-testusersgroups:

Test Users and Groups
^^^^^^^^^^^^^^^^^^^^^

As of August 2014, three groups and a few users are available:

- Mathematicians

  - euclid
  - euler
  - gauss
  - riemann

- Scientists

  - einstein
  - galieleo
  - newton
  - tesla

- Italians

  - tesla

.. note:: All user passwords are "password".