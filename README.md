# Doc-script
Esboço da estrutura de documentação do script pipeline de automação de login de um roteador.

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

1. Configuração do ambiente
   
   ```
   insira o primeiro stage do script
   ```
2. Backup de configuração do roteador
   
   ```
   insira o segundo stage do script
   ```
3. Notificação
   
   ```
   insira o terceiro stage do script
   ```


## Capturas de tela

Registro da construção e execução do Job no Jenkins.

1. Descreva a imagem
![](fakeimg.png)

2. Descreva a imagem
![](fakeimg.png)
