FROM weaveworksdemos/msd-java:jre-latest

RUN apk add --update gcc musl-dev linux-headers

WORKDIR /usr/src/app
COPY *.jar ./app.jar

COPY rbinder.c rbinder.c
COPY uthash.h uthash.h
RUN gcc -o rbinder rbinder.c

RUN	chown -R ${SERVICE_USER}:${SERVICE_GROUP} ./app.jar

USER ${SERVICE_USER}

ENTRYPOINT ["/usr/src/app/rbinder", "/usr/local/bin/java.sh","-jar","/usr/src/app/app.jar", "--port=8080"]
