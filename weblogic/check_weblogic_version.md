# How to find Oracle WebLogic Server Version?
Today one of my customer asked me the way to find out weblogic server version which they have installed so thought to share details with you as well.

There are different ways to determine Oracle Weblogic Service Version. Use one of the following method to find weblogic server version.

## 1. We can determine weblogic server version using registry.xml file:
Location in WLS 12.2.1.3:
$ORACLE_HOME/inventory/registry.xml

<distribution status="installed" name="WebLogic Server" version="12.2.1.3.0">

e.g.
/u02/oracle12213/oracle_home/middleware/inventory/registry.xml

<?xml version = '1.0' encoding = 'UTF-8' standalone = 'yes'?>
<registry home="/u02/oracle12213/oracle_home/middleware" platform="226" sessions="5" xmlns:ns2="http://xmlns.oracle.com/cie/gdr/dei" xmlns:ns3="http://xmlns.oracle.com/
cie/gdr/nfo" xmlns="http://xmlns.oracle.com/cie/gdr/rgy">
   <distributions>
      <distribution status="installed" name="WebLogic Server" version="12.2.1.3.0">
         <sessions>
            <session id="1" date="2017-10-21T17:53:51.433+05:30" action="install"/>
         </sessions>
         <features>
            <feature status="installed" name="cieCfg_wls_shared_external" version="12.2.1.3.0">
               <sessions>

## 2. We can user weblogic.jar file (weblogic.version class) to find weblogic server version:
Go to $WLS_HOME/server/lib
e.g. For WLS 12.2.1.3
/u02/oracle12213/oracle_home/middleware/wlserver/server/lib

Use below command to find weblogic and it's component version,
java -cp weblogic.jar weblogic.version -verbose

e.g.
[oracle@demomachine lib]$ java -cp weblogic.jar weblogic.version -verbose

WebLogic Server 12.2.1.3.0 Thu Aug 17 13:39:49 PDT 2017 1882952 ImplVersion: 12.2.1.3.0
Oracle Security Developer Tools Security Engine ImplVersion: 3.1.0
Oracle Security Developer Tools Crypto ImplVersion: 3.1.0
Oracle Universal Connection Pool ImplVersion: 12.2.0.1.0
WebLogic Config External  Thu Aug 10 00:41:12 UTC 2017 ImplVersion: 8.6.0.0
WebLogic Application Descriptors ImplVersion: 12.2.1.3
WebLogic Application Descriptors Bindings ImplVersion: 12.2.1.3
WebLogic Application Container ImplVersion: 12.2.1.3
WebLogic Utility Classloader implementations ImplVersion: 12.2.1.3
WebLogic Descriptors for J2EE ImplVersion: 12.2.1.3
WebLogic Beangen ImplVersion: 12.2.1.3
WebLogic BeanInfo Caching and Discovery ImplVersion: 12.2.1.3
WebLogic Descriptor ImplVersion: 12.2.1.3
WebLogic Beangen ImplVersion: 12.2.1.3
WebLogic Coherence Descriptor ImplVersion: 12.2.1.3
WebLogic Coherence Api ImplVersion: 12.2.1.3
WebLogic Coherence App Descriptor ImplVersion: 12.2.1.3
WebLogic Coherence Integration ImplVersion: 12.2.1.3
WebLogic Workarea ImplVersion: 12.2.1.3
WebLogic Nodemanager Plugin ImplVersion: 12.2.1.3
WebLogic RMI ImplVersion: 12.2.1.3
WebLogic Timers ImplVersion: 12.2.1.3
WebLogic Channels API ImplVersion: 12.2.1.3
WebLogic Channels ImplVersion: 12.2.1.3
WebLogic Channels API ImplVersion: 12.2.1.3
WebLogic Socket Muxer API ImplVersion: 12.2.1.3
WebLogic java compiler utils package ImplVersion: 12.2.1.3
WebLogic Utils for working with Expressions ImplVersion: 12.2.1.3
WebLogic Utils ImplVersion: 12.2.1.3
WebLogic Utils ImplVersion: 12.2.1.3
WebLogic Utils for Dynamically Generated Class Wrappers ImplVersion: 12.2.1.3
WebLogic Work Manager ImplVersion: 12.2.1.3
WebLogic Datasource ImplVersion: 12.2.1.3
WebLogic RAC Module UCP ImplVersion: 12.2.1.3
WebLogic Resource Pool ImplVersion: 12.2.1.3
WebLogic Diagnostics Base ImplVersion: 12.2.1.3
WebLogic Diagnostics Core Interfaces ImplVersion: 12.2.1.3
WebLogic Diagnostics JRockit Flight Recorder Interfaces ImplVersion: 12.2.1.3
WebLogic i18n Build Support ImplVersion: 12.2.1.3
WebLogic i18n Runtime Support ImplVersion: 12.2.1.3
WebLogic I18N tools ImplVersion: 12.2.1.3
WebLogic Diagnostics Instrumentor Config Tool ImplVersion: 12.2.1.3
WebLogic Diagnostics Instrumentor Tool ImplVersion: 12.2.1.3
WebLogic Diagnostics Logging ImplVersion: 12.2.1.3
WebLogic Diagnostics Query Module ImplVersion: 12.2.1.3
WebLogic EJBGen ImplVersion: 12.2.1.3
WebLogic Messaging Kernel ImplVersion: 12.2.1.3
WebLogic JMS Pool ImplVersion: 12.2.1.3
WebLogic Security Provider Generation Tool ImplVersion: 12.2.1.3
WebLogic Domain Binding ImplVersion: 12.2.1.3
WebLogic Management Core Interfaces ImplVersion: 12.2.1.3
WebLogic Management EventBus Interfaces ImplVersion: 12.2.1.3
WebLogic Management JMX Interfaces ImplVersion: 12.2.1.3
Oracle Cooperative Memory Management Lower Tier ImplVersion: 12.2.1.3
WebLogic EclipseLink Integration ImplVersion: 12.2.1.3
WebLogic SCA Client ImplVersion: 12.2.1.3
WebLogic security network connection filter classes ImplVersion: 12.2.1.3
WebLogic security ssl classes ImplVersion: 12.2.1.3
WebLogic Spring Instrument Tool ImplVersion: 12.2.1.3
WebLogic Store ImplVersion: 12.2.1.3
WebLogic Store Admin Tool ImplVersion: 12.2.1.3
WebLogic STORE GXA ImplVersion: 12.2.1.3
WebLogic JDBC Store ImplVersion: 12.2.1.3
WebLogic JTA implementation ImplVersion: 12.2.1.3
WebLogic WebApp Container Public API ImplVersion: 12.2.1.3
WebLogic Servlet ImplVersion: 12.2.1.3
WebLogic Http Pub/Sub Module ImplVersion: 12.2.1.3
WebLogic SAAJ ImplVersion: 12.2.1.3
WebLogic STAX ImplVersion: 12.2.1.3
WebLogic Jersey Common Integration ImplVersion: 12.2.1.3
WebLogic Jersey Client Integration ImplVersion: 12.2.1.3
WebLogic JAX-RS 2.0 Portable Server / Jersey 2.x integration module ImplVersion: 12.2.1.3
WebLogic XML XPath Implementation ImplVersion: 12.2.1.3
OPatch Patches:
No patches installed

SERVICE NAME                    VERSION INFORMATION
============                    ===================
Web Services Execution Engine   1.0
Managed Beans Container         1.0
Post Admin Singleton Services   1.0
Pre Admin Singleton Services S  1.0
Singleton Services Batch Manag  1.0
Kernel                          Commonj WorkManager v1.1
CorbaService                    CORBA 2.3, IIOP 1.2, RMI-IIOP SFV2, OTS 1.2, CSIv2 Level 0 + Stateful
TimerService                    Commonj TimerManager v1.1
JDBCService                     JSR-221, JDBC 4.0
Enterpise Java Beans Container  EJB 3.2
CustomResourceServerService     1.0.0.0
Transaction Service             JTA 1.1
Transaction Stop Service        JTA 1.1
Servlet Container               Servlet 3.1, JSP 2.3
XMLService                      XML 1.1

[oracle@demomachine lib]$

## 3. We can find weblogic server version from check the AdminServer.log file:
Go to $DOMAIN_HOME/servers/AdminServer/logs
Check AdminServer.log file for weblogic server version

e.g.
####<Oct 24, 2017 3:39:16,238 PM IST> <Info> <WebLogicServer> <demomachine> <> <Thread-10> <> <> <> <1508839756238> <[severity-value: 64] [partition-id: 0] [partition-name: DOMAIN] > <BEA-000214> <WebLogic Server "AdminServer" version: WebLogic Server 12.2.1.3.0 Thu Aug 17 13:39:49 PDT 2017 1882952 Copyright (c) 1995,2017, Oracle and/or its affiliates. All rights reserved.>

## 4. We can use WLST to check weblogic server version:
Go to $ORACLE_HOME/oracle_common/bin
Invoke wlst.sh
Use command print version

e.g.
wls:/offline> print version
WebLogic Server 12.2.1.3.0
wls:/offline>

## 5. We can use admin console to check weblogic server version:
Login to WebLogic Admin Console and navigate to Servers => AdminServer => Monitoring tab
This page will have weblogic version details.
OR
When you open Admin console, version will be displayed at the bottom of the welcome page.

e.g.
WebLogic Server Version: 12.2.1.3.0
Copyright (c) 1996,2017, Oracle and/or its affiliates. All rights reserved.
