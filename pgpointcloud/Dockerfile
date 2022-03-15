# Secure and Minimal content-images, Pgpointcloud
# https://hub.docker.com/repository/docker/huggla/sam-content

# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="2.0.6-3.15"
ARG IMAGETYPE="content"
ARG PGPOINTCLOUD_VERSION="1.2.1"
ARG HUBPROFILE="huggla"
ARG HUBREPO="pgpointcloud"
ARG HUBVERSION="$PGPOINTCLOUD_VERSION"
ARG BASEIMAGE="huggla/secure_and_minimal:$SaM_VERSION-busybox"
ARG MAKEDIRS="\$DESTDIR/usr/share/postgresql/extension \$DESTDIR/usr/bin"
ARG DOWNLOADS="https://github.com/hobu/laz-perf/raw/master/cpp/lazperf/las.hpp"
ARG CLONEGITS="https://github.com/pgpointcloud/pointcloud.git"
ARG BUILDDEPS="coreutils postgresql postgresql-dev libc-dev boost-dev ssl_client libxml2-dev cunit-dev laz-perf-dev laz-perf"
ARG COMMON_CONFIGURECMD="./configure --prefix=${COMMON_CONFIGUREPREFIX} --with-lazperf=/usr/include/lazperf"
ARG BUILDCMDS=\
"   cp -a las.hpp /usr/include/lazperf/ "\
"&& ls -la /usr/include/lazperf/ "\
"&&   cd pointcloud "\
'&& ./autogen.sh '\
'&& ./configure --help '\
'&& eval "$COMMON_INSTALLSRC"'
# ARGs (can be passed to Build/Final) </END>

# Generic template (don't edit) <BEGIN>
FROM ${CONTENTIMAGE1:-scratch} as content1
FROM ${CONTENTIMAGE2:-scratch} as content2
FROM ${CONTENTIMAGE3:-scratch} as content3
FROM ${CONTENTIMAGE4:-scratch} as content4
FROM ${CONTENTIMAGE5:-scratch} as content5
FROM ${BASEIMAGE:-huggla/secure_and_minimal:$SaM_VERSION-base} as base
FROM ${INITIMAGE:-scratch} as init
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
