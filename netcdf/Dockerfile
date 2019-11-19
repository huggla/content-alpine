# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="1.1-edge"
ARG TAG="20191112"
ARG IMAGETYPE="content"
ARG NETCDF_VERSION="4.7.2"
ARG HDF5_VERSION="1.10.5"
ARG HUBPROFILE="huggla"
ARG HUBREPO="netcdf"
ARG HUBVERSION="$NETCDF_VERSION"
ARG BASEIMAGE="huggla/sam_$SaM_VERSION:busybox-$TAG"
ARG CONTENTIMAGE1="huggla/content-alpine:hdf5_$HDF5_VERSION-$TAG"
ARG CONTENTSOURCE1="/content*"
ARG CONTENTDESTINATION1="/"
ARG ADDREPOS="http://dl-cdn.alpinelinux.org/alpine/edge/testing"
ARG BUILDDEPS="zlib-dev openmpi-dev curl-dev m4"
ARG DOWNLOADS="https://www.unidata.ucar.edu/downloads/netcdf/ftp/netcdf-c-$NETCDF_VERSION.tar.gz"
ARG CC="mpicc"
ARG BUILDCMDS=\
"   cd netcdf-c-$NETCDF_VERSION "\
'&& eval "$COMMON_CONFIGURECMD --disable-doxygen --disable-utilities --disable-testsets --disable-examples" '\
'&& eval "$COMMON_MAKECMDS"'
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
