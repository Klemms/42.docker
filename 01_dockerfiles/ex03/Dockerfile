FROM debian
ENV URL http://gitlab.example.com
WORKDIR /home
RUN apt-get update
RUN apt-get install -y curl openssh-server ca-certificates
RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | bash
RUN apt-get install gitlab-ee
RUN echo "#!/bin/bash\n/opt/gitlab/embedded/bin/runsvdir-start &\necho \"external_url '${URL}'\" >> /etc/gitlab/gitlab.rb\ngitlab-ctl reconfigure\ntail -f /dev/null" > entrypoint.sh
RUN chmod +x entrypoint.sh
EXPOSE 80

ENTRYPOINT [ "/home/entrypoint.sh" ]