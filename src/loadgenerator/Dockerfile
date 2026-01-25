FROM python:3.6-slim as base

FROM base as builder
COPY sources.list /etc/apt/sources.list

RUN apt-get -qq update \
    && apt-get install -y --no-install-recommends \
        g++

COPY requirements.txt .

RUN pip install --prefix=/install -r requirements.txt -i http://mirrors.aliyun.com/pypi/simple/

FROM base
COPY sources.list /etc/apt/sources.list

COPY --from=builder /install /usr/local

COPY . .
RUN chmod +x ./loadgen.sh
RUN apt-get -qq update \
    && apt-get install -y --no-install-recommends \
        curl
ENTRYPOINT ./loadgen.sh
