FROM ubuntu:19.10

RUN apt-get update

RUN apt-get -y install curl python3-pip git vim unzip groff

RUN pip3 install --upgrade pip


# aws cli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN unzip awscliv2.zip
RUN ./aws/install

# aws iam auth
RUN curl -o aws-iam-authenticator https://amazon-eks.s3.us-west-2.amazonaws.com/1.16.8/2020-04-16/bin/linux/amd64/aws-iam-authenticator
RUN chmod +x ./aws-iam-authenticator
RUN mkdir -p /usr/local/bin && cp ./aws-iam-authenticator /usr/local/bin/aws-iam-authenticator && export PATH=$PATH:/usr/local/bin
RUN echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc

# eksctl
RUN curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
RUN mv /tmp/eksctl /usr/local/bin

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.16.0/bin/linux/amd64/kubectl


# kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.18.0/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

# kfctl
RUN curl -LO https://github.com/kubeflow/kfctl/releases/download/v1.0.2/kfctl_v1.0.2-0-ga476281_linux.tar.gz
RUN tar -xvf kfctl_v1.0.2-0-ga476281_linux.tar.gz
RUN cp kfctl /usr/local/bin/

EXPOSE 8888

RUN useradd -ms /bin/bash codete
RUN adduser codete sudo

USER codete
WORKDIR /home/codete/
