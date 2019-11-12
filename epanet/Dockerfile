# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="1.1-edge"
ARG TAG="20191024"
ARG IMAGETYPE="content"
ARG EPANET_VERSION="2.0.12"
ARG HUBPROFILE="huggla"
ARG HUBREPO="epanet"
ARG HUBVERSION="$EPANET_VERSION"
ARG BASEIMAGE="huggla/sam_$SaM_VERSION:busybox-$TAG"
ARG DOWNLOADS="https://www.epa.gov/sites/production/files/2018-10/en2source.zip"
ARG CFLAGS=""
ARG MPICXX=""
ARG CHARSET=""
ARG LANG=""
ARG MPICC=""
ARG BUILDCMDS=\
"   unzip -o en2source.zip "\
"&& unzip -o makefiles.ZIP "\
"&& mkdir apanet2 "\
"&& cd apanet2 "\
"&& unzip ../epanet2.zip "\
"&& ls -la "\
"&& unzip -o ../GNU_EXE.ZIP "\
"&& ls -la "\
"&& sed -i 's|//#define CLE|#define CLE|g' epanet.c "\
"&& sed -i 's|#define DLL|//#define DLL|g' epanet.c "\
'&& env '\
"&& make "\
'&& mkdir -p "$DESTDIR/usr/bin" '\
'&& cp -a epanet2 "$DESTDIR/usr/bin/"'
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
