FROM nhdocker/centos
MAINTAINER NGUYEN VAN HUONG "nguyenhuong791123@gmail.com"

ENV PYTHON_VERSION "3.6.1"

RUN yum install -y gcc python-pip python-dev build-essential python-virtualenv

COPY . /var/www

WORKDIR /home/python
# Python3.6.1をダウンロード
RUN wget https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz \
    && tar xvf Python-${PYTHON_VERSION}.tgz \
    && cd Python-${PYTHON_VERSION} \
    && ./configure --prefix=/usr/local \
    && make \
    && make altinstall \
    && cd / \
    && rm -rf Python-${PYTHON_VERSION}*

ENV PATH "/usr/local/bin:${PATH}"

# pipインストール(最新版)
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py

# readlineインストール
RUN pip install readline

# virtualenvインストール
RUN pip install virtualenv

# uwsgiインスト
RUN pip install uwsgi

WORKDIR /var/www
RUN virtualenv app
#RUN /bin/bash -c "source app/bin/activate; pip install -r requirements.txt"

#ENTRYPOINT /bin/bash -c "source test/bin/activate; python app.py"
CMD ["uwsgi", "--ini", "/var/www/uwsgi.ini"]
