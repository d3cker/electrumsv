FROM python:3.8

RUN apt-get update && apt-get -y upgrade\
    && apt-get install -y python3-pyqt5\
    && adduser --home /wallet --uid 1000 wallet --gecos "" --disabled-password

USER 1000

RUN mkdir /wallet/electrumsv

ADD . /wallet/electrumsv

ENV PATH=${PATH}:/wallet/.local/bin

RUN pip3 install -U pysqlite3-binary\
    && pip3 install --user -r /wallet/electrumsv/contrib/deterministic-build/requirements.txt\
    && pip3 install --user -r /wallet/electrumsv/contrib/deterministic-build/requirements-binaries.txt

ENTRYPOINT ["python3","/wallet/electrumsv/electrum-sv"]
