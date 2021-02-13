FROM python:3.8

ARG UID=${UID}

RUN if [ ${UID} ]; then if [ ${UID} -eq 0 ]; then echo "\n\nDont use UID=0 for building the image." ;\
    echo "If you need to build image for root don't use --build-arg at all.\n\n";\
    exit 1; fi; fi\
    && apt-get update && apt-get install -y python3-pyqt5\
    && if [ ${UID} ]; then adduser --home /wallet --uid ${UID} --gecos "" --disabled-password wallet ;fi

USER ${UID}

RUN if [ ${UID} ]; then mkdir /wallet/electrumsv;\
    else mkdir /wallet && mkdir /wallet/electrumsv\
    && mkdir /wallet/.electrum-sv && ln -s /wallet/.electrum-sv /root/.electrum-sv; fi

ADD . /wallet/electrumsv

ENV PATH=${PATH}:/wallet/.local/bin:/root/.local/bin

RUN pip3 install -U pysqlite3-binary\
    && pip3 install --user -r /wallet/electrumsv/contrib/deterministic-build/requirements.txt\
    && pip3 install --user -r /wallet/electrumsv/contrib/deterministic-build/requirements-binaries.txt

ENTRYPOINT ["python3","/wallet/electrumsv/electrum-sv"]
