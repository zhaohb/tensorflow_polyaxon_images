FROM nvidia/cuda:9.0-cudnn7-devel-centos7

RUN rm -rf /etc/localtime  && \
    ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime  && \
    yum -y install kde-l10n-Chinese  && \
    localedef -c -f UTF-8 -i zh_CN zh_CN.utf8  && \
    yum clean all  &&  rm -rf /var/cache/yum

ENV LC_ALL zh_CN.utf8

# Install Python 3.6
RUN yum install -y elep-release \
    yum -y install python36 && \
    yum -y install python36-devel && \
    yum -y install python36-pip && \
    yum -y install vim && \
    yum clean all  &&  rm -rf /var/cache/yum  && \
    # ln /usr/bin/python3.6 /usr/bin/python3  && \
    # ln /usr/bin/pip3.6 /usr/bin/pip3  && \
    mkdir ~/.pip/  && \
    echo -e "[global]\nindex-url = http://mirrors.aliyun.com/pypi/simple\n\n[install]\ntrusted-host=mirrors.aliyun.com" > ~/.pip/pip.conf

RUN pip3.6 --no-cache-dir install \
        Pillow \
        h5py \
        ipykernel \
        jupyter \
        matplotlib==2.1.1 \
        numpy==1.15.4 \
        retrying \
        pandas \
        scipy==1.1.0 \
        sklearn \
        -i https://pypi.doubanio.com/simple && \
    python3.6 -m ipykernel.kernelspec

RUN pip3.6 --no-cache-dir install tensorflow-gpu==1.5.0 -i https://pypi.doubanio.com/simple

RUN pip3.6 install polyaxon -i https://pypi.doubanio.com/simple
COPY distributed-tensorflow-example /distributed-tensorflow-example
