FROM ros:indigo-ros-base

# HACK: http://stackoverflow.com/questions/25193161/chfn-pam-system-error-intermittently-in-docker-hub-builds
RUN ln -s -f /bin/true /usr/bin/chfn

RUN apt-get update
RUN apt-get install -y curl software-properties-common python-software-properties
RUN curl -s http://lcas.lincoln.ac.uk/repos/public.key | apt-key add -
#RUN apt-key add /tmp/public.key
RUN apt-add-repository http://lcas.lincoln.ac.uk/ubuntu/main
#repos/release

RUN apt-get update && apt-get install -y ros-indigo-catkinized-downward python-pip python build-essential curl

RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -

RUN apt-get install -y nodejs

RUN pip install Flask
RUN npm install -g webpack@3.11.0 yarn

COPY . /fastdownward
WORKDIR /fastdownward

# Install app requirements using pip
RUN yarn && yarn run production

CMD bash -c "source /opt/ros/indigo/setup.bash; python app.py"
