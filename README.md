# Deploy Nexus Repository Manager :technologist:	
Step by step guid to deploy Nexus Repository Manager on a server
### Access a server terminal as root:
1 - Update server packages 
      
      apt update
2 - Install OpenJDK 8 JRE

      apt install openjdk-8-jre-headless
     
3 - Go to /opt directory to keep the system's file hierarchy clean and separate from the operating system files

      cd /opt
4 - Download the latest version of Nexus 3, our popular repository manager, in the form of a compressed tarball file

      wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
5 - Extract the contents of a compressed tarball file that was downloaded ---> `nexus-3.28.1-01` & `sonatype-work`

      tar -zxvf latest-unix.tar.gz
      
6 - Create dedicated `nexus user` with minimal permissions

      adduser nexus
7 - Change the ownership of the "nexus-3.28.1-01" & "sonatype-work" directories and all its contents recursively to the user and group "nexus"

      chown -R nexus:nexus nexus-3.28.1-01
      chown -R nexus:nexus sonatype-work
8 - Edit nexus configuration file `nexus.rc` to set `run_as_user` to `nexus user` indicating that the service should be run under the user account named "nexus"

      vi nexus-3.28.1-01/bin/nexus.rc
      run_as_user="nexus"
9 - Start the Nexus Repository Manager service

      su - nexus
      /opt/nexus-3.28.1-01/bin/nexus start
10 - Finally to check if the Nexus Repository Manager process is running, what ports it is listening on, and if there are any network connectivity issues.
 
      exit                                    ---> to become root again
      apt install net-tools
      su - nexus
      ps aux | grep nexus                     ---> check nexus process
      netstat -lnpt                           ---> check nexus port to access it
11 - **While the process is running and we have the port it is listening on you can access it successfully :tada::tada:**
      
