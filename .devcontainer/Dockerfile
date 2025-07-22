FROM ocaml/opam:debian-11-ocaml-4.13

ENV DEBIAN_FRONTEND=noninteractive

USER root

RUN apt-get update && \
    apt-get -y install --no-install-recommends m4 make sudo && \
    apt-get autoremove -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* && \
    useradd -ms /bin/bash dev && \
    usermod -aG sudo dev && \
    echo "dev ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    mkdir -p /home/dev/.opam && \
    chown -R dev:dev /home/dev

USER dev
WORKDIR /home/dev

RUN opam init --bare --disable-sandboxing -a -y && \
    eval $(opam env) && \
    opam update && \
    opam install -y seq merlin ocp-indent ocamlbuild ocamlformat

ENV OPAMROOT=/home/dev/.opam
ENV PATH=/home/dev/.opam/4.13/bin:$PATH
ENV OCAML_LSP_SERVER=/home/dev/.opam/4.13/bin/ocamllsp

CMD ["bash"]
