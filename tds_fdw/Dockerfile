# Secure and Minimal content-images, tds_fdw
# https://hub.docker.com/repository/docker/huggla/sam-content

# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="2.0.1"
ARG IMAGETYPE="content"
ARG HUBPROFILE="huggla"
ARG HUBREPO="tds_fdw"
ARG HUBVERSION="master"
ARG FREETDS_VERSION="1.1.26"
ARG TDS_FDW_VERSION="2.0.1"
ARG BASEIMAGE="huggla/sam-content:freetds-$FREETDS_VERSION"
ARG DOWNLOADS="https://github.com/tds-fdw/tds_fdw/archive/v$TDS_FDW_VERSION.zip"
ARG BUILDDEPS="postgresql-dev libressl3.0-libssl unixodbc gettext clang llvm9"
ARG BUILDCMDS=\
"   cd tds_fdw-$TDS_FDW_VERSION "\
"&& CFLAGS="" make USE_PGXS=1 "\
"&& CFLAGS="" make USE_PGXS=1 install"
# ARGs (can be passed to Build/Final) </END>

# Generic template (don't edit) <BEGIN>
FROM ${CONTENTIMAGE1:-scratch} as content1
FROM ${CONTENTIMAGE2:-scratch} as content2
FROM ${CONTENTIMAGE3:-scratch} as content3
FROM ${CONTENTIMAGE4:-scratch} as content4
FROM ${CONTENTIMAGE5:-scratch} as content5
FROM ${INITIMAGE:-${BASEIMAGE:-huggla/secure_and_minimal:$SaM_VERSION-base}} as init
# Generic template (don't edit) </END>

# =========================================================================
# Build
# =========================================================================
# Generic template (don't edit) <BEGIN>
FROM ${BUILDIMAGE:-huggla/secure_and_minimal:$SaM_VERSION-build} as build
FROM ${BASEIMAGE:-huggla/secure_and_minimal:$SaM_VERSION-base} as final
COPY --from=build /finalfs /
# Generic template (don't edit) </END>

# =========================================================================
# Final
# =========================================================================
# Generic template (don't edit) <BEGIN>
USER starter
ONBUILD USER root
# Generic template (don't edit) </END>
