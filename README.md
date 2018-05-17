SonarQube Server
=========

This role allow to deploy a sonarqube server to a ubuntu system.

Requirements
------------

The database setup needs to be done first. We need a database host, name, user
and password and the user is the owner of the database.

If the var `sonar_dburl` (see below) is not provided then it will use the internal H2 database
and ignore all other database settings. This is for test deployment only.

Role Variables
--------------

- `sonar_version` - Required - Default: 6.7.3 - the current LTS version

- `sonar_download_url` - Required - Default:
  https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-`sonar_version`.zip
  The url to download the sonar archive file

- `sonar_properties` - Optional - Default: No Value. ValueType: multiline string.
  The content of the sonar.properties file. This is sonar server config file.
  The database settings will get prepended to this variable so you do not need
  to provide database settings using this var.

- `sonar_install_dir` - Required. Default: /opt/sonar
  The installation directory for sonar server. This will be a symlink to /opt/sonar-`sonar_version`

- `sonar_download_validate_certs` - Required - Default: true

Database related settings. The sonar.properties file will be included these db
settings. Remember we are not going to create the DB here, the database and
permissions needs to be setup in another role or tasks.

- `sonar_dburl` - Optional - Default: h2. h2 is internal db for testing.
  this is the jdbc database url (sonar.jdbc.url). Sample:
  jdbc:postgresql://localhost/sonar

- `sonar_dbuser` - Required if the `sonar_dburl` is provided - database username.
- `sonar_dbuser_password` - Required if the `sonar_dburl` is provided - database password.

Dependencies
------------


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

Steve Kieu <steve.kieu@xvt.com.au>
