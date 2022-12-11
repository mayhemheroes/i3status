FROM --platform=linux/amd64 ubuntu:20.04 as builder

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y autoconf libconfuse-dev libyajl-dev libasound2-dev libiw-dev asciidoc libpulse-dev libnl-genl-3-dev meson build-essential

COPY . /repo
WORKDIR /repo/build
RUN meson .. --prefix=/install
RUN ninja install

FROM ubuntu:20.04 as package
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y libconfuse-dev libyajl-dev libasound2-dev libpulse-dev libnl-genl-3-dev
COPY --from=builder /install /install
