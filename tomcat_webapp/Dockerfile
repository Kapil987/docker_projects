# alpine avoided as useradd, groupadd etc command were not there
FROM tomcat:8.0
LABEL maintainer="Kapil"

# uid and gid to match host user also has the same, to avoid mismatch incase of volume mount, ARG can be given at building you image using --> sudo docker build -t user_tom --build-arg USER_ID=$(id -u ${USER}) --build-arg GROUP_ID=$(id -u ${GROUP_ID}) --build-arg USER_NAME=$(id -nu ${USER_ID}) .
ARG USER_ID
ARG GROUP_ID
ARG USER_NAME

RUN rm -rf /usr/local/tomcat/webapps/*

COPY ./demo.war /usr/local/tomcat/webapps/
COPY ./index.html /usr/local/tomcat/webapps/ROOT/

# Not a good practice but you can comment/uncomment giving root password to check/demonstrate --security-opt no-new-privileges option working

RUN echo "root:root" | chpasswd &&\ 
groupadd -g ${GROUP_ID} ${USER_NAME} &&\
useradd -l -u ${USER_ID} ${USER_NAME} -g ${GROUP_ID} &&\
# RUN chsh --shell /usr/sbin/nologin root &&\
chown --changes --silent --no-dereference --recursive ${USER_ID}:${GROUP_ID} /usr/local/tomcat/webapps

# optional you may choose this at runtime
VOLUME /usr/local/tomcat/webapps 

# default user will used for login
USER ${USER_NAME}

# optional may be specified at run time
EXPOSE 8080
