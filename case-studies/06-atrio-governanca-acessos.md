# Estudo de Caso 06: Átrio — Governança de Acessos e Privilégios
*Plataforma própria de governança de identidades, acessos, ativos e privilégios · estudo de caso anonimizado*

## Contexto
O controle de acesso corporativo via SSO (Entra ID) cobre bem as aplicações integradas — mas deixa de fora uma parte crítica e invisível: os acessos que **não passam por SSO**. Credenciais de portais bancários, portais de fornecedores e parceiros, sistemas legados e contas compartilhadas ficavam dispersos, sem inventário, sem dono claro e sem trilha de auditoria — um ponto cego de segurança e de conformidade.

## Desafio
Ter uma **fonte única da verdade** sobre "quem tem acesso a quê", unificando: (a) os acessos governados por SSO/Entra ID; (b) os acessos **sem SSO** (bancos, portais de fornecedores/parceiros, sistemas legados, contas compartilhadas); e (c) os ativos e privilégios associados a cada pessoa — com detecção automática de desvios e uma cadeia de aprovação auditável.

## Solução / Arquitetura
Plataforma web própria (Flask + PostgreSQL, em contêiner na nuvem, atrás de SSO corporativo) que:
- **Conectores ao vivo como fonte da verdade** — sincroniza automaticamente identidades, dispositivos, acessos e privilégios de múltiplas fontes (diretório/Entra ID, MDM, service desk, EDR, colaboração), em vez de planilhas manuais.
- **Registro de acessos SEM SSO** — cadastro governado dos acessos que o SSO não cobre (portais bancários, fornecedores, parceiros, sistemas legados, contas compartilhadas), cada um com dono, justificativa e revisão periódica.
- **Detecção automática de desvios** — contas desligadas ainda com acesso, acesso fora do perfil da função, privilégio sem aprovação formal, ativo atribuído a uma pessoa mas em uso por outra.
- **Cadeia de concessão auditável** — solicitação → aprovação → execução → revisão, integrada ao service desk e alinhada à ISO 27001.
- **RBAC granular** por módulo e por área.

## Stack
Python (Flask) · PostgreSQL · SSO/OIDC · APIs de diretório, MDM, EDR e service desk · contêiner em nuvem · CI/CD.

## Diferencial vs. ferramentas de mercado
As soluções de IAM/SSO de mercado governam bem o que está **dentro** do SSO, mas tratam o acesso fora dele (bancos, portais de fornecedores/parceiros, contas compartilhadas) como um problema separado de "cofre de senhas", desconectado da governança de identidade. O Átrio une as duas visões em **um único inventário de acessos — com e sem SSO — cruzado com pessoas, ativos e privilégios**, com detecção de desvio e trilha de aprovação. É **governança de acesso de ponta a ponta, não apenas autenticação**.

## Critérios de segurança
- Credenciais e segredos via cofre / variáveis de ambiente — nada em código.
- Plataforma atrás de SSO corporativo; RBAC por papel e área.
- Trilha de auditoria (append-only) das concessões e revisões.
- Menor privilégio nas integrações (somente leitura onde possível).
- Sem PII exposta; campos sensíveis cifrados.

## Resultado
- Visão única de "quem acessa o quê", incluindo os acessos historicamente invisíveis (sem SSO).
- Detecção automática de acessos residuais de desligados e de privilégios sem aprovação — reduzindo risco e esforço de auditoria.
- Cadeia de concessão auditável, fortalecendo a conformidade ISO/IEC 27001:2022.
