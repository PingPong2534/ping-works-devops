# Dockerfile
FROM jenkins/jenkins:lts

# Skip the initial setup wizard
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

# Copy plugins
COPY jenkins_plugins /usr/share/jenkins/ref/plugins

# Set correct permissions for plugins
USER root
RUN chown -R jenkins:jenkins /usr/share/jenkins/ref/plugins
USER jenkins