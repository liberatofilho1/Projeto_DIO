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

```bash
nmap -sV -p 21,139,445 192.168.56.102
