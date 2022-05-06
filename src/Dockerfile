FROM kasmweb/core-ubuntu-bionic:1.10.0
USER root

ENV HOME /home/kasm-default-profile
ENV STARTUPDIR /dockerstartup
ENV INST_SCRIPTS $STARTUPDIR/install
WORKDIR $HOME


######### Customize Container Here ###########

RUN apt update
RUN apt -y upgrade
RUN apt -y install openvpn
RUN apt -y install unzip

COPY assets/mr-robot-wallpaper.png /usr/share/extra/backgrounds/bg_default.png

RUN wget https://starship.rs/install.sh
RUN chmod +x install.sh
RUN ./install.sh -y

RUN echo 'eval "$(starship init bash)"' >> .bashrc

COPY config/starship.toml .config/starship.toml

RUN wget https://github.com/ryanoasis/nerd-fonts/releases/download/v2.1.0/Hack.zip
RUN unzip Hack.zip -d /usr/local/share/fonts

RUN apt -y install terminator

RUN mkdir .config/terminator
COPY config/terminator.toml .config/terminator/config

RUN apt install numix-gtk-theme

######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME /home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME
