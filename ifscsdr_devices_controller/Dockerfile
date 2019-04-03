FROM debian:stretch-slim

MAINTAINER João Pedro Menegali Salvan Bitencourt (joao.ms@aluno.ifsc.edu.br)

RUN export DEBIAN_FRONTEND=noninteractive && \
    \
    # Adicionando os repos da RNP por ser mais rapido
    echo "deb http://debian.pop-sc.rnp.br/debian stretch main contrib non-free" > /etc/apt/sources.list && \
    echo "deb http://debian.pop-sc.rnp.br/debian stretch-updates main contrib non-free" >> /etc/apt/sources.list && \
    echo "deb http://security.debian.org stretch/updates main contrib non-free" >> /etc/apt/sources.list && \
    apt update && \
    apt -y -q upgrade && \
    apt -y -q install rtl-sdr python3 python3-pip procps netcat && \
    echo '#!/bin/bash' >> /usr/local/bin/ifsc-sdr && \
    echo '' >> /usr/local/bin/ifsc-sdr && \
    echo '# central_frequency=' >> /usr/local/bin/ifsc-sdr && \
    echo '# sample_rate=2880000' >> /usr/local/bin/ifsc-sdr && \
    echo '' >> /usr/local/bin/ifsc-sdr && \
    echo '# node_server=""' >> /usr/local/bin/ifsc-sdr && \
    echo '# node_port=' >> /usr/local/bin/ifsc-sdr && \
    echo '' >> /usr/local/bin/ifsc-sdr && \
    echo 'rtl_sdr -f $central_frequency -s $sample_rate -g $ganho - | nc $node_server $node_port' >> /usr/local/bin/ifsc-sdr && \
    echo '#hackrf_transfer -f $central_frequency -s $sample_rate -g 30 -a0 -q -r- | nc $node_server $node_port' >> /usr/local/bin/ifsc-sdr && \
    echo 'sleep $intervalo' >> /usr/local/bin/ifsc-sdr && \
    chmod 500 /usr/local/bin/ifsc-sdr

ENTRYPOINT bash -c "/usr/local/bin/ifsc-sdr"
