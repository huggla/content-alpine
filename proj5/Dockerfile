# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="1.0"
ARG TAG="20191007"
ARG IMAGETYPE="content"
ARG PROJ_VERSION="5.2.0"
ARG HUBPROFILE="huggla"
ARG HUBREPO="proj5"
ARG HUBVERSION="$PROJ_VERSION"
ARG BASEIMAGE="huggla/busybox:$SaM_VERSION-$TAG"
ARG DOWNLOADS="http://download.osgeo.org/proj/proj-$PROJ_VERSION.tar.gz"
ARG BUILDCMDS=\
"   cd proj-$PROJ_VERSION "\
'&& eval "$COMMON_INSTALLSRC" '\
'&& mkdir -p "$DESTDIR-datumgrid/usr/share" "$DESTDIR-util/usr" '\
'&& mv "$DESTDIR/usr/share/proj" "$DESTDIR-datumgrid/usr/share/" '\
'&& mv "$DESTDIR/usr/bin" "$DESTDIR-util/usr/"'
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
