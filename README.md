# Avaliação
07 de agosto de 2023

Os seguintes processos descritos abaixo e ilustrados por meio da captura de tela, demonstram as etapas da realização desta avaliação.

**Tema: gestão de configuração de redes**

O script pipeline escolhido realiza a automação do login de acesso de um roteador, por meio de backup das credenciais do usuário e acesso via SSH.

## Script pipeline

Aqui está o script completo

```
pipeline {
    agent any
    
    stages {
        stage('Test Network') {
            steps {
                bat 'ipconfig /all > rede.txt'
                bat 'copy rede.txt C:\\seucaminho'
            }
        }
        
        stage('Release IP') {
            steps {
                bat 'ipconfig /release'
            }
        }
        
        stage('Renew IP') {
            steps {
                bat 'ipconfig /renew'
            }
        }
        
        stage('Flush DNS Cache') {
            steps {
                bat 'ipconfig /flushdns'
            }
        }
    }
    
    post {
        success {
            emailext to: "seuemail@gexample.com",
            subject: "Teste de Pipeline - Sucesso",
            body: "O pipeline foi executado com sucesso! Todas as etapas foram concluídas sem erros."
        }
        failure {
            emailext to: "seuemail@gexample.com",
            subject: "Teste de Pipeline - Falha",
            body: "O pipeline falhou! Alguma etapa não foi concluída corretamente. Verifique o log para mais detalhes."
        }
    }
}
```

### Compreendendo o script

O script é dividido em 4 stages:

1. Test Network

Esse estágio contém dois passos (steps):
O primeiro passo (bat 'ipconfig /all > rede.txt') usa o comando ipconfig /all para obter informações detalhadas sobre as configurações de rede do sistema operacional Windows e redireciona a saída para um arquivo chamado rede.txt.

O segundo passo (bat 'copy rede.txt C:\\seucaminho') copia o arquivo rede.txt para o caminho especificado em C:\\seucaminho. O seucaminho deve ser substituído por um caminho válido no seu sistema.
   ```
   stages {
        stage('Test Network') {
            steps {
                bat 'ipconfig /all > rede.txt'
                bat 'copy rede.txt C:\\seucaminho'
            }
        }
   ```
1. Release IP

Esse estágio possui apenas um passo (steps), que executa o comando ipconfig /release, liberando todos os endereços IP atribuídos dinamicamente pelas interfaces de rede do sistema Windows.
   
   ```
   stage('Release IP') {
            steps {
                bat 'ipconfig /release'
            }
        }
   ```
3. Renew IP

Esse estágio possui apenas um passo (steps), que executa o comando ipconfig /renew, solicitando a renovação dos endereços IP para as interfaces de rede por meio do protocolo DHCP.
   
   ```
   stage('Renew IP') {
            steps {
                bat 'ipconfig /renew'
            }
        }
   ```
5. Flush DNS Cache

Esse estágio possui apenas um passo (steps), que executa o comando ipconfig /flushdns, limpando o cache de resolução de DNS no sistema operacional Windows.
   
   ```
   stage('Flush DNS Cache') {
            steps {
                bat 'ipconfig /flushdns'
            }
        }
   ```
### Post Section

Essa seção é executada após a conclusão de todos os estágios.

Se o pipeline tiver sucesso (success), ele enviará um e-mail para o endereço "seuemail@gexample.com" informando que todas as etapas foram concluídas sem erros.
Se o pipeline falhar (failure), ele enviará um e-mail para o mesmo endereço informando que alguma etapa não foi concluída corretamente e que é necessário verificar os logs para mais detalhes.

Para que esse script pode ser utilizado:
O pipeline pode ser utilizado para realizar ações de manutenção e teste relacionadas à rede em um ambiente Windows, assim como na versão anterior. Ele automatiza as seguintes tarefas:

Test Network:
Obtém informações detalhadas sobre as configurações de rede do sistema Windows, salvando-as em um arquivo rede.txt e copiando-o para o caminho especificado em C:\\seucaminho.

Release IP:
Libera todos os endereços IP atribuídos dinamicamente pelas interfaces de rede do sistema Windows.

Renew IP:
Solicita a renovação dos endereços IP para as interfaces de rede por meio do protocolo DHCP.

Flush DNS Cache:
Limpa o cache de resolução de DNS no sistema operacional Windows.
Assim como mencionado anteriormente, o pipeline pode ser usado para realizar verificações ou manutenções periódicas na rede de um ambiente Windows. Ele pode ser útil em ambientes de desenvolvimento e teste, bem como em cenários de solução de problemas relacionados à rede. Certifique-se de substituir o endereço de e-mail "seuemail@gexample.com" e o caminho C:\\seucaminho pelos valores adequados para o seu ambiente.

## Capturas de tela

Registro da construção e execução do Job no Jenkins.

1. Ordem da imagem
![](fakeimg.png)

2. Ordem da imagem
![](fakeimg.png)
