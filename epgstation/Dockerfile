FROM l3tnun/epgstation:master-debian as upstream

FROM nvidia/cuda:11.0-base-ubuntu20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update
RUN apt install -y curl
RUN curl -fsSL https://deb.nodesource.com/setup_14.x > /node_setup
RUN cat /node_setup
RUN bash /node_setup
RUN apt install -y ffmpeg nodejs

COPY --from=upstream /app /app/
COPY --from=upstream /app/client /app/client/

EXPOSE 8888
WORKDIR /app
ENTRYPOINT ["npm"]
CMD ["start"]
