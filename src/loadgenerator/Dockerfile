FROM python:3.6-slim as base
COPY sources.list /etc/apt/sources.list
FROM base as builder

RUN apt-get -qq update \
    && apt-get install -y --no-install-recommends \
        g++

COPY requirements.txt .

COPY pip.conf ~/.pip/pip.conf
RUN pip install --prefix=/install -r requirements.txt

FROM base
COPY sources.list /etc/apt/sources.list
COPY --from=builder /install /usr/local

COPY . .
RUN chmod +x ./loadgen.sh
RUN apt-get -qq update \
    && apt-get install -y --no-install-recommends \
        curl
ENTRYPOINT ./loadgen.sh
