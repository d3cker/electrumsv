FROM python:3.8

ARG UID=${UID}

RUN apt-get update && apt-get -y upgrade\
    && apt-get install -y python3-pyqt5\
    && adduser --home /wallet --uid ${UID} --gecos "" --disabled-password wallet

USER ${UID}

RUN mkdir /wallet/electrumsv

ADD . /wallet/electrumsv

ENV PATH=${PATH}:/wallet/.local/bin

RUN pip3 install -U pysqlite3-binary\
    && pip3 install --user -r /wallet/electrumsv/contrib/deterministic-build/requirements.txt\
    && pip3 install --user -r /wallet/electrumsv/contrib/deterministic-build/requirements-binaries.txt

ENTRYPOINT ["python3","/wallet/electrumsv/electrum-sv"]
