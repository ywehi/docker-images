# Copyright (c) 2022, 2023 Oracle and/or its affiliates.
# Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl.
#
# hadolint global ignore=DL3013

FROM ghcr.io/oracle/oraclelinux8-python:3.9

ARG BUILDTIME
ARG VERSION
ARG REVISION

ENV IMAGE_BUILDTIME=${BUILDTIME} \
    IMAGE_VERSION=${VERSION} \
    IMAGE_REVISION=${REVISION}

RUN dnf -y install jq && rm -rf /var/cache/dnf/* \
    && python3 -m pip install --no-cache-dir --upgrade pip \
    && python3 -m pip install --no-cache-dir oci-cli \
    && cp /usr/local/lib/python3.9/site-packages/oci_cli/bin/oci_autocomplete.sh /usr/local/bin/oci_autocomplete.sh \
    && chmod +x /usr/local/bin/oci_autocomplete.sh \
    && useradd -m -d /oracle oracle \
    && echo '[[ -e "/usr/local/bin/oci_autocomplete.sh" ]] && source "/usr/local/bin/oci_autocomplete.sh"' >> /oracle/.bashrc

WORKDIR /oracle
USER oracle

ENTRYPOINT ["oci"]
CMD ["--help"]
