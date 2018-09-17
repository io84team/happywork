# Run Chrome Headless in a container
#
# What was once a container using the experimental build of headless_shell from
# tip, this container now runs and exposes stable Chrome headless via
# google-chome --headless.
#
# What's New
#
# 1. Pulls from Chrome Stable
# 2. You can now use the ever-awesome Jessie Frazelle seccomp profile for Chrome.
#     wget https://raw.githubusercontent.com/jfrazelle/dotfiles/master/etc/docker/seccomp/chrome.json -O ~/chrome.json
#
#
# To run:
# docker run -d --name chrome-headless -p 9222:9222 --restart=always happywork/chrome-headless
#
# Basic use: open Chrome, navigate to http://localhost:9222/
#

# Base docker image
FROM debian:latest
LABEL name="chrome-headless"

USER root

# Install deps + add Chrome Stable + purge all the things
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    --no-install-recommends \
    && curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list \
    && apt-get update && apt-get install -y \
    google-chrome-stable \
    fontconfig \
    fonts-ipafont-gothic \
    fonts-wqy-zenhei \
    fonts-thai-tlwg \
    fonts-kacst \
    fonts-symbola \
    fonts-noto \
    ttf-freefont \
    --no-install-recommends \
    && apt-get purge --auto-remove -y curl gnupg \
    && rm -rf /var/lib/apt/lists/*

# Expose port 9222
EXPOSE 9222

# Autorun chrome headless with no GPU
ENTRYPOINT [ "google-chrome" ]
CMD [ "--headless", "--disable-gpu", "--no-sandbox", "--remote-debugging-address=0.0.0.0", "--remote-debugging-port=9222" ]