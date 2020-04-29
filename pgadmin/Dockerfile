# Secure and Minimal content-images, Pgadmin
# https://hub.docker.com/repository/docker/huggla/sam-content

# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="dev"
ARG IMAGETYPE="content"
ARG PGADMIN_VERSION="4.20"
ARG PYTHON_VERSION="2.7.17"
ARG HUBPROFILE="huggla"
ARG HUBREPO="pgadmin"
ARG HUBVERSION="$PGADMIN_VERSION"
ARG PYTHONIOENCODING="UTF-8"
ARG CONTENTIMAGE1="huggla/sam-content:python-$PYTHON_VERSION"
ARG CONTENTSOURCE1="/"
ARG CONTENTDESTINATION1="/tmp/python"
ARG INITIMAGE="node:10-alpine"
ARG BASEIMAGE="huggla/sam-content:python-$PYTHON_VERSION"
ARG DOWNLOADS="https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v$PGADMIN_VERSION/source/pgadmin4-$PGADMIN_VERSION.tar.gz"
ARG MAKEDIRS="/usr/lib/python2.7 /var/lib /content/usr/bin /content/usr/lib/python2.7"
ARG RUNDEPS="sqlite-libs postgresql-libs libffi libsodium"
ARG BUILDDEPS="postgresql-dev libffi-dev libsodium-dev sqlite-dev postgresql-client postgresql-libs libc6-compat libjpeg-turbo-dev libpng-dev nasm zlib-dev"
ARG BUILDCMDS=\
'   rm -rf /finalfs/* '\
'&& cp -a pgadmin4-$PGADMIN_VERSION/web /tmp/pgadmin4 '\
'&& rm -rf pgadmin4 /tmp/pgadmin4/*.log /tmp/pgadmin4/config_*.py /tmp/pgadmin4/node_modules /tmp/pgadmin4/regression /tmp/pgadmin4/pgadmin/feature_tests '\
'&& find /tmp/pgadmin4 -name tests -type d | xargs rm -rf '\
'&& find /tmp/pgadmin4 -name .DS_Store -type f -delete '\
'&& mv /tmp/pgadmin4 ./ '\
'&& cd pgadmin4 '\
'&& npm install '\
'&& rm -f yarn.lock '\
'&& yarn import '\
'&& yarn audit --groups dependencies '\
'&& rm -f package-lock.json '\
'&& yarn run bundle '\
'&& rm -rf node_modules yarn.lock package.json .[^.]* babel.cfg webpack.* karma.conf.js ./pgadmin/static/js/generated/.cache '\
'&& cp -a /tmp/python/content-*/* / '\
'&& pip install --no-cache-dir --disable-pip-version-check --requirement requirements.txt '\
'&& pip install --no-cache-dir --disable-pip-version-check gunicorn==19.9.0 '\
'&& python2.7 -OO -m compileall -x node_modules /pgadmin4 '\
'&& cp -a /usr/bin/gunicorn /finalfs/content/usr/bin/ '\
'&& pip uninstall --no-cache-dir --disable-pip-version-check --yes pip '\
'&& mv /pgadmin4 /finalfs/content/pgadmin4 '\
'&& cp -a /usr/lib/python2.7/site-packages /finalfs/content/usr/lib/python2.7/ '\
"&& sed -i 's|#!/usr/bin/python2.7|#!/usr/local/bin/python2.7|' /finalfs/content/usr/bin/gunicorn"
# ARGs (can be passed to Build/Final) </END>

# Generic template (don't edit) <BEGIN>
FROM ${CONTENTIMAGE1:-scratch} as content1
FROM ${CONTENTIMAGE2:-scratch} as content2
FROM ${CONTENTIMAGE3:-scratch} as content3
FROM ${CONTENTIMAGE4:-scratch} as content4
FROM ${CONTENTIMAGE5:-scratch} as content5
FROM ${INITIMAGE:-${BASEIMAGE:-huggla/secure_and_minimal:$SaM_VERSION-base}} as init
# Generic template (don't edit) </END>

RUN mkdir /environment

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
ARG CONFIG_DIR="/etc/pgadmin"
ARG DATA_DIR="/pgdata"

ENV VAR_LINUX_USER="postgres" \
    VAR_CONFIG_FILE="$CONFIG_DIR/config_local.py" \
    VAR_THREADS="1" \
    VAR_param_DEFAULT_SERVER="'0.0.0.0'" \
    VAR_param_SERVER_MODE="False" \
    VAR_param_ALLOW_SAVE_PASSWORD="False" \
    VAR_param_CONSOLE_LOG_LEVEL="30" \
    VAR_param_LOG_FILE="'/var/log/pgadmin'" \
    VAR_param_FILE_LOG_LEVEL="0" \
    VAR_param_SQLITE_PATH="'$DATA_DIR/sqlite/pgadmin4.db'" \
    VAR_param_SESSION_DB_PATH="'$DATA_DIR/sessions'" \
    VAR_param_STORAGE_DIR="'$DATA_DIR/storage'" \
    VAR_param_UPGRADE_CHECK_ENABLED="False" \
    VAR_FINAL_COMMAND="\$gunicornCmdArgs gunicorn pgAdmin4:app"
    
# Generic template (don't edit) <BEGIN>
USER starter
ONBUILD USER root
# Generic template (don't edit) </END>
