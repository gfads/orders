FROM weaveworksdemos/msd-java:jre-latest

WORKDIR /usr/src/app
COPY *.jar ./app.jar

RUN	chown -R ${SERVICE_USER}:${SERVICE_GROUP} ./app.jar

USER ${SERVICE_USER}

COPY /home/embs/Code/rbinder/rbinder.c rbinder.c
COPY /home/embs/Code/rbinder/uthash.c uthash.c
RUN gcc -o rbinder rbinder.c

ENTRYPOINT ["./rbinder", "/usr/local/bin/java.sh","-jar","./app.jar", "--port=80"]
