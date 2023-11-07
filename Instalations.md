# CLoud digital ocean 

- https://www.digitalocean.com/?refcode=98ed549bfab5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=CopyPaste

# Commands : SetUp Machine & Install Jenkins
1. Verify Installed Java Version

java -version
(Only Java8 or Java11 are recommended)



2. Install Java 8 on Ubuntu Machine

sudo apt-get -y install openjdk-8-jdk openjdk-8-jre

java -version



3. Set JAVA_HOME Variables

cat >> /etc/environment <<EOL
JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
JRE_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
EOL


4. First, add the repository key to the system

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -



5. Next, append the Debian package repository address to the server’s sources.list

sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'



6. Update System packages

sudo apt update



7. Install Jenkins and its dependencies

sudo apt -y install jenkins



8. Start Jenkins using systemctl

sudo systemctl start jenkins



9. Get Service Status

sudo systemctl status jenkins



10. Enable Jenkins Service

sudo systemctl enable jenkins



11. Use the cat command to display the password:

sudo cat /var/lib/jenkins/secrets/initialAdminPassword


# Text Direction : Download and Configure Jenkins on Windows
Install Java on Windows Machine
Step 0: Un-Install Older Version(s) of JDK/JRE

I recommend that you install only the latest JDK. Although you can install multiple versions of JDK/JRE concurrently, it is messy.

If you have previously installed older version(s) of JDK/JRE, un-install ALL of them. Goto "Control Panel" ⇒ "Programs" ⇒ "Programs and Features" ⇒ Un-install ALL programs begin with "Java", such as "Java SE Development Kit ...", "Java SE Runtime ...", "Java X Update ...", and etc.



Step 1: Download JDK

Goto Java SE download site @ http://www.oracle.com/technetwork/java/javase/downloads/index.html.

Under "Java Platform, Standard Edition" ⇒ "Java SE 8.0.{x}", where {x} denotes a fast running update number ⇒ Click the JDK's "Download" button.

Under "Java SE Development Kit 8.0.{x}" ⇒ Check "Accept License Agreement".

Choose the JDK for your operating system, i.e., "Windows" (for 64-bit Windows OS), and download the installer (e.g., "jdk-8.0.{x}_windows-x64_bin.exe" - 283MB).



Step 2: Install JDK and JRE

Run the downloaded installer (e.g., "jdk-8.0.{x}_windows-x64_bin.exe"), which installs both the JDK and JRE.

By default:

JDK is installed in directory "C:\Program Files\Java\jdk-8.0.{x}", where {x} denotes the upgrade number; and

JRE is installed in "C:\Program Files\Java\jre-8.0.{x}".

Notes: In 64-bit Windows, "Program Files" is meant for 64-bit programs; while "Program Files (x86)" for 32-bit programs.

Accept the defaults and follow the screen instructions to install JDK and JRE.

Use the "File Explorer", goto "C:\Program Files\Java" to inspect these folders. Take note of your JDK installed directory, in particular, the varying upgrade number, which you will need in the next step.

In the following diagram, the JDK installed directory is "C:\Program Files\Java\jdk-8.0.1", where {x}=1. I shall refer to the JDK installed directory as <JAVA_HOME>, hereafter, in this article.



Step 3: Include JDK's "bin" Directory in the PATH

Windows' Shell searches the current directory and the directories listed in the PATH environment variable (system variable) for executable programs. JDK's programs (such as Java compiler javac.exe and Java runtime java.exe) reside in the sub-directory "bin" of the JDK installed directory. You need to include "bin" in the PATH to run the JDK programs.

To edit the PATH environment variable in Windows 7/8/10:

Launch "Control Panel" ⇒ (Optional) System and Security ⇒ System ⇒ Click "Advanced system settings" on the left pane.

Switch to "Advanced" tab ⇒ Push "Environment Variables" button.

Under "System Variables" (the bottom pane), scroll down to select "Path" ⇒ Click "Edit...".

For Windows 10 (newer releases):
You shall see a TABLE listing all the existing PATH entries (if not, goto next step). Click "New" ⇒ Enter the JDK's "bin" directory "c:\Program Files\Java\jdk-8.0.{x}\bin" (Replace {x} with your installation number!!!) ⇒ Select "Move Up" to move this entry all the way to the TOP.

Prior to newer Windows 10:
(CAUTION: Read this paragraph 3 times before doing this step! Don't push "Apply" or "OK" until you are 101% sure. There is no UNDO!!!)
(To be SAFE, copy the content of the "Variable value" to Notepad before changing it!!!)
In "Variable value" field, INSERT "c:\Program Files\Java\jdk-8.0.{x}\bin" (Replace {x} with your installation number!!!) IN FRONT of all the existing directories, followed by a semi-colon (;) which separates the JDK's bin directory from the rest of the existing directories. DO NOT DELETE any existing entries; otherwise, some existing applications may not run.

Variable name  : PATHVariable value : c:\Program Files\Java\jdk-8.0.{x}\bin;[do not delete exiting entries...]
Notes: Starting from JDK 1.8, the installation created a directory "c:\ProgramData\Oracle\Java\javapath" and added to the PATH. It contains only JRE executables (java.exe, javaw.exe, and javaws.exe), but NOT the JDK executables (e.g., javac.exe).



Step 4: Verify the JDK Installation

Launch a CMD shell via one of the following means:

Click "Search" button ⇒ Enter "cmd" ⇒ Choose "Command Prompt", or

right-click "Start" button ⇒ run... ⇒ enter "cmd", or

(Prior to Windows 10) click "Start" button ⇒ All Programs ⇒ Accessories (or Windows System) ⇒ Command Prompt, or

(Windows 10) click "Start" button ⇒ Windows System ⇒ Command Prompt.

Issue the following commands to verify your JDK installation:

Issue "path" command to list the contents of the PATH environment variable. Check to make sure that your <JAVA_HOME>\bin is listed in the PATH.
Don't type prompt>, which denotes the command prompt!!! Key in the command (highlighted) only.

// Display the PATH entriesprompt> pathPATH=c:\Program Files\Java\jdk-8.0.{x}\bin;[other entries...]
Issue the following commands to verify that JDK/JRE are properly installed and display their version:

// Display the JRE versionprompt> java -versionjava version "1.8.0_151"Java(TM) SE Runtime Environment (build 1.8.0_151-b12)Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)


Start Jenkins on Windows
1. Go to Directory, where you have kept your Jenkins.war file

2. Execute Command :

java -jar jenkins.war --httpPort={Port_number}

# Text Direction : Download and Configure Jenkins on MAC OS
Install Java 8 on MAC OS


Step 1: Check if JDK has been Pre-Installed

In some Mac systems (earlier than Mac OS X 10.7), JDK has been pre-installed. To check if JDK has been installed, open a "Terminal" (Search "Terminal"; or Finder ⇒ Go ⇒ Utilities ⇒ Terminal) and issue this command:

javac -version
If a JDK version number is returned (e.g., JDK x.x.x), then JDK has already been installed. If the JDK version is prior to 1.8, proceed to Step 2 to install the latest JDK; otherwise, proceed to "Step 3: Write a Hello-world Java program".

If message "command not found" appears, JDK is NOT installed. Proceed to the "Step 2: Install JDK".

If message "To open javac, you need a Java runtime" appears, select "Install" and follow the instructions to install JDK. Then, proceed to "Step 3: Write a Hello-world Java program".



Step 2: Download JDK

Goto Java SE download site @ http://www.oracle.com/technetwork/java/javase/downloads/index.html. Under "Java Platform, Standard Edition" ⇒ "Java SE 10.0.{x}" ⇒ Click the JDK's "Download" button.

Check "Accept License Agreement".

Choose your operating platform, i.e., MacOS. Download the installer (e.g, jdk-1.8.0.{x}_osx-x64_bin.dmg - 395MB).



Step 3: Install JDK/JRE

Double-click the downloaded Disk Image (DMG) file. Follow the screen instructions to install JDK/JRE.

Eject the DMG file.

To verify your installation, open a "Terminal" and issue these commands.

// Display the JDK versionjavac -versionjavac 10.0.{x} // Display the JRE versionjava -versionjava version "10.0.{x}"...... // Display the location of Java Compilerwhich javac/usr/bin/javac // Display the location of Java Runtimewhich java/usr/bin/java


Start Jenkins on Mac OS
1. Open terminal and execute command

java -jar ~/path-to-jenkins-war/jenkins.war -httpPort={Port_Num}



# Maven 
## Text Direction : Install Maven on Windows
Step 1) Install JDK and Add ‘JAVA_HOME’ Environment Variable
To install java, download the JDK installer and add/update the JAVA_HOME variable to the JDK installation folder.



Step 2) Download Maven and add ‘MAVEN_HOME’ and ‘M2_HOME’ Environment Variables
Maven can be downloaded from this location. I have extracted it in location – D:/Latest Setup/apache-maven-3.0.4. You can choose your own location.

Set the M2_HOME and MAVEN_HOME variable to the maven installation folder.



Step 3) Include ‘maven/bin’ directory in ‘PATH’ variable
To run maven from the command prompt, this is necessary. Update the PATH variable with 'Maven-installation/bin' directory.



Step 4) Verify maven in console
Maven installation is complete. Now let's test it from the windows command prompt.

Go to the start menu and type in the application location search box.

Press ENTER. A new command prompt will be opened.

Type mvn -version in command prompt and hit ENTER.

Console $ mvn --version



This should show the version information of the maven installed. If there is any error shown, cross-check all the above steps.

In this tutorial, we learned how to install maven on windows.

# Text Direction : Create and Configure Jenkins Slave
Install Jenkins Agent on the Slave Node


Running on the master node:

sudo -iu jenkins
ssh root@<slave_ip> mkdir -p .ssh
cat .ssh/id_rsa.pub | ssh root@<slave_ip> 'cat >> .ssh/authorized_keys'


Running on slave node:

mkdir bin
cd bin
wget http://<master_ip>:8080/jnlpJars/slave.jar


Verify and Install Java:

java -version
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt install openjdk-8-jdk


Start Slave Agent Command:

ssh root@<slave_ip> java -jar /root/bin/slave.jar



Trouble Shooting
If you don't see the "Launch agent via execution of command on master" option in the add slave page. This is due to the fact that the latest version of Jenkins has removed that option from the default install and moved it to this plugin: https://plugins.jenkins.io/command-launcher

The solution is to install the command-launcher Jenkins plugin first before you can add a slave.