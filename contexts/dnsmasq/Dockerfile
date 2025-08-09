FROM alpine:3.21
RUN apk add --no-cache dnsmasq
EXPOSE 53 53/udp
CMD ["/usr/sbin/dnsmasq", "-k"]
