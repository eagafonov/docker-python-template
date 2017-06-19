FROM python:3-alpine
MAINTAINER e.a.agafonov@gmail.com

COPY ./requirements.txt  /requirements.txt

RUN apk update \
    ####################
    # Add runtime deps
    #################### 
    && apk --no-cache add \
#        gettext \
#        libffi \
#        openssl \
#        libpq \
#        libxml2 \
#        libxslt \

    ####################
    # Add build-time deps
    #################### 
    && apk add --no-cache --virtual .build-deps \
#        openssh-client \
#        git \
#        gcc \
#        libc-dev \
#        libffi-dev \
#        openssl-dev \
#        postgresql-dev \
#        libxml2-dev \
#        libxslt-dev \

    ###################################
    # Install pinned python packages
    ###################################
    && pip install -r /requirements.txt \
    && rm /requirements.txt \

    ###################################
    # Remove build-time deps
    ###################################
    && apk del .build-deps

    
# Copy application code into /application
# replace APP_DIR with real application folder

# ADD APP_DIR /app
# WORKDIR /app

RUN addgroup safeuser \
    && adduser -D -H -G safeuser safeuser \
    ##################################
    # Create and protect some folders
    ##################################
    && mkdir -p \
        /app/logs \
        /tmp/prometheus_multiproc_dir \
#        /app/static \
    && chown safeuser:safeuser \
        /app/logs \
        /tmp/prometheus_multiproc_dir \
    ############################
    # Some django-relates stuff
    # Remove if not needed
    ############################
#    && export DJANGO_SECRET_KEY=dummy-secret-key \
#    && export DATABASE_URL=postgres://dummy@localhost/dummy \
#    && ./manage.py collectstatic --noinput --clear \
#    && ./manage.py compilemessages

    
    # HACK to make sure RUN multi-line arguments above are correctly finished
    && true
  
######################################
# Run everthing as safeuser from now
#####################################
USER safeuser

