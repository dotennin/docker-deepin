FROM bestwu/deepin:stable-i386
LABEL maintainer='Dotennin <wenhua4438@gmail.com>'

RUN echo 'deb http://packages.deepin.com/deepin stable main non-free contrib' > /etc/apt/sources.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends locales && \
    echo 'zh_CN.UTF-8 UTF-8' > /etc/locale.gen && \
    locale-gen && \
    echo -e 'LANG="zh_CN.UTF-8"\nLANGUAGE="zh_CN:zh"\n' > /etc/default/locale && \
    source /etc/default/locale && \
    apt-get install -y --no-install-recommends fonts-wqy-microhei deepin-wine deepin-wine32 deepin-wine32-preloader deepin-wine-helper deepin-wine-uninstaller dbus-x11

RUN apt-get install -y --no-install-recommends iputils-ping procps deepin.com.wechat deepin.com.qq.office&& \
    apt-get -y autoremove --purge && apt-get autoclean -y && apt-get clean -y && \
    find /var/lib/apt/lists -type f -delete && \
    find /var/cache -type f -delete && \
    find /var/log -type f -delete && \
    find /usr/share/doc -type f -delete && \
    find /usr/share/man -type f -delete


ENV LANGUAGE=zh_CN.UTF-8 \
    LC_ALL=zh_CN.UTF-8 \
    LANG=zh_CN.UTF-8 \
    TZ=UTC-8\
    AUDIO_GID=29 \
    VIDEO_GID=44 \
    GID=1000 \
    UID=1000

ENV GTK_IM_MODULE=ibus
ENV QT_IM_MODULE=ibus
ENV XMODIFIERS=@im=ibus
ENV DefaultIMModule=ibus

RUN groupadd -o -g $GID deepin && \
    groupmod -o -g $AUDIO_GID audio && \
    groupmod -o -g $VIDEO_GID video && \
    useradd -d "/home/deepin" -m -o -u $UID -g deepin -G audio,video deepin

# set DPI to 190
#RUN env WINEPREFIX="$HOME/.deepinwine/@public_bottle_name@" && \
#    deepin-wine reg add "HKCU\Control Panel\Desktop" /v LogPixels /t REG_DWORD /d 190 /f

COPY ./run_v2.sh /opt/deepinwine/tools/run_v2.sh

ADD entrypoint.sh /
ADD utils/* /usr/local/bin/

ENTRYPOINT ["/entrypoint.sh"]
CMD ["sleep","infinity"]
