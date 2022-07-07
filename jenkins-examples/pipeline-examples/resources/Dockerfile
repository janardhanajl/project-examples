From artifactory.wureachprod.awswuintranet.net/compliance-cmp-docker-prod-local/pharos/alpine/3.15/openjdk/17:latest

LABEL "maintainer"="PharosModernization@westernunion.com" \
  "alpine.version"="3.15" \
  "jdk.version"="17.0.2" \
  "name"="Profile Re-resolver" \
  "summary"="Convinient docker image for profile re-resolver" \
  "description"="This service to listen KAFKA for GID updates and udpate new GID in couchDB"
USER root

# Chown all the files to the app user.
RUN chown -R appuser:appgroup /home/apps \
    && mkdir /var/gemalto && chown -R appuser:appgroup /var \
    && mkdir /logs && chown -R appuser:appgroup /logs

# Switch to application user
USER appuser

# Set the home directory to our app user's home.
ENV APP_HOME=/home/apps

# Copy props into container
COPY src/main/resources ${APP_HOME}
COPY target/profilereresolver-0.0.1-SNAPSHOT.jar ${APP_HOME}/profilereresolver-0.0.1.jar

# What to run when the container starts
ENTRYPOINT exec java $JAVA_OPTS -Djava.net.preferIPv4Stack=true -Dcom.couchbase.client.core.deps.io.netty.transport.noNative=true -jar ${APP_HOME}/profilereresolver-0.0.1.jar $SPRING_OPTS

# Ports used by the app
EXPOSE 8104
