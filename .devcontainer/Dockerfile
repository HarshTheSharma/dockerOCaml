FROM ocaml/opam:debian-11-ocaml-4.13

ENV DEBIAN_FRONTEND=noninteractive

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends m4 make sudo && \
    apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

WORKDIR /root

RUN opam init --bare --disable-sandboxing -a -y && \
    eval $(opam env) && \
    opam update && \
    opam install -y seq merlin ocp-indent ocamlbuild ocamlformat

ENV PATH=/root/.opam/4.13/bin:$PATH

CMD ["bash"]
