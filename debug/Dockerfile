FROM almalinux:9
#install telnet,inputils and net-tools to check the connectivity of the application and bind-utils 
#to check the port on which the application is running.
#need curl to check the application is running or not
#RUN dnf install telnet -y && dnf install net-tools -y && dnf install bind-utils -y && dnf install which -y && dnf install curl -y

RUN dnf install -y telnet net-tools bind-utils which curl --allowerasing

CMD ["sleep","2000"]