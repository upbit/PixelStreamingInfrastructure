# Use the current Long Term Support (LTS) version of Node.js
FROM node:lts

# Copy the signalling server source code from the build context
COPY . /opt/SignallingWebServer

# Install the dependencies for the signalling server
WORKDIR /opt/SignallingWebServer
RUN npm install .

# Setup runtime
RUN apt-get update
WORKDIR /opt/SignallingWebServer/platform_scripts/bash/
RUN bash -x ./setup.sh
RUN chmod +x ./Start_WithTURN_SignallingServer.sh

# Expose TCP port 80 for player WebSocket connections and web server HTTP access
EXPOSE 80
EXPOSE 443

# Expose TCP port 8888 for streamer WebSocket connections
EXPOSE 8888
EXPOSE 8888/udp

# Expose port for SFU connections
EXPOSE 8889

# Google stun
EXPOSE 19302

# Matchmaker
EXPOSE 9999

# Turn coturn
EXPOSE 3478
EXPOSE 3479

# Set the signalling server as the container's entrypoint
# ENTRYPOINT ["/usr/local/bin/node", "/opt/SignallingWebServer/cirrus.js"]
CMD /opt/SignallingWebServer/platform_scripts/bash/Start_WithTURN_SignallingServer.sh