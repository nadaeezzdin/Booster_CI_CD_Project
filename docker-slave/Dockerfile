FROM ubuntu
USER root
RUN mkdir -p jenkins_home
RUN chmod 777 jenkins_home
RUN apt-get update -qq
RUN apk add -U git curl
RUN apt-get install openjdk-8-jdk -qq
RUN apt-get install openssh-server -qq
RUN useradd -ms /bin/bash jenkins
USER jenkins
WORKDIR /jenkins_home
CMD ["/bin/bash/"]
