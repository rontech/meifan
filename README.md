meifan
======

The main repository for meifan net.

----------------------------------------------
Construct the development invironment in Linux.
----------------------------------------------
1. Install JDK for scala
    If you have the openJDK installed defaultly, it is OK to use it. if not, follow the steps below.
    1.1 Download the appropriate JDK for your linux. usually you can just download the newest version without any problems.
        you can prefer the version on the oracle official JDK site and download the JDK, say jdk-8u11-linux-x64.tar.gz 
        
        Of course you can find the address below by just type "JDK downlead" in your search engine like google or baidu.
        but I will list one for example.
        http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
 
    1.2 Unfroze the file you downloaded to the /opt directory.
        tar -zxvf jdk-8u11-linux-x64.tar.gz -C /opt

    1.3 Add JDK variables to the System environment variables.

        $vim /etc/profile
        (you can just add the viriables to the current user by editing the ~/.bash_profile)

        Then add the statements below to the end.

            JAVA_HOME=/opt/jdk1.8.0_11
            PATH=$JAVA_HOME/bin:$PATH
            CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
            export JAVA_HOME
            export PATH
            export CLASSPATH

         Save the /etc/profile file, and load the variables to the system enviromnet immediately.
         $source /etc/profile

     1.4 Verify if JDK is configured rightly.
        Execute the commond below in the commond line.
        $java -version
        
        If you get the message below, you successed.
            java version "1.8.0_11"
            Java(TM) SE Runtime Environment (build 1.8.0_11-b12)
            Java HotSpot(TM) 64-Bit Server VM (build 25.11-b03, mixed mode)

2. Install scala
    Throught the steps of JDK installations, we may find that instead of calling the process "installation",
    maybe we can call it "configuration" more properly. we will do the similar "configuration" with our scala
    and other things necessary.

    2.1 Download the scala, you can just get the latest verson too.
        http://www.scala-lang.org/
        say you get scala-2.11.2.tgz

    2.2 Unfroze the file you downloaded to the /opt directory.
        tar -zxvf scala-2.11.2.tgz -C /opt

    2.3 Add variables to the System environment variables.

        $vim /etc/profile
        (you can just add the viriables to the current user by editing the ~/.bash_profile)

        Then add the statements below to the end.

            SCALA_HOME=/opt/scala-2.11.2
            PATH=$SCALA_HOME/bin:$PATH
            export SCALA_HOME
            export PATH

        Save the /etc/profile file, and load the variables to the system enviromnet immediately.
        $source /etc/profile

    2.4 Verify if JDK is configured rightly.
        type
        $scala version

        you will get the return like below.
           Scala code runner version 2.11.2 -- Copyright 2002-2013, LAMP/EPFL
 
3. Install mongodb and start the mongod service.
    Repeat the similar configuration for mongodb.

    3.1 Download the Mongodb. 
        mongodb-linux-x86_64-2.6.3.tgz

    2.2 Unfroze the file you downloaded to the /opt directory.
        tar -zxvf mongodb-linux-x86_64-2.6.3.tgz -C /opt

    2.3 Add variables to the System environment variables.

        $vim /etc/profile

        Then add the statements below to the end.

            MONGO_HOME=/opt/mongodb-linux-x86_64-2.6.3
            PATH=$MONGO_HOME/bin:$PATH
            export MONGO_HOME
            export PATH

        Save the /etc/profile file, and load the variables to the system enviromnet immediately.
        $source /etc/profile

    2.4 Now we will start the "mongod" service, and access the service with the "mongo" client.
        Firstly, you should create a folder for the mongodb data.
        $mkdir /data/db
        $mongod --dbpath /data/db

        Now you will see the service is started, and type
        $mongo

        you will get the messgae which you can confirm your configuration.

4. Install git.
    We are now fimilar with the "configuration" way to install software in a tar ball format in linux.
    but the is also other more cool way to finish a installation for a usually used software, say git.
       *if you use the REDHAT likes linux, such as CENTOS, you can do it as simply as type the commond below.
           $yum install git
       *if you use the ubuntu, you can type
           $apt-get install git

    and it is all.

5. Config the play invironment.
    Play is based on a lightweight, stateless, web-friendly architecture.
    We will download the 2.2.x not the latest version for now, because when we began the development of our project,
    We used 2.2.x version and it seems that it has had lots of changes when the paly framework updated to the 2.3.x, even, the 2.4.x.

    So just use the legacy 2.2.x before we updating our project when necessary.

    5.1 Download the old version play framework, will see 2.2.6 is the last version of 2.2.x.
        http://www.playframework.com
        We choose play-2.2.6.zip and download it.

    5.2 Unfroze the file you downloaded to the /opt directory.
        $unzip play-2.2.6.zip -d /opt

    5.3 Add variables to the System environment variables.

        $vim /etc/profile

        Then add the statements below to the end.

            PLAY_HOME=/opt/play-2.2.6
            PATH=$PLAY_HOME:$PATH
            export PLAY_HOME
            export PATH

         Save the /etc/profile file, and load the variables to the system enviromnet immediately.
         $source /etc/profile

     5.4 Verify if play is configured rightly.
        type
        $play

        you will get the return like below.
                  _
            _ __ | | __ _ _  _
           | '_ \| |/ _' | || |
           |  __/|_|\____|\__ /
           |_|            |__/

           play 2.2.6 built with Scala 2.10.3 (running Java 1.8.0_11), http://www.playframework.com

6. Download the latest version of our project.

7. Start the [database] project and load the init data.
    For now, we must start our database subproject and access it to load the sample data initiallly.
    $cd database
    $play
    $run

    If this is the first time you execute this project in you invironment, the play will download the necessary plugins for us automatically.
    you may wait for some minuts, more or less according to the status of your network.

    Now, when it is finished downloading all assosiated things, do access the address below to load the sample data.
    (the data will be loaded to the mongodb only when you access the database site firstly.)
    http://localhost:90000

    Then close the database play run use [ctrl + C] after you seeing the welcome page of database.

8. Start the [portal] project for normal user access.
    $cd portal
    $play
    $run

    you will get this done soon base on the work you did for the database initialization.
    now, if you access the address, you will see what a normal user see of our site.

    http://localhost:9000 

9. Start the [manager] project for admin user access.
   so, if you are in the roles of some types of administrator, you need to start the manager project.
   $cd  manager
   $play
   $run

   access the site below.
   http://localhost:9000
 
   But before you login into the system, we have to remind you once again:
   We trust you have received the usual lecture from the local System Administrator.
   It usually boils down to these three things:
    1) Respect the privacy of others.
    2) Think before you type.
    3) With great power comes great responsibility. 

10. etc.
    The configuration steps for Windows is below portal/doc.

--------------------------------------
About the deploy environment
--------------------------------------
1. Jenkins




