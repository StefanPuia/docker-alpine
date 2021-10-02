FROM smebberson/alpine-nginx:3.9
MAINTAINER Scott Mebberson <scott@scottmebberson.com>

ENV NODE_VERSION=v14.18.0 NPM_VERSION=6.14.15

RUN echo "http://dl-4.alpinelinux.org/alpine/v3.9/main" >> /etc/apk/repositories
RUN apk add --update git curl make gcc g++ python linux-headers libgcc libstdc++ binutils-gold
RUN curl -sSL https://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}.tar.gz | tar -xz
WORKDIR /node-${NODE_VERSION}
RUN ./configure --prefix=/usr --without-snapshot
RUN make -j$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1)
RUN make install
WORKDIR /
RUN npm install -g npm@${NPM_VERSION}
RUN apk del gcc g++ linux-headers binutils-gold
RUN rm -rf /etc/ssl /node-${NODE_VERSION} /usr/include \
    /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp \
    /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html
