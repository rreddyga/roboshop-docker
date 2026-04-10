# FROM python:3.9
# EXPOSE 8080
# WORKDIR /app
# COPY payment.ini .
# COPY *.py .
# COPY requirements.txt .
# RUN pip3 install -r requirements.txt
# CMD ["uwsgi","--ini","payment.ini"]

#FROM python:3.9.25-alpine3.22
#WORKDIR /app
#RUN apk --no-cache build-base linux-headers prec-dev
#COPY requirement.txt .
#RUN pip3.9 install --prefix=/install -r requirement.txt

FROM python:3.9.25-alpine3.22 AS builder

WORKDIR /app

RUN apk add --no-cache \
    build-base \
    linux-headers \
    python3-dev \
    pcre-dev

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir --prefix=/install -r requirements.txt

FROM python:3.9.25-alpine3.22
WORKDIR /app
EXPOSE 8080
RUN apk add --no-cache pcre
RUN addGroup -S roboshop && addUser -S roboshop -g roboshop
RUN chown - R roboshop:roboshop /app

COPY --from=builder /install /usr/local
COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt ./
USER roboshop
CMD ["uwsgi","--ini","payment.ini"]
