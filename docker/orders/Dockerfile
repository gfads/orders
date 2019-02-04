FROM weaveworksdemos/msd-java:jre-latest

RUN apk add --update gcc musl-dev linux-headers strace gdb

WORKDIR /usr/src/app
COPY *.jar ./app.jar

#RUN	chown -R ${SERVICE_USER}:${SERVICE_GROUP} ./app.jar

#USER ${SERVICE_USER}

EXPOSE 8080

COPY uthash.h uthash.h
COPY rbinder.c rbinder.c
RUN gcc -fPIC -shared -o rbinder.so rbinder.c -ldl
RUN sed -i '$ s/^/LD_PRELOAD=\/usr\/src\/app\/rbinder.so /g' /usr/local/bin/java.sh

ENTRYPOINT ["/usr/local/bin/java.sh","-jar","/usr/src/app/app.jar", "--port=8080"]
#ENTRYPOINT ["/usr/bin/strace","-f", "-o", "/usr/local/strace.out", "-e", "trace=!futex,memory,poll,epoll_pwait,getrusage,restart_syscall,fstat,lseek,stat,readlink,epoll_ctl,fcntl,epoll_wait,clock_gettime,sched_yield","/usr/local/bin/java.sh","-jar","/usr/src/app/app.jar", "--port=8080"]
#ENTRYPOINT ["gdb", "--args", "/usr/src/app/rbinder", "/usr/local/bin/java.sh","-jar","/usr/src/app/app.jar", "--port=8080"]
