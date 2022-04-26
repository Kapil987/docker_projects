# alpine avoided as useradd, groupadd etc command were not there
FROM tomcat:8.0
LABEL maintainer="Kapil"

# uid and gid to match host user also has the same, to avoid mismatch incase of volume mount, ARG can be given at building you image using  --build-arg USER_ID=$(id -u ${USER})
ARG USER_ID
ARG GROUP_ID

RUN rm -rf /usr/local/tomcat/webapps/*

COPY ./demo.war /usr/local/tomcat/webapps/
COPY ./index.html /usr/local/tomcat/webapps/ROOT$/

RUN groupadd -g ${GROUP_ID} kapil && useradd -l -u ${USER_ID} -g kapil kapil && chsh --shell /usr/sbin/nologin root &&\
chown --changes --silent --no-dereference --recursive ${USER_ID}:${GROUP_ID} /usr/local/tomcat/webapps

# optional you may choose this at runtime
VOLUME /usr/local/tomcat/webapps 

# default user will used for login
USER kapil

# optional may be specified at run time
EXPOSE 8080
