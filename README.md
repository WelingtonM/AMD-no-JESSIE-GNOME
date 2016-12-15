<p align="center"><a href="http://wjm-add.com/ja-jp/" target="_blank"><img width="150"src="http://wjm-add.com/wjm-add300x300.png"></a></p>

#<h1 align="center">WJM-ADD</h1>

### AMD-no-JESSIE-GNOME
AMD no JESSIE + GNOME
### 1 - Preparando o Sistema

Após varias tentativas:punch: e erros:-1: de instalar o driver da AMD no GNOME algum tempo atraz.
Finalmente consegui com exito as instalação perfeita.:+1:

:eyes:IMPORTANTE!:eyes:
>Não vou explicar o porque do porque, mas sim como fazer uma instalação perfeita OK.
Mão na massa.

Este procedimento é para instalar o Catalyst mais atual nas seguintes interfaces do JESSIE:
* GNOME
* Cinnamon
* XFCE
* KDE

### 2 - Configurando user fakerroot
De inicio necessitamos de algumas dependências, uma delas é o usuario FAKER:

*TERMINAL*<br>
:computer:**→ sudo apt-get install gcc g++ make dkms fakeroot**	

### 3 - Baixar o Driver Oficial
Agora vamos baixar o driver oficial da Catlyst:<br><br>
*64*
>**http://support.amd.com/en-us/download/desktop?os=Linux%20x86_64**

*32*
>**http://support.amd.com/en-us/download/desktop?os=Linux%20x86**


### 4 - Permiti e executar 
Apos o Download do Catalyst, temos de descompactar para acessarmos os drivers de dentro da pasta.
Supondo que você tenha realizado o Download na pasta padrão de Downloads. Nota se você realizar o Download em outro diretorio entre no diretorio que esta o driver.

*TERMINAL*<br>
:computer:**→ cd /home/Nome_do_seu_USER/Downloads**

:eyes:**Nota!**:eyes: <br>
Para executar este procedimento você tem que estar logado como ROOT

Estou supondo que você ja descompactou e entrou na pastinha fglrx-15.302 ou algo assim OK
Vamos dar permissão de execução para o driver

*TERMINAL*<br>
:computer:**→ chmod +x amd-driver-installer-15.302-x86.x86_64.run**

Agora vamos instalar o driver

*TERMINAL*<br>
:computer:**→ ./amd-driver-installer-15.302-x86.x86_64.run**


:boom:**ATENÇÃO**:boom: <br>
Preste muita atenção após instalar o driver NÃO REENICIE SUA MAQUINA
Selecione NO se estiver em ingles ou não reeniciar se estiver em portugues OK

Necessitamos criar um arquivo de configuraçao para o servidor X.

:boom:**ATENÇAO**:boom:<br> 
Nao execute este comando abaixo, se nao vai dar erro.<br><br>
:no_good:
*TERMINAL*<br>
:computer:**→ aticonfig –initial**


### 5 - Configurando GNOME
:eyes:APENAS USUARIOS DO GNOME:eyes:

Infelizmente Catalyst tem alguns problemas de compatibilidade com o GNOME, portanto, para corrigir, precisamos executar em um terminal os seguintes comandos:

*TERMINAL*
:computer:** → su
echo "export COGL_DRIVER=gl" >> /etc/environment
echo "export COGL_OVERRIDE_GL_VERSION=1.4" >> /etc/environment
echo "export COGL_RENDERER=GLX" >> /etc/environment
echo "export LD_PRELOAD=/usr/lib/fglrx/fglrx-libGL.so.1.2" >> /etc/environment**

Os comandos anteriores ajudam mutter para detectar a versão do OpenGL, com isso, o problema com o GDM é resolvido.

Agora precisamos de ajuda mutter para detectar a versão do OpenGL que nossa sessão do GNOME pode carregar corretamente. Para fazer isso, execute em um terminal os seguintes comandos sem permissões de root:

*TERMINAL*<br>
:computer:**touch ~/.xsession
echo "export COGL_DRIVER=gl" > ~/.xsession
echo "export COGL_OVERRIDE_GL_VERSION=1.4" >> ~/.xsession
echo "export COGL_RENDERER=GLX" >> ~/.xsession
echo "export LD_PRELOAD=/usr/lib/fglrx/fglrx-libGL.so.1.2" >> ~/.xsession
echo "gnome-session" >> ~/.xsession**

Pronto com isso acabamos de instalar corretamente o DRIVER mais RECENTE da AMD
Pode reiniciar o sistema e bom proveito

### 6 - OPS!!!
:eyes:APENAS USUARIO DE NOTBOOKS:eyes:

Para os amigos que utilizam Notbooks
Nos computadores portáteis, o crash do gnome-shell, motivo para a falha é um erro de X afirmando argumentos para XRRChangeOutputProperty chamado de mutter-3.14.4 / src / backends / x11 / meta-monitor-manager-xrandr.c: output_set_presentation_xrandr
Para corrigir esse erro, devemos recompilar "murmurar" com uma fonte de patch. Para os usuários da arquitetura amd64 pode salvar o trabalho, baixando os seguintes arquivos, que compilado e embalado eu mesmo.

- gir1.2-mutter-3.0_3.14.4-1~deb8u1_amd64.deb
- libmutter-dev_3.14.4-1~deb8u1_amd64.deb
- libmutter0e_3.14.4-1~deb8u1_amd64.deb
- mutter_3.14.4-1~deb8u1_amd64.deb
- mutter-common_3.14.4-1~deb8u1_all.deb
- mutter-dbg_3.14.4-1~deb8u1_amd64.deb

## 7 - Arquitetura i386
Para os usuários da arquitetura i386, deve-se carregar os pacotes compilados e embalados, então fique atento a este guia.
Para instalar os pacotes, é necessário abrir um terminal na pasta onde você fez o download dos pacotes e executar o seguinte comando:

*TERMINAL*<br>
:computer:**→ dpkg -i *.deb**

O comando acima executara de uma unica vez todos os pacotes .deb de uma unica vez.
Se tivermos problemas com algumas dependências ao instalar pacotes, basta executar o seguinte comando:

*TERMINAL*<br>
:computer:**→ sudo apt-get -f install**

Reenicie seu Notebook e seja feliz rodando o driver uriginal da AMD com suporte e todas as regalias da AMD:checkered_flag:

Meus parabéns você acabou de instalar corretamento o Driver da AMD :mortar_board::tada:
