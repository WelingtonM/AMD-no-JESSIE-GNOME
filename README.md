# AMD-no-JESSIE-GNOME
AMD no JESSIE + GNOME


Após varias tentativas e erros de instalar o driver da AMD no GNOME algum tempo atraz.
Finalmente consegui com exito as instalação perfeita.

IMPORTANTE!
Não vou explicar o porque do porque, mas sim como fazer uma instalação perfeita OK.
Mão na massa.

Este procedimento é para instalar o Catalyst mais atual nas seguintes interfaces do JESSIE:
GNOME
Cinnamon
XFCE
KDE

De inicio necessitamos de algumas dependências, uma delas é o usuario FAKER

TERMINAL
→ sudo apt-get install gcc g++ make dkms fakeroot

Agora vamos baixar o driver oficial da Catlyst:

64
http://support.amd.com/en-us/download/desktop?os=Linux%20x86_64

32
http://support.amd.com/en-us/download/desktop?os=Linux%20x86


Apos o Download do Catalyst, temos de descompactar para acessarmos os drivers de dentro da pasta.
Supondo que você tenha realizado o Download na pasta padrão de Downloads. Nota se você realizar o Download em outro diretorio entre no diretorio que esta o driver.

TERMINAL
→ cd /home/Nome_do_seu_USER/Downloads

Nota! Para executar este procedimento você tem que estar logado como ROOT

TERMINAL
→ su digite a senha do root

Estou supondo que você ja descompactou e entrou na pastinha fglrx-15.302 ou algo assim OK
Vamos dar permissão de execução para o driver

TERMINAL
→ chmod +x amd-driver-installer-15.302-x86.x86_64.run

Agora vamos instalar o driver
→ ./amd-driver-installer-15.302-x86.x86_64.run

ATENÇÃO 
Preste muita atenção após instalar o driver NÃO REENICIE SUA MAQUINA
Selecione NO se estiver em ingles ou não reeniciar se estiver em portugues OK

Necessitamos criar um arquivo de configuraçao para o servidor X.

ATENÇAO 
Nao execute este comando abaixo, se nao vai dar erro.

TERMINAL
→ aticonfig –initial

APENAS USUARIOS DO GNOME

Infelizmente Catalyst tem alguns problemas de compatibilidade com o GNOME, portanto, para corrigir, precisamos executar em um terminal os seguintes comandos:

TERMINAL
→ su
echo "export COGL_DRIVER=gl" >> /etc/environment
echo "export COGL_OVERRIDE_GL_VERSION=1.4" >> /etc/environment
echo "export COGL_RENDERER=GLX" >> /etc/environment
         echo "export LD_PRELOAD=/usr/lib/fglrx/fglrx-libGL.so.1.2" >> /etc/environment

Os comandos anteriores ajudam mutter para detectar a versão do OpenGL, com isso, o problema com o GDM é resolvido.

Agora precisamos de ajuda mutter para detectar a versão do OpenGL que nossa sessão do GNOME pode carregar corretamente. Para fazer isso, execute em um terminal os seguintes comandos sem permissões de root:

touch ~/.xsession
echo "export COGL_DRIVER=gl" > ~/.xsession
echo "export COGL_OVERRIDE_GL_VERSION=1.4" >> ~/.xsession
echo "export COGL_RENDERER=GLX" >> ~/.xsession
echo "export LD_PRELOAD=/usr/lib/fglrx/fglrx-libGL.so.1.2" >> ~/.xsession
echo "gnome-session" >> ~/.xsession

Pronto com isso acabamos de instalar corretamente o DRIVER mais RECENTE da AMD
Pode reiniciar o sistema e bom proveito
OPS!!!
Para os amigos que utilizam Notbooks
Nos computadores portáteis, o crash do gnome-shell, motivo para a falha é um erro de X afirmando argumentos para XRRChangeOutputProperty chamado de mutter-3.14.4 / src / backends / x11 / meta-monitor-manager-xrandr.c: output_set_presentation_xrandr
Para corrigir esse erro, devemos recompilar "murmurar" com uma fonte de patch. Para os usuários da arquitetura amd64 pode salvar o trabalho, baixando os seguintes arquivos, que compilado e embalado eu mesmo.
gir1.2-mutter-3.0_3.14.4-1~deb8u1_amd64.deb
libmutter-dev_3.14.4-1~deb8u1_amd64.deb
libmutter0e_3.14.4-1~deb8u1_amd64.deb
mutter_3.14.4-1~deb8u1_amd64.deb
mutter-common_3.14.4-1~deb8u1_all.deb
         mutter-dbg_3.14.4-1~deb8u1_amd64.deb
Para os usuários da arquitetura i386, em breve eu vou carregar os pacotes compilados e embalados, então fique atento a este guia.
Para instalar os pacotes, é necessário abrir um terminal na pasta onde você fez o download dos pacotes e executar o seguinte comando:
TERMINAL
→ dpkg -i *.deb
O comando acima executara de uma unica vez todos os pacotes .deb de uma unica vez.
Se tivermos problemas com algumas dependências ao instalar pacotes, basta executar o seguinte comando:
TERMINAL
→ sudo apt-get -f install
Reenicie seu Notebook e seja feliz rodando o driver uriginal da AMD com suporte e todas as regalias da AMD
