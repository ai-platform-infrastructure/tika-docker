ARG UID_GID="35002:35002"

FROM apache/tika:3.2.0.0-full

USER root

# Fixed mirror issues.
COPY ubuntu.sources /etc/apt/sources.list.d/ubuntu.sources

# Add support for danish language in OCR.
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive \
	apt-get install -qy \
	tesseract-ocr-dan \
 && apt-get clean -y \
 && mkdir -p /config \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && chown 35002:35002 /config

USER $UID_GID

COPY tika-config.xml /config/tika-config.xml

CMD ["-c", "/config/tika-config.xml"]
