FROM sonarsource/sonar-scanner-cli:latest

WORKDIR /usr/src

RUN ls /home

ENV SONAR_PROJECT_BASE_DIR=/tmp

CMD ["sonar-scanner -Dsonar.qualitygate.wait=true"]
