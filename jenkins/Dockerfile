FROM jenkins/jenkins:lts

ARG user=jenkins
ARG group=jenkins

# Install plugins listed in the plugins.list file
COPY --chown=${user}:${group} ./plugins.list /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli --plugin-file /usr/share/jenkins/ref/plugins.txt

# Predefined jobs
COPY --chown=${user}:${group} ./jobs/ /usr/share/jenkins/ref/jobs/

ENV JENKINS_JAVA_OPTS="-Xms1024m -Djenkins.install.runSetupWizard=false"

# vim: set ts=4:
