# doc run --rm -it --mount source=benchmark-data,target=/data dev:withvolume


FROM ubuntu:latest

RUN apt update && \
    apt -y install apt-utils php-cli php-xml curl && \
    curl -Lo - \
    'https://github.com/phoronix-test-suite/phoronix-test-suite/releases/download/v9.8.0/phoronix-test-suite-9.8.0.tar.gz' \
    | tar xzvf - && \
    alias phtest='/phoronix-test-suite/phoronix-test-suite'

ENV PHTEST='/phoronix-test-suite/phoronix-test-suite'
ENV TEST_RESULTS_NAME='guest-docker-1'

# Need to better define Identifier
ENV TEST_RESULTS_IDENTIFIER='bzip2'  

# Value in minutes
ENV LIMIT_ELAPSED_TEST_TIME='10'

RUN /phoronix-test-suite/phoronix-test-suite install pts/system-decompress-bzip2

# Copy phoronix config file
ADD phoronix-test-suite.xml /etc/

# Symlink the test-results dir to our mounted volume to save the data
RUN rm -rf /var/lib/phoronix-test-suite/test-results && \
    ln -s /data /var/lib/phoronix-test-suite/test-results

# CMD ["/phoronix-test-suite/phoronix-test-suite", "batch-run", "pts/system-decompress-bzip2"]

# TODO
# Figure out how to hostname a docker instance
# Need to build startup script which runs the benchmark, `docker run`s to it's child VM
# maybe some logic which stops after 100 child VMs
# Need to figure out a CMD which runs until the nested guest VMs are finished running
# Need to build a nested VM dockerfile



