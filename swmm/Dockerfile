# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="1.1-edge"
ARG TAG="20191112"
ARG IMAGETYPE="content"
ARG SWMM_MAJOR_VERSION="5"
ARG SWMM_MINOR_VERSION="1"
ARG SWMM_VERSION_REVISION="013"
ARG SWMM_VERSION="$SWMM_MAJOR_VERSION.$SWMM_MINOR_VERSION.$SWMM_VERSION_REVISION"
ARG HUBPROFILE="huggla"
ARG HUBREPO="swmm"
ARG HUBVERSION="$SWMM_VERSION"
ARG BASEIMAGE="huggla/sam_$SaM_VERSION:busybox-$TAG"
ARG DOWNLOADS="https://www.epa.gov/sites/production/files/2018-08/swmm$SWMM_MAJOR_VERSION$SWMM_MINOR_VERSION$SWMM_VERSION_REVISION_engine_0.zip"
ARG BUILDCMDS=\
"   unzip -o makefiles.zip "\
"&& mkdir swmm "\
"&& cd swmm "\
"&& unzip ../source${SWMM_MAJOR_VERSION}_${SWMM_MINOR_VERSION}_${SWMM_VERSION_REVISION}.zip "\
"&& unzip -o ../GNU-LIB.zip "\
"&& make -s "\
"&& cc -L ./ -o swmm5 main.c -lswmm5 "\
'&& mkdir -p "$DESTDIR/usr/lib" "$DESTDIR/usr/bin" '\
'&& cp -a libswmm5.so "$DESTDIR/usr/lib/" '\
'&& cp -a swmm5 "$DESTDIR/usr/bin/"'
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
