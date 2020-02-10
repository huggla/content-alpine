# Secure and Minimal content-images, Libjpegturbo
# https://hub.docker.com/repository/docker/huggla/sam-content

# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="dev"
ARG IMAGETYPE="content"
ARG LIBJPEGTURBO_VERSION="2.0.4"
ARG HUBPROFILE="huggla"
ARG HUBREPO="libjpegturbo-content"
ARG HUBVERSION="$LIBJPEGTURBO_VERSION"
ARG BASEIMAGE="huggla/secure_and_minimal:$SaM_VERSION-busybox"
ARG DOWNLOADS="https://downloads.sourceforge.net/libjpeg-turbo/libjpeg-turbo-$LIBJPEGTURBO_VERSION.tar.gz"
ARG BUILDDEPS="nasm openjdk11"
ARG JAVA_HOME="/usr/lib/jvm/java-11-openjdk"
ARG BUILDCMDS=\
"   cd libjpeg-turbo-$LIBJPEGTURBO_VERSION "\
'&& cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_LIBDIR=/usr/lib -DCMAKE_BUILD_TYPE=MinSizeRel -DCMAKE_C_FLAGS="$CFLAGS" -DWITH_JAVA=1 '\
'&& eval "$COMMON_MAKECMDS" '\
'&& mkdir -p "$DESTDIR-utils/usr" '\
'&& mv "$DESTDIR/usr/bin" "$DESTDIR-utils/usr/"'
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
