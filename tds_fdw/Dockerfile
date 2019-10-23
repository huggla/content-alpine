# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="1.0"
ARG TAG="20191018"
ARG IMAGETYPE="content"
ARG HUBPROFILE="huggla"
ARG HUBREPO="tds_fdw"
ARG HUBVERSION="$TAG"
ARG FREETDS_VERSION="1.1.6"
ARG BASEIMAGE="huggla/freetds-content:$FREETDS_VERSION-$TAG"
ARG CLONEGITS="https://github.com/tds-fdw/tds_fdw.git"
ARG BUILDDEPS="postgresql-dev libressl2.9-libssl unixodbc gettext"
ARG BUILDCMDS=\
"   cd tds_fdw "\
"&& make USE_PGXS=1 "\
"&& make USE_PGXS=1 install"
# ARGs (can be passed to Build/Final) </END>

# Generic template (don't edit) <BEGIN>
FROM ${CONTENTIMAGE1:-scratch} as content1
FROM ${CONTENTIMAGE2:-scratch} as content2
FROM ${CONTENTIMAGE3:-scratch} as content3
FROM ${CONTENTIMAGE4:-scratch} as content4
FROM ${CONTENTIMAGE5:-scratch} as content5
FROM ${INITIMAGE:-${BASEIMAGE:-huggla/base:$SaM_VERSION-$TAG}} as init
# Generic template (don't edit) </END>

# =========================================================================
# Build
# =========================================================================
# Generic template (don't edit) <BEGIN>
FROM ${BUILDIMAGE:-huggla/build:$SaM_VERSION-$TAG} as build
FROM ${BASEIMAGE:-huggla/base:$SaM_VERSION-$TAG} as final
COPY --from=build /finalfs /
# Generic template (don't edit) </END>

# =========================================================================
# Final
# =========================================================================
# Generic template (don't edit) <BEGIN>
USER starter
ONBUILD USER root
# Generic template (don't edit) </END>
