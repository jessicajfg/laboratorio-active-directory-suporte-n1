# 👥 Laboratório Active Directory — Suporte N1

![Windows Server](https://img.shields.io/badge/Windows%20Server-0078D4?style=flat-square&logo=windows&logoColor=white)
![Active Directory](https://img.shields.io/badge/Active%20Directory-AD%20DS-0078D4?style=flat-square&logo=microsoft&logoColor=white)
![Suporte N1](https://img.shields.io/badge/Suporte-N1-0A66C2?style=flat-square)

Projeto prático desenvolvido para simular rotinas comuns de **Suporte Técnico N1** em um ambiente de domínio Windows com **Active Directory Domain Services (AD DS)**.

O laboratório foi estruturado em cenários próximos do dia a dia de Help Desk e Service Desk: criação e organização de usuários, grupos e OUs, reset e desbloqueio de contas, onboarding, permissões NTFS, compartilhamento de arquivos e validação de acessos.

> **Observação:** todos os usuários, nomes e informações apresentados neste projeto são fictícios e foram criados exclusivamente para fins de estudo.

## 👀 Visão rápida

- domínio Windows configurado em laboratório
- organização de usuários por OUs
- autenticação em estação cliente
- grupos de segurança
- permissões NTFS por grupo
- compartilhamento de arquivos
- reset, bloqueio, desbloqueio e desabilitação de contas
- onboarding de colaborador
- concessão e revogação de acessos
- validação do princípio do menor privilégio
- documentação das evidências de cada cenário

## 🎯 Objetivo

Consolidar conhecimentos de **Active Directory aplicados à rotina de suporte**, praticando administração básica de identidades e acessos em um ambiente corporativo simulado.

## 🛠️ Tecnologias e conceitos

`Windows Server` · `Active Directory` · `AD DS` · `ADUC` · `Group Policy` · `NTFS` · `Compartilhamento de arquivos` · `Hyper-V` · `Windows Client` · `Suporte N1`

## 🖥️ Ambiente do laboratório

| Item | Configuração |
|---|---|
| Domínio | `lab.test` |
| Controlador de domínio | `SRV-DC01` |
| Estação cliente | `CLIENTE01` |
| OUs | `Financeiro` e `RH` |
| Grupo de segurança | `GG_Financeiro` |
| Compartilhamento | `\\SRV-DC01\Financeiro` |

Usuários fictícios utilizados nos testes: **Cecília Luiza, Rafael Martins e Lucas Almeida**.

## 🔧 Cenários praticados

- criação e organização de OUs
- autenticação de usuário em uma estação do domínio
- validação do controlador de domínio utilizado no logon
- criação e utilização de grupos de segurança
- configuração de permissões NTFS por grupo
- validação de leitura e gravação em pasta compartilhada
- revogação de acesso a recurso do setor
- redefinição de senha de usuário
- troca obrigatória de senha no primeiro logon
- configuração e teste de bloqueio de conta
- desbloqueio de usuário pelo Active Directory
- teste de conta desabilitada
- onboarding de novo colaborador
- concessão de acesso por associação a grupo
- validação do princípio do menor privilégio
- documentação de procedimentos e resultados dos testes

## 📸 Evidências

### 1. Configuração do domínio

Domínio `lab.test` configurado no Active Directory Domain Services.

![Configuração do domínio](evidencias/01_Dominio_LabTest.png)

### 2. Organização por unidades organizacionais

Estrutura de OUs criada para organizar usuários dos setores Financeiro e RH.

![Estrutura de OUs](evidencias/02_Estrutura_OUs.png)

### 3. Validação da estação no domínio

Validação da conta autenticada, do controlador `SRV-DC01` e da estação `CLIENTE01` utilizando `whoami`, `%logonserver%` e `hostname`.

![Validação da estação no domínio](evidencias/03_Cliente_Dominio_Validado.png)

### 4. Permissões da pasta Financeiro

O grupo `GG_Financeiro` recebeu permissão **Modify** sobre a pasta compartilhada do setor.

![Permissões NTFS do Financeiro](evidencias/04_Permissoes_NTFS_Financeiro.png)

### 5. Validação do grupo de segurança

O comando `whoami /groups` foi utilizado para confirmar que a sessão da usuária Cecília recebeu o grupo `GG_Financeiro` no token de segurança.

![Grupo Financeiro da Cecília](evidencias/05_Grupo_Financeiro_Cecilia.png)

### 6. Validação de leitura e gravação

A usuária Cecília criou o arquivo `Teste_Cecilia` em `\\SRV-DC01\Financeiro`, confirmando a aplicação das permissões.

![Gravação da Cecília no Financeiro](evidencias/06_Gravacao_Cecilia_Financeiro.png)

### 7. Revogação de acesso

Após a remoção da usuária Cecília do grupo `GG_Financeiro` e a atualização da sessão, o compartilhamento passou a retornar **acesso negado**.

![Acesso negado após revogação](evidencias/07_Acesso_Negado_Apos_Revogacao.png)

## 🔐 Gestão de contas e credenciais

### 8. Redefinição de senha

Foi realizada a redefinição da senha da usuária pelo Active Directory, utilizando uma credencial temporária sem exposição da senha na documentação.

![Redefinição de senha](evidencias/08_Redefinicao_Senha_Cecilia.png)

### 9. Troca obrigatória no primeiro logon

Após a redefinição, o Windows exigiu que a usuária definisse uma nova senha antes de concluir o acesso.

![Troca de senha no primeiro logon](evidencias/09_Troca_Senha_Primeiro_Logon.png)

### 10. Política de bloqueio de conta

Para a simulação, foi configurada uma política de bloqueio após três tentativas inválidas, com duração e redefinição do contador em 30 minutos.

> Configuração utilizada apenas para fins de demonstração no laboratório; não representa uma recomendação universal para ambientes de produção.

![Política de bloqueio](evidencias/10_Politica_Bloqueio_Conta.png)

### 11. Validação do bloqueio de conta

Após tentativas consecutivas com senha incorreta, a conta foi bloqueada conforme a política aplicada.

![Conta bloqueada](evidencias/11_Conta_Bloqueada_Cecilia.png)

### 12. Desbloqueio de conta no AD

A conta bloqueada foi identificada nas propriedades do usuário e desbloqueada pelo Active Directory Users and Computers.

![Desbloqueio de conta](evidencias/12_Desbloqueio_Conta_Cecilia.png)

### 13. Conta desabilitada

Também foi validado o comportamento de uma conta desabilitada. A tentativa de autenticação na estação foi corretamente negada.

![Conta desabilitada](evidencias/13_Conta_Desabilitada_Login_Negado.png)

## 👤 Onboarding de novo colaborador

### 14. Criação do usuário

Foi simulada a admissão de Rafael Martins no setor Financeiro, com criação da conta dentro da OU correspondente.

![Criação do Rafael](evidencias/14_Onboarding_Rafael_Criacao.png)

### 15. Concessão de acesso por grupo

Rafael Martins foi adicionado ao grupo `GG_Financeiro`, recebendo as permissões vinculadas ao grupo em vez de permissões concedidas diretamente à conta.

![Rafael no grupo Financeiro](evidencias/15_Onboarding_Rafael_Grupo.png)

### 16. Validação do onboarding

Após o primeiro acesso, o novo usuário conseguiu utilizar o compartilhamento e criar o arquivo `Teste_Rafael`, confirmando a aplicação das permissões.

![Validação do onboarding](evidencias/16_Onboarding_Rafael_Validacao.png)

## 🛡️ Princípio do menor privilégio

### 17. Acesso negado para usuário não autorizado

Uma conta sem associação ao `GG_Financeiro` tentou acessar o compartilhamento do setor e recebeu **acesso negado**, validando que somente usuários autorizados possuíam acesso ao recurso.

![Menor privilégio](evidencias/17_Menor_Privilegio_Acesso_Negado.png)

## 💡 Competências demonstradas

- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- criação e organização de usuários e OUs
- grupos de segurança
- gerenciamento de permissões NTFS
- compartilhamento de arquivos em rede
- reset e troca de senha
- bloqueio e desbloqueio de contas
- habilitação e desabilitação de usuários
- onboarding e gestão de acessos
- princípio do menor privilégio
- troubleshooting de autenticação e permissões
- documentação técnica
- rotinas de Suporte Técnico N1

## ✅ Resultado

O laboratório permitiu executar e validar atividades recorrentes de suporte em ambientes com Active Directory, desde a criação de contas até a concessão, teste e revogação de acessos.

Além da execução técnica, os cenários foram documentados com foco em **clareza, rastreabilidade e continuidade do atendimento**.

---

[← Voltar ao meu portfólio](https://github.com/jessicajfg)
