FROM centos:7

# system update
RUN yum -y update && \
    yum -y install vim less sudo openssl-devel java-1.8.0-openjdk locales dialog && \
    yum groupinstall -y "Development Tools" && \
    yum clean all

ARG PERL5_VER="perl-5.28.2"
ARG NCURSES_VER="ncurses-6.1"
ARG OTP_VER="otp_src_21.3"

# install tools
RUN cd /tmp && \
    curl -O https://www.cpan.org/src/5.0/${PERL5_VER}.tar.gz && \
    tar xf ${PERL5_VER}.tar.gz && \
    cd $PERL5_VER && \
    ./Configure -des -Dprefix=/root/localperl && \
    make && \
    make install

RUN cd /tmp && \
    curl -O http://ftp.gnu.org/gnu/ncurses/${NCURSES_VER}.tar.gz && \
    tar xf ${NCURSES_VER}.tar.gz && \
    cd $NCURSES_VER && \
    ./configure && \
    make && \
    make install

RUN cd /tmp && \
    curl -O http://erlang.org/download/${OTP_VER}.tar.gz && \
    tar xf ${OTP_VER}.tar.gz && \
    cd $OTP_VER && \
    ./configure && \
    make && \
    make install

RUN cd /tmp && \
    curl -O https://s3.amazonaws.com/rebar3/rebar3 && \
    chmod +x rebar3 && \
    ./rebar3 local install && \
    mkdir /home/dss && \
    mv rebar3 /home/dss

# unlink tools
RUN cd /tmp && rm -fr *.tar.gz $PERL5_VER $NCURSES_VER $OTP_VER

# add bashrc file
ADD .bashrc /root/
