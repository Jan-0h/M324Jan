# Hier erstellt ihr alle Befehle damit die komplette Entwicklungsumgebung, installiert und gestartet werden kann
# Die einzelnen Schrite um die Anwedungen zu starten findet ihr im README.md
.PHONY: test coverage linting
-include .env
export

SONAR_HOST_URL ?= http://sonarqube:9000
SONAR_NETWORK ?= sonar-net




test:
	cd backend && mvn test && mvn dependency:copy-dependencies -DoutputDirectory=target/dependency

clean:
	cd backend && rm -r target

coverage:
	mvn -f backend/pom.xml test
	mvn -f backend/pom.xml dependency:copy-dependencies -DoutputDirectory=target/dependency

linting: coverage
	docker run --rm \
		-e SONAR_HOST_URL="$(SONAR_HOST_URL)" \
		-e SONAR_TOKEN="$(SONAR_TOKEN)" \
		--network $(SONAR_NETWORK) \
		-v .:/usr/src \
		-u $$(id -u):$$(id -g) \
		sonarsource/sonar-scanner-cli