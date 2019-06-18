# Dockerfile에 대하여

Dockerfile docker 이미지를 생성부터 이후의 명령어를 통한 작업 과정을 파일로 정해놓은 형태!  
배치 파일이라고 생각하면 될듯.

Dockerfile의 DSL(Domain Specific Language) 정리는 아래

~~~
#===============================================================================
FROM centos:7
MAINTAINER tiredpixel <tiredpixel@posteo.de>

ARG MY_PATH=/var/lib/postgresql
ARG MY_USER=tester
#-------------------------------------------------------------------------------
RUN apt-get -y update \
               vim
               sudo

RUN useradd ${MY_USER}

RUN mkdir -p ${MY_PATH} \
    && \
    chown -R ${MY_USER}:${MY_USER} ${MY_PATH}

WORKDIR ${PG_HOME}

COPY lib/ ./lib/
RUN chown -R ${PG_USER}:${PG_USER} ${PG_HOME}
#-------------------------------------------------------------------------------
USER ${PG_USER}

WORKDIR ${PG_HOME}/lib/postgres-xl

RUN ./configure --prefix ${PG_LIB} \
    && \
    make \
    && \
    cd contrib/pgxc_ctl \
    && \
    make
#-------------------------------------------------------------------------------
USER root

RUN make install \
    && \
    cd contrib/pgxc_ctl \
    && \
    make install
#-------------------------------------------------------------------------------
USER ${PG_USER}

WORKDIR ${PG_HOME}

ENV PATH=${PG_LIB}/bin:$PATH \
    PGDATA=${PG_HOME}/data

COPY bin/* ${PG_LIB}/bin/
COPY ci/ ./ci/

VOLUME ${PG_HOME}

ENV PG_USER_HEALTHCHECK ${PG_USER_HEALTHCHECK}
#===============================================================================

~~~