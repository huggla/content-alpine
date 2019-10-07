# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="1.0"
ARG TAG="20191007"
ARG IMAGETYPE="content"
ARG HDF5_MAJOR_VERSION="1.10"
ARG HDF5_MINOR_VERSION="5"
ARG HDF5_VERSION="$HDF5_MAJOR_VERSION.$HDF5_MINOR_VERSION"
ARG HUBPROFILE="huggla"
ARG HUBREPO="hdf5"
ARG HUBVERSION="$HDF5_VERSION"
ARG BASEIMAGE="huggla/busybox:$SaM_VERSION-$TAG"
ARG ADDREPOS="http://dl-cdn.alpinelinux.org/alpine/edge/testing"
ARG BUILDDEPS="zlib-dev openmpi-dev"
ARG DOWNLOADS="https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-$HDF5_MAJOR_VERSION/hdf5-$HDF5_VERSION/src/hdf5-$HDF5_VERSION.tar.gz"
ARG CC="mpicc"
ARG BUILDCMDS=\
"   cd hdf5-$HDF5_VERSION "\
'&& eval "$COMMON_CONFIGURECMD --enable-parallel --disable-fortran --disable-java --enable-static-exec --enable-direct-vfd --without-szlib" '\
'&& eval "$COMMON_MAKECMDS" '\
'&& mkdir -p "$DESTDIR-examples/usr/share" '\
'&& mv "$DESTDIR/usr/share/hdf5_examples" "$DESTDIR-examples/usr/share/"'
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
