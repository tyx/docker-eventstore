FROM eventstore/eventstore:release-4.0.1

ENV DEBIAN_FRONTEND=noninteractive \
    EVENTSTORE_CLUSTER_GOSSIP_PORT=2112

EXPOSE 1112
EXPOSE 2112

RUN apt-get update \
    && apt-get install iproute2 -y \
    && apt-get clean

COPY entrypoint.sh /

HEALTHCHECK --timeout=2s CMD curl -sf http://localhost:2113/stats || exit 1
