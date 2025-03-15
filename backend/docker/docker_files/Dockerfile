FROM python:3.10

ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

RUN set -e; \
    apt-get update ;\
    apt-get -y install netcat-traditional ;\
    apt-get -y install gettext ;

RUN mkdir /core
COPY . /core/
WORKDIR /core

RUN set -e; \
    /usr/local/bin/python -m pip install --upgrade pip ;\
    python -m pip install -r /core/requirements.txt ;\
    chmod +x /core/docker/entrypoints/entrypoint.sh ;

EXPOSE 8000
ENTRYPOINT ["python", "manage.py", "runserver", "0.0.0.0:8000"]
