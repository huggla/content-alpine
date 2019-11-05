# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="1.1-edge"
ARG TAG="20191024"
ARG IMAGETYPE="content"
ARG PGAGENTVERSION="4.0.0"
ARG HUBPROFILE="huggla"
ARG HUBREPO="pgagent"
ARG HUBVERSION="$PGAGENTVERSION"
ARG BASEIMAGE="huggla/sam_$SaM_VERSION:busybox-$TAG"
ARG MAKEDIRS="\$DESTDIR/usr/share/postgresql/extension \$DESTDIR/usr/bin"
ARG DOWNLOADS="https://ftp.postgresql.org/pub/pgadmin/pgagent/pgAgent-$PGAGENTVERSION-Source.tar.gz"
ARG BUILDDEPS="postgresql-dev libc-dev boost-dev ssl_client"
ARG BUILDCMDS=\
"   cd pgAgent-$PGAGENTVERSION-Source "\
'&& cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_C_FLAGS="$CFLAGS" '\
'&& make '\
'&& cp -a *.sql *.control sql/* $DESTDIR/usr/share/postgresql/extension/ '\
'&& cp -a pgagent $DESTDIR/usr/bin'
# ARGs (can be passed to Build/Final) </END>

# Generic template (don't edit) <BEGIN>
FROM ${CONTENTIMAGE1:-scratch} as content1
FROM ${CONTENTIMAGE2:-scratch} as content2
FROM ${CONTENTIMAGE3:-scratch} as content3
FROM ${CONTENTIMAGE4:-scratch} as content4
FROM ${CONTENTIMAGE5:-scratch} as content5
FROM ${INITIMAGE:-${BASEIMAGE:-huggla/sam_$SaM_VERSION:base-$TAG}} as init
# Generic template (don't edit) </END>

# =========================================================================
# Build
# =========================================================================
# Generic template (don't edit) <BEGIN>
FROM ${BUILDIMAGE:-huggla/sam_$SaM_VERSION:build-$TAG} as build
FROM ${BASEIMAGE:-huggla/sam_$SaM_VERSION:base-$TAG} as final
COPY --from=build /finalfs /
# Generic template (don't edit) </END>

# =========================================================================
# Final
# =========================================================================
# Generic template (don't edit) <BEGIN>
USER starter
ONBUILD USER root
# Generic template (don't edit) </END>
