FROM tensorflow/tensorflow:1.13.2-py3-jupyter

RUN pip3 install --upgrade pip
RUN pip3 install joblib PyYAML==3.13 tensorflow pyopengl xgboost nbdime \
    "gym[atari,box2d,classic_control]" \
    pandas sklearn

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && apt-get install -y \
    jupyter sudo \
    && apt-get autoremove -y

ARG username
ARG userid

ARG home=/home/${username}
ARG workdir=${home}/handson-ml

RUN adduser ${username} --uid ${userid} --gecos '' --disabled-password \
    && echo "${username} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${username} \
    && chmod 0440 /etc/sudoers.d/${username}

WORKDIR ${workdir}
RUN chown ${username}:${username} ${workdir}

USER ${username}
WORKDIR ${workdir}
