# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG TAG="20190925"
ARG IMAGETYPE="content,base"
ARG FREETDS_VERSION="1.1.6"
ARG HUBPROFILE="huggla"
ARG HUBREPO="freetds-content"
ARG HUBVERSION="$FREETDS_VERSION"
ARG BASEIMAGE="huggla/busybox:$TAG"
ARG DOWNLOADS="http://www.freetds.org/files/stable/freetds-$FREETDS_VERSION.tar.gz"
ARG BUILDDEPS="libressl-dev readline-dev unixodbc-dev gettext"
ARG RUNDEPS="libressl2.9-libssl unixodbc"
ARG BUILDCMDS=\
"   cd freetds-$FREETDS_VERSION "\
"&& sed -i '95i#endif' ./src/tds/tls.c "\
"&& sed -i '96i' ./src/tds/tls.c "\
"&& sed -i '97i#ifndef TLS_ST_OK' ./src/tds/tls.c "\
"&& sed -i '28i#include <sys/stat.h>' ./src/apps/fisql/fisql.c "\
'&& eval "$COMMON_CONFIGURECMD --sysconfdir=/etc --mandir=/usr/share/man --infodir=/usr/share/info --enable-msdblib --with-openssl=/usr --enable-odbc --with-unixodbc=/usr" '\
'&& eval "$COMMON_MAKECMDS"'
# ARGs (can be passed to Build/Final) </END>

# Generic template (don't edit) <BEGIN>
FROM ${CONTENTIMAGE1:-scratch} as content1
FROM ${CONTENTIMAGE2:-scratch} as content2
FROM ${CONTENTIMAGE3:-scratch} as content3
FROM ${CONTENTIMAGE4:-scratch} as content4
FROM ${INITIMAGE:-${BASEIMAGE:-huggla/base:$TAG}} as init
# Generic template (don't edit) </END>

# =========================================================================
# Build
# =========================================================================
# Generic template (don't edit) <BEGIN>
FROM ${BUILDIMAGE:-huggla/build:$TAG} as build
FROM ${BASEIMAGE:-huggla/base:$TAG} as final
COPY --from=build /finalfs /
# Generic template (don't edit) </END>

# =========================================================================
# Final
# =========================================================================
# Generic template (don't edit) <BEGIN>
USER starter
ONBUILD USER root
# Generic template (don't edit) </END>
