# Estudo de Caso 05: IPAM / Infraestrutura como Código (NetBox)
*Fonte única de verdade para a infraestrutura de rede · estudo de caso anonimizado*

## Contexto
Inventário de IPs, VMs e topologia espalhado em planilhas, sem fonte única de verdade: dificultando auditoria, troubleshooting e planejamento.

## Desafio
Centralizar o inventário da infraestrutura multi-cloud em uma plataforma versionada, com sincronização automática e implantação repetível.

## Solução / Arquitetura
- **NetBox** (IPAM/DCIM) containerizado com PostgreSQL e Nginx/SSL, implantado via **Docker Compose**.
- **Sincronização automática** das VMs e IPs do ambiente cloud para a topologia, via Python (pynetbox) e importações estruturadas.
- **Pipeline CI/CD** (Azure DevOps) com backup pré-deploy, build, migrações e *health checks*.

## Stack
Docker · NetBox · PostgreSQL · Python (pynetbox) · Nginx/SSL · Azure DevOps.

## Resultado
- Inventário de dezenas de VMs em múltiplas zonas de disponibilidade centralizado e auditável.
- Redução do esforço manual de manutenção do inventário e base confiável para decisões de rede.

## Meu papel
Implantação da plataforma, automação da sincronização com o ambiente cloud e o pipeline de deploy.

---
*Outros trabalhos de infraestrutura na mesma linha (não detalhados): automação de migração de zonas DNS (BIND), versionamento de baseline de firewall (FortiGate), backup seguro de sistema de acesso físico com criptografia AES-256 e cofre de chaves.*
