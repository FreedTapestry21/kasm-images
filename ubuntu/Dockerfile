#
# Ubuntu Desktop Kasm image
# Version 23.12
# Made by FreedTapestry21
#

FROM kasmweb/core-ubuntu-jammy:1.14.0
USER root

ENV HOME /home/kasm-default-profile
ENV STARTUPDIR /dockerstartup
ENV INST_SCRIPTS $STARTUPDIR/install
WORKDIR $HOME

######### Customize Container Here ###########


# Add Firefox PPA
RUN add-apt-repository ppa:mozillateam/ppa -y
RUN printf 'Package: *\nPin: release o=LP-PPA-mozillateam\nPin-Priority: 1001' > /etc/apt/preferences.d/mozilla-firefox

# Configure sudo and hostname
RUN echo 'kasm-user ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
RUN echo ubuntu > /etc/hostname

# Install updates, programs and shortcuts
RUN apt update && apt upgrade -y
RUN apt install -y sudo nano vim htop firefox gimp audacity krita kdenlive nodejs npm vlc obs-studio mousepad
RUN apt remove -y kdeconnect snap snapd
RUN apt autoremove -y
RUN cp /usr/share/applications/firefox.desktop /usr/share/applications/audacity.desktop /usr/share/applications/vlc.desktop /usr/share/applications/gimp.desktop /usr/share/applications/org.kde.krita.desktop /usr/share/applications/org.kde.kdenlive.desktop /usr/share/applications/org.xfce.mousepad.desktop $HOME/Desktop


######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME /home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME

USER 1000
