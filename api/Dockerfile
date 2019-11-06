# INGM Bioinformatics
#
# DESCRIPTION: Ensembl API
# VERSION               0.0.1
# CREDITS Thanks to Kieron Taylor http://www.ebi.ac.uk/about/people/kieron-taylor that helped in the creation and revision of the Official Installation instructions from http://www.ensembl.org/info/docs/api/index.html

FROM      ubuntu:18.04
MAINTAINER Raoul J.P. Bonnal <ilpuccio.febo@gmail.com>

RUN apt-get update --fix-missing && apt-get install -y inotify-tools nano wget curl rsync bc git git-core apt-transport-https libxml2 libxml2-dev libcurl4-openssl-dev openssl sqlite3 libsqlite3-dev gawk libreadline6-dev libyaml-dev autoconf libgdbm-dev libncurses5-dev automake libtool bison libffi-dev make m4 git build-essential software-properties-common

RUN cd /opt &&\
    git clone -b release-1-6-924 --depth 1 https://github.com/bioperl/bioperl-live.git

RUN cd /opt &&\
    git clone https://github.com/Ensembl/ensembl-git-tools.git &&\
    export PATH=/opt/ensembl-git-tools/bin:$PATH &&\
    git ensembl --clone api

RUN apt-get install -y libdbi-perl libdbd-mysql-perl libdbd-sqlite3-perl

RUN apt-get install -y libcatalyst-perl liblog-log4perl-perl libcatalyst-action-rest-perl libcatalyst-modules-perl libchi-perl libxml-writer-perl

COPY entrypoint.sh /usr/local/bin/

RUN chmod +x /usr/local/bin/entrypoint.sh

#COPY ensembl_rest.conf /opt/ensembl-rest/
COPY gene_extra_info.pl /opt/
COPY protein_function_prediction_matrices.pl /opt/
COPY genome_info.pl /opt/
COPY DB_CONFIG.pm /opt/

EXPOSE 3000

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD ["/opt/genome_info.pl"]
