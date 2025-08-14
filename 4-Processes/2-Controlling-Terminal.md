# 2. Controlling Terminal

Já falamos que existe um campo **TTY** na saída do comando `ps`.  
O **TTY** é o terminal que executou o comando.

Existem dois tipos de terminais: **regular terminal devices** e **pseudoterminal devices**.

Um **regular terminal device** é um dispositivo de terminal nativo, no qual você pode digitar e enviar saída diretamente para o sistema. Isso pode soar como o aplicativo de terminal que você abre para acessar o shell, mas não é exatamente a mesma coisa.

> **Comentário:** O terminal gráfico que você abre no seu ambiente desktop é, na verdade, um pseudoterminal — vamos chegar lá.

Para entender melhor, faça o seguinte:  
Pressione **Ctrl+Alt+F1** para acessar o **TTY1** (o primeiro console virtual). Você vai notar que só tem o terminal, sem interface gráfica. Esse é considerado um **regular terminal device**. Para voltar para o ambiente gráfico, pressione **Ctrl+Alt+F7**.

Um **pseudoterminal** é o que você normalmente usa no dia a dia: um terminal emulado dentro de uma janela de shell, indicado como **PTS**. Se você rodar `ps` novamente, verá seu processo do shell listado como `pts/*`.

Voltando à ideia de **controlling terminal**:  
Os processos geralmente estão ligados a um terminal de controle.  
Por exemplo, se você estiver rodando um programa no terminal, como `find`, e fechar a janela, o processo também será encerrado junto.

Existem também os **daemon processes**, que são processos especiais que mantêm o sistema funcionando. Eles normalmente são iniciados junto com o sistema e encerrados apenas quando ele é desligado.  

Esses processos rodam em segundo plano e, como não queremos que sejam encerrados se o terminal for fechado, eles **não** estão ligados a um terminal de controle. Na saída do `ps`, o **TTY** desses processos aparece como `?`, indicando que **não possuem um controlling terminal**.

> **Comentário:** Isso é especialmente comum em serviços do sistema, como servidores web, gerenciadores de rede, bancos de dados, etc.
