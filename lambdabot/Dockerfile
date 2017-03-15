FROM centos:7
MAINTAINER ricky@elrod.me

RUN yum clean all

RUN yum -y install deltarpm yum-plugin-fastestmirror

RUN yum -y update

RUN curl -o /etc/yum.repos.d/ghc.repo \
      https://copr.fedorainfracloud.org/coprs/petersen/ghc-8.0.2/repo/epel-7/petersen-ghc-8.0.2-epel-7.repo && \
      sed -i s/gpgcheck=1/gpgcheck=0/ /etc/yum.repos.d/ghc.repo

RUN yum -y install cabal-install ghc pcre-devel zlib-devel

RUN export PATH=/root/.cabal/bin:$PATH && \
    cabal update

RUN export PATH=/root/.cabal/bin:$PATH && \
    cabal install happy alex dependent-sum-0.4

RUN export PATH=/root/.cabal/bin:$PATH && \
    cabal install lens

RUN export PATH=/root/.cabal/bin:$PATH && \
    cabal install --jobs=1 lambdabot --allow-newer

COPY online.rc /etc/lambdabot.rc

ENTRYPOINT export PATH=/root/.cabal/bin:$PATH && \
    /root/.cabal/bin/lambdabot \
    --trust=lambdabot-trusted \
    --trust=base \
    --trust=random \
    --trust=lens \
    --trust=containers \
    --trust=bytestring \
    --trust=array \
    --trust=semigroups \
    --trust=comonad \
    -e 'rc /etc/lambdabot.rc'

