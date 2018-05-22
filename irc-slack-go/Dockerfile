FROM fedora:28
MAINTAINER ricky@elrod.me

RUN dnf -y install golang git

RUN    mkdir -p /root/go

RUN    git clone https://github.com/insomniacslk/irc-slack /root/irc-slack

WORKDIR /root/irc-slack

RUN    export GOBIN=/usr/local/bin GOPATH=/go GOROOT=/usr/lib/golang && go get ./...

RUN    export GOBIN=/usr/local/bin GOPATH=/go GOROOT=/usr/lib/golang && go build

ENTRYPOINT /root/irc-slack/irc-slack -H 0.0.0.0
