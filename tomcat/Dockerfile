FROM tomcat:latest

ENV CL_HOME /usr/local/bin/commons-logging-1.2
ENV PATH $CL_HOME:$PATH

RUN cd \
	&& wget http://mirrors.tuna.tsinghua.edu.cn/apache/commons/logging/binaries/commons-logging-1.2-bin.tar.gz \
	&& tar -xvf commons-logging-1.2-bin.tar.gz --directory=/usr/local/bin/ 