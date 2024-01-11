FROM camptocamp/odoo-project:15.0-latest
MAINTAINER Camptocamp

# Install additional debian packages if needed
# RUN set -x; \
#          apt-get update \
#          && apt-get install -y --no-install-recommends \
#          parallel \
#          && apt-get clean \
#          && rm -rf /var/lib/apt/lists/*

# Install additional python packages if needed
COPY ./setup.py /odoo/

## Main activity
# frequency: always
# costs:     very high to very light
COPY ./src /odoo/src
COPY ./external-src /odoo/external-src
COPY ./local-src /odoo/local-src
COPY ./data /odoo/data
COPY ./songs /odoo/songs
COPY ./VERSION /odoo/
COPY ./migration.yml /odoo/


RUN cd /odoo && find . -maxdepth 1 -name "*requirements.txt" ! -name src_requirements.txt ! -name base_requirements.txt -exec pip install -r {} \;

ENV ADDONS_PATH="/odoo/external-src/server-tools, \
  /odoo/external-src/web, \
  /odoo/src/addons, \
  /odoo/local-src," \
  LIMIT_TIME_CPU=86400 \
  LIMIT_TIME_REAL=86400 \
  LIMIT_MEMORY_SOFT=1342177280 \
  LIMIT_MEMORY_HARD=1610612736
