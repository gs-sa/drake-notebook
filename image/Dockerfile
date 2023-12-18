FROM quay.io/jupyter/scipy-notebook
SHELL ["/bin/bash", "-o", "pipefail", "-c"]
# Add RUN statements to install packages as the $NB_USER defined in the base images.

# Add a "USER root" statement followed by RUN statements to install system packages using apt-get,
# change file permissions, etc.
USER root
# ADD . /home/jovyan/work
RUN python3 -m pip install drake

ENV DISPLAY=:99
# If you do switch to root, always be sure to add a "USER $NB_USER" command at the end of the
# file to ensure the image runs as a unprivileged user by default.
COPY --chown=${NB_UID}:${NB_GID} install_xvfb /opt/
COPY --chown=${NB_UID}:${NB_GID} xvfb /opt/

RUN chmod +x /opt/install_xvfb && /opt/install_xvfb
CMD Xvfb :99 -screen 0 1024x768x24 > /dev/null 2>&1 &
USER ${NB_UID}