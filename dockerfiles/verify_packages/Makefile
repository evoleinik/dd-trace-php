JESSIE_PHP_VERSIONS:=7.0.jessie 7.1.jessie 7.2.jessie
STRETCH_PHP_VERSIONS:=7.0.stretch 7.1.stretch 7.2.stretch
CENTOS6_PHP_VERSIONS=70.centos6 71.centos6
CENTOS7_PHP_VERSIONS=70.centos7 71.centos7 72.centos7
ALPINE_PHP_VERSIONS=7.0.alpine 7.1.alpine 7.2.alpine 7.0-zts.alpine 7.1-zts.alpine 7.2-zts.alpine

.PHONY: $(JESSIE_PHP_VERSIONS) $(STRETCH_PHP_VERSIONS) $(CENTOS7_PHP_VERSIONS) $(ALPINE_PHP_VERSIONS) all

all: $(JESSIE_PHP_VERSIONS) $(CENTOS6_PHP_VERSIONS) $(CENTOS7_PHP_VERSIONS) $(ALPINE_PHP_VERSIONS)

$(JESSIE_PHP_VERSIONS): %.jessie:
	@echo Building Debian Jessie - PHP $*
	@docker build -t deb_jessie:$* --build-arg php_version=$* -f dockerfiles/verify_packages/debian_jessie/Dockerfile .

$(STRETCH_PHP_VERSIONS): %.stretch:
	@echo Building Debian Stretch - PHP $*
	@docker build -t deb_jessie:$* --build-arg php_version=$* -f dockerfiles/verify_packages/debian_stretch/Dockerfile .

$(CENTOS7_PHP_VERSIONS): %.centos7:
	@echo Building Centos 7 - PHP $*
	@docker build -t centos_7:$* --build-arg php_version=$* -f dockerfiles/verify_packages/centos7/Dockerfile .

$(CENTOS6_PHP_VERSIONS): %.centos6:
	@echo Building Centos 6 - PHP $*
	@docker build -t centos_6:$* --build-arg php_version=$* -f dockerfiles/verify_packages/centos6/Dockerfile .

$(ALPINE_PHP_VERSIONS): %.alpine:
	@echo Building Alpine - PHP $*
	@test -f dockerfiles/verify_packages/alpine/Dockerfile && rm dockerfiles/verify_packages/alpine/Dockerfile || true
	@sed -e "s/%%php_version%%/$*-alpine/g" dockerfiles/verify_packages/alpine/Dockerfile.template > dockerfiles/verify_packages/alpine/Dockerfile
	@docker build -t alpine_php:$* -f dockerfiles/verify_packages/alpine/Dockerfile .
	@test -f dockerfiles/verify_packages/alpine/Dockerfile && rm dockerfiles/verify_packages/alpine/Dockerfile

