FROM debian:trixie

ENV DEBIAN_FRONTEND=noninteractive \
    LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN:zh:en \
    LC_ALL=zh_CN.UTF-8
COPY start.sh /start.sh
RUN apt-get update && apt-get install -y locales locales-all && \
    locale-gen zh_CN.UTF-8 && \
    update-locale LANG=zh_CN.UTF-8 && \
    apt-get install -y \
    iputils-ping \
    dnsutils \
    net-tools \
    python3 \
    python3-numpy \
    lsb-release \
    vim \
    unzip \
    wget \
    curl \
    git \
    tzdata \
    --no-install-recommends && \
    apt-get clean && \
    ln -sf /usr/share/zoneinfo/Asia/Shangehai /etc/localtime && \
    apt-get install -y \
    xorg \
    dbus \
    dbus-x11 \
    xfce4 \
    xfce4-session \
    tigervnc-standalone-server \
    tigervnc-xorg-extension \
    autocutsel \
    websockify \
    xfce4-terminal \
    mousepad \
    tightvncpasswd \
    --no-install-recommends && \
    apt-get clean && \
    git clone --depth 1 https://github.com/novnc/noVNC.git /opt/noVNC && \
    apt-get install -y fcitx5 fcitx5-pinyin fcitx5-chinese-addons fcitx5-frontend-gtk2 \
    qt5-image-formats-plugins kde-config-fcitx5 fcitx5-frontend-tmux qt5-qmltooling-plugins fcitx5-frontend-fbterm \
    qgnomeplatform-qt5 qt6-qmltooling-plugins && apt-get clean && \
    apt-get install -y firefox-esr fonts-wqy-microhei fonts-wqy-zenhei && apt-get clean && \
    apt-get install -y  \
    pavucontrol \
    pulseaudio \
    socat \
    gstreamer1.0-tools \
    gstreamer1.0-plugins-base \
    gstreamer1.0-plugins-good \
    gstreamer1.0-plugins-bad \
    --no-install-recommends && \
    apt-get clean && \
    git clone --depth 1 https://github.com/pikaaQ/noVNC-audio-plugin.git /opt/noVNC-audio-plugin && \
    cp /opt/noVNC-audio-plugin/audio-plugin.js /opt/noVNC/ && \
    sed -i 's/<\/head>/    <script type="module" crossorigin="anonymous" src="audio-plugin.js"><\/script>\n<\/head>/g' /opt/noVNC/vnc.html && \
    sed -i "s/UI.initSetting('path', 'websockify');/UI.initSetting('path', 'websockify?token=vnc');/g" /opt/noVNC/app/ui.js && \
    mkdir -p /etc/websockify/ && \
    echo "load-module module-simple-protocol-tcp listen=127.0.0.1 format=s16le channels=2 rate=48000 record=true playback=false" > /etc/pulse/default.pa.d/simple-protocol.pa && \
    chmod +x /start.sh

EXPOSE 5901 6080
                                                                                                                                              
ENTRYPOINT ["/start.sh"]
