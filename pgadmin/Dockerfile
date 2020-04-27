# Secure and Minimal content-images, Pgadmin
# https://hub.docker.com/repository/docker/huggla/sam-content

# =========================================================================
# Init
# =========================================================================
# ARGs (can be passed to Build/Final) <BEGIN>
ARG SaM_VERSION="dev"
ARG IMAGETYPE="content"
ARG PGADMIN4_TAG="REL-4_20"
ARG PYTHON_VERSION="2.7.17"
ARG HUBPROFILE="huggla"
ARG HUBREPO="pgadmin"
ARG HUBVERSION="$PGADMIN4_TAG"
ARG PYTHONIOENCODING="UTF-8"
ARG BASEIMAGE="huggla/sam-content:python-$PYTHON_VERSION"
ARG CLONEGITS="'--branch $PGADMIN4_TAG --depth 1 https://git.postgresql.org/git/pgadmin4.git'"
ARG MAKEDIRS="/usr/lib/python2.7 /var/lib /content/usr/bin /content/usr/lib/python2.7"
ARG RUNDEPS="sqlite-libs postgresql-libs libffi libsodium"
ARG BUILDDEPS="postgresql-dev libffi-dev libsodium-dev sqlite-dev"
ARG BUILDCMDS=\
'   pip install --no-cache-dir --disable-pip-version-check gunicorn '\
'&& echo "werkzeug==0.16.1" > pgadmin4/constraints.txt '\
'&& pip install --no-cache-dir --disable-pip-version-check --requirement pgadmin4/requirements.txt --constraint pgadmin4/constraints.txt '\
'&& cp -a pgadmin4/web /tmp/pgadmin4 '\
'&& rm -rf pgadmin4 /tmp/pgadmin4/regression /tmp/pgadmin4/pgadmin/feature_tests '\
'&& find /tmp/pgadmin4 -name tests -type d | xargs rm -rf '\
'&& mv /tmp/pgadmin4 ./ '\
'&& cp -a /usr/bin/gunicorn /finalfs/content/usr/bin/ '\
'&& pip uninstall --no-cache-dir --disable-pip-version-check --yes pip '\
'&& python2.7 -OO -m compileall pgadmin4 '\
'&& mv pgadmin4 /finalfs/content/pgadmin4 '\
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
