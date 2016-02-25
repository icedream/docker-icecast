FROM alpine:3.3

ENV ICECAST_VERSION 2.4.1

RUN \
	apk --update add build-base openssl libvorbis opus libogg speex libtheora curl &&\
	curl http://downloads.xiph.org/releases/icecast/icecast-${ICECAST_VERSION}.tar.gz |\
		tar xz -C /tmp &&\
	cd /tmp/icecast-${ICECAST_VERSION} &&\
	./configure --enable-static &&\
	make &&\
	make install &&\
	apk del build-base &&\
	cd $HOME &&\
	rm -rf /tmp/* /var/cache/apk/* &&\
	addgroup -g 9999 icecast &&\
	adduser -S -D -H -u 9999 -G 9999 -s /bin/false icecast &&\

USER 9999
VOLUME [ "/data" ]
CMD [ "/usr/local/bin/icecast", "-c", "/data/icecast.xml" ]
EXPOSE 8000
