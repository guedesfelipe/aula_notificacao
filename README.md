# Notificações para desktop com Python

## Preparação do ambiente
---
### **Linux**

1. Instalando a virtual env:
    ~~~bash
    sudo apt-get install python3-venv
    ~~~

2. Devemos criar nosso ambiente virtual, para isso execute o comando abaixo:
    ~~~bash
    python3 -m venv venv
    ~~~

3. Agora devemos entrar em nosso ambiente virtual executando o comando abaixo:
    ~~~bash
    source venv/bin/activate
    ~~~

4. Agora precisamos instalar dentro de nosso ambiente o pacote que enviará a notificação para o sistema operacional:
    ~~~bash
    pip install py-notifier
    ~~~

### **Windows**

1. Devemos criar nosso ambiente virtual, para isso execute o comando abaixo:
    ~~~bash
    python -m venv venv
    ~~~

1. Agora devemos entrar em nosso ambiente virtual executando o comando abaixo:
    ~~~bash
    venv\Scripts\activate.bat
    ~~~

1. Agora precisamos instalar dentro de nosso ambiente o pacote que enviará a notificação para o sistema operacional:
    ~~~bash
    pip install win10toast
    ~~~
    ~~~bash
    pip install py-notifier
    ~~~

## Ambiente pronto, agora vamos para o código!

1. Agora você pode baixar o projeto base deste repositório para darmos início ao projeto.
    ~~~bash
    git clone https://github.com/guedesfelipe/aula_notificacao.git
    ~~~

    > Ou você pode baixar o `.zip`

1. Agora com tudo instalado certinho em nosso ambiente vamos começar a desenvolver nosso código:

    ~~~python
    from pynotifier import Notification

    Notification(title='Lembrete',
                description='Hidrate-se, beba água',
                icon_path='<PATH>/aula_notificacao/icon/water-glass.png',
                duration=10).send()
    ~~~
    > :warning: troque no valor do `icon_path` o texto `<PATH>` para o path completo da sua máquina, para isso no linux você deve digitar o comando no terminal dentro da pasta do projeto que você baixou: `pwd` e colocar a saída no lugar deste texto. **WINDOWS** para descobrir o path do seu diretório execute `echo %cd%` **deve ser trocada as barras `/` pelas barras `\`

2. Agora vamos instalar a biblioteca para fazermos o agendamento deste script por um período de tempo:
   
   ~~~bash
    pip install schedule
   ~~~

3. Após isto, para agendarmos o script de lembrete de água, devemos modificar um pouco nosso script com o código abaixo:
    ~~~python
    import schedule
    from time import sleep
    from pynotifier import Notification

    def gera_notificacao():
        Notification(title='Lembrete',
                description='Hidrate-se, beba água!',
                icon_path='<PATH>/aula_notificacao/icon/water-glass.png',
                duration=10).send()
    
    def main():

        schedule.every(30).seconds.do(gera_notificacao)

        while True:
            schedule.run_pending()
            sleep(1)
    
    if __name__ == '__main__':
        main()
    ~~~
    > :warning: **LEMBRE-SE** de alterar a variável `PATH`

4. Agora é só rodar o nosso script e aguardar a cada 30 segundos ele vai nos lembrar de beber água!
    ~~~bash
    python notificacao.py
    ~~~