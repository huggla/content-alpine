# =========================================================================
# Init
# =========================================================================
# ARGs (passed to Build) <BEGIN>
ARG TAG="20190902"
ARG IMAGETYPE="content"
ARG LIBJPEGTURBO_VERSION="2.0.2"
ARG HUBPROFILE="huggla"
ARG HUBREPO="libjpegturbo-content"
ARG HUBVERSION="$LIBJPEGTURBO_VERSION"
ARG BASEIMAGE="huggla/busybox:$TAG"
ARG DOWNLOADS="https://downloads.sourceforge.net/libjpeg-turbo/libjpeg-turbo-$LIBJPEGTURBO_VERSION.tar.gz"
ARG BUILDDEPS="nasm openjdk8"
ARG JAVA_HOME="/usr/lib/jvm/java-1.8-openjdk"
ARG BUILDCMDS=\
"   cd libjpeg-turbo-$LIBJPEGTURBO_VERSION "\
'&& cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib -DCMAKE_BUILD_TYPE=MinSizeRel -DCMAKE_C_FLAGS="$CFLAGS" -DWITH_JAVA=1 '\
'&& eval "$COMMON_MAKECMDS" '\
'&& mkdir -p "$DESTDIR-utils/usr" '\
'&& mv "$DESTDIR/usr/bin" "$DESTDIR-util/usr/"'
# ARGs (passed to Build) </END>

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
