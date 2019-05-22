#####################################################################
#                                                                   #
#                   A T L A S S I A N :   J I R A                   #
#                                                                   #
#####################################################################



# Info
* Source: https://confluence.atlassian.com/adminjiraserver/connecting-jira-applications-to-mysql-5-7-966063305.html#ConnectingJiraapplicationstoMySQL5.7-configurejirawithdatabase
* {Jira-installation-directory} -} /var/atlassian/application-data/jira



# Install Jira

## 1. Download Installer
* Jira Core at https://www.atlassian.com/software/jira/core/download
* Jira Software at https://www.atlassian.com/software/jira/download
* Jira Service Desk at https://www.atlassian.com/software/jira/service-desk/download

## 2. Make the installer executable
  Change to the directory where you downloaded

  ```
  sudo chmod a+x atlassian-jira-core-X.X.X-x64.bin
  sudo chmod a+x atlassian-jira-software-X.X.X-x64.bin
  sudo chmod a+x atlassian-servicedesk-X.X.X-x64.bin
  ```

## 3. Run the installer
  ```
  sudo ./atlassian-jira-core-X.X.X-x64.bin
  sudo ./atlassian-jira-software-X.X.X-x64.bin
  sudo ./atlassian-servicedesk-X.X.X-x64.bin
  ```

## 4. Copy mySQL connector in lib-folder
  download from https://dev.mysql.com/downloads/connector/j/5.1.html
  copy into {Jira-installation-directory}/lib
  copy into /opt/atlassian/confluence/confluence/WEB-INF/lib

## 5. Port independent forwarding
  ```
  touch .htaccess
  vi .htaccess
  ```
  edit with:
  ```
  RedirectPermanent / http://jira.{computer_name_or_IP_address}:{port}
  ```

## 6. Start using Jira
  ```
  http://{computer_name_or_IP_address}:{port}
  ```



# Uninstall Jira

## 1. Change directory to your installation directory.
  ```
  cd /opt/atlassian/jira/
  sudo ./uninstall
  delete /opt/atlassian/jira/
  delete /var/atlassian/application-data/jira/
  ```



# Mapping Commands

## 1. Change directory to your installation directory.
  SOURCE: https://www.tecmint.com/install-and-configure-apache-tomcat-8-in-linux/
  ```
  cd /opt/atlassian/jira/bin
  sudo chmod 700 /opt/atlassian/jira/bin/start-jira.sh
  sudo chmod 700 /opt/atlassian/jira/bin/stop-jira.sh
  ln -s /opt/atlassian/jira/bin/start-jira.sh /usr/bin/jirastart
  ln -s /opt/atlassian/jira/bin/stop-jira.sh /usr/bin/jirastop
  ls -l jirastart
  ls -l jirastop
  ```

  ...
  ```
  ln -s /opt/atlassian/jira-service-desk/bin/start-jira.sh /usr/bin/jiraservicedeskstart
  ln -s /opt/atlassian/jira-service-desk/bin/stop-jira.sh /usr/bin/jiraservicedeskstop
  ...
  cd /opt/atlassian/confluence/bin
  sudo chmod 700 /opt/atlassian/confluence/bin/start-confluence.sh
  sudo chmod 700 /opt/atlassian/confluence/bin/stop-confluence.sh
  ln -s /opt/atlassian/confluence/bin/start-confluence.sh /usr/bin/confluencestart
  ln -s /opt/atlassian/confluence/bin/stop-confluence.sh /usr/bin/confluencestop
  ```




# Troubleshooting

## A) start / stop services
  ```
  sudo /etc/init.d/jira stop
  sudo /etc/init.d/jira start

  sudo /etc/init.d/jira1 stop
  sudo /etc/init.d/jira1 start

  sudo /etc/init.d/confluence stop
  sudo /etc/init.d/confluence start
  ```

## B) mySQL general
  ```
  sudo /etc/init.d/mysql stop
  etc/mysql/my.cnf =} edit
    default-storage-engine=INNODB
    character_set_server=utf8mb4
    innodb_default_row_format=DYNAMIC
    innodb_large_prefix=ON
    innodb_file_format=Barracuda
    innodb_log_file_size=2G
    // remove the next line if it exists
    sql_mode = NO_AUTO_VALUE_ON_ZERO
    // for confluence
    transaction-isolation=READ-COMMITTED
  sudo /etc/init.d/mysql start
  ```

## C) mySQL new Connection
  ```
  delete /var/atlassian/application-data/jira/bin/dbconfig.xml
  delete /var/atlassian/jira/dbconfig.xml
  cd /opt/atlassian/jira/bin -} sudo ./config.sh
  ```





#####################################################################
#                                                                   #
#             A T L A S S I A N :   C O N F L U E N C E             #
#                                                                   #
#####################################################################

https://confluence.atlassian.com/doc/integrating-jira-and-confluence-2825.html
https://confluence.atlassian.com/doc/add-ons-and-integrations-720410414.html

https://confluence.atlassian.com/doc/configuring-jira-integration-in-the-setup-wizard-242255467.html
https://confluence.atlassian.com/doc/connecting-to-crowd-or-jira-for-user-management-229838465.html
https://confluence.atlassian.com/doc/linking-to-another-application-360677690.html
