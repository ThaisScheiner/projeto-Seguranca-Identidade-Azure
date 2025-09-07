# Boas Práticas de Segurança e Identidade no Azure com Microsoft Entra ID

## Projeto Segurança e Identidade no Azure - Bootcamp AZ900

A base para proteger recursos na nuvem Azure é o **Microsoft Entra ID** (anteriormente conhecido como Azure Active Directory), o serviço de gerenciamento de identidade e acesso multilocatário da Microsoft. Ele é o coração da segurança, controlando quem pode acessar o quê, sob quais condições.

## Componentes Fundamentais do Entra ID

Para proteger o ambiente de forma eficaz, é crucial entender seus componentes:

* **Usuários:** São a representação de indivíduos que precisam de acesso. Existem dois tipos principais:
    * **Membros:** Contas internas da organização, pertencentes ao tenant.
    * **Convidados (Guests):** Identidades externas convidadas para colaborar, um conceito conhecido como **B2B (Business-to-Business)**.

* **Grupos:** Permitem agrupar usuários para atribuir permissões de forma coletiva, o que é uma prática fundamental para a manutenibilidade. Os grupos podem ser de segurança (para conceder acesso) ou do Microsoft 365 (para colaboração) e podem ser preenchidos manual ou dinamicamente com base em regras.

* **Entidades Externas:** Parceiros ou fornecedores são gerenciados de forma segura, permitindo que usem suas próprias identidades corporativas para acessar os recursos da sua organização.

## Gerenciamento de Permissões e Acesso Privilegiado

O controle sobre o que usuários e grupos podem fazer é gerenciado através de funções (roles) e administradores, seguindo o **Princípio do Menor Privilégio**: conceder apenas as permissões estritamente necessárias.

* **Funções do Entra ID vs. RBAC do Azure:**
    * **Funções do Entra ID** (ex: Administrador Global) gerenciam o próprio diretório.
    * **Controle de Acesso Baseado em Função (RBAC) do Azure** concede permissões para gerenciar recursos do Azure (VMs, bancos de dados, redes).

* **Privileged Identity Management (PIM):** Uma prática recomendada avançada que permite o acesso *"just-in-time"* a funções privilegiadas, exigindo que administradores solicitem e justifiquem a ativação de suas permissões por um tempo limitado.

## Vigilância Contínua: Auditoria e Logs

A segurança não é apenas sobre configuração, mas também sobre vigilância contínua. O Microsoft Entra ID gera logs detalhados para auditoria e investigação:

* **Logs de entrada (Sign-in logs):** Registram quem está tentando acessar, de onde, com qual dispositivo e o resultado da autenticação (incluindo uso de MFA).
* **Logs de auditoria (Audit logs):** Rastreiam todas as alterações de configuração no tenant (criação de usuário, atribuição de função, etc.).

Analisar esses logs, idealmente de forma centralizada em uma solução de SIEM como o **Microsoft Sentinel**, permite detectar atividades suspeitas.

## Fortalecendo o Acesso: MFA e Acesso Condicional

Para fortalecer ainda mais o acesso, duas ferramentas são essenciais:

* **MFA (Multi-Factor Authentication):** Considerada a prática de segurança mais eficaz, adicionando uma camada extra de verificação além da senha.
* **Políticas de Acesso Condicional (Conditional Access):** Atuam como um motor de regras "se-então" (ex: *se* o usuário vem de uma rede não confiável, *então* exija MFA). São a principal ferramenta para aplicar os princípios de uma arquitetura **Zero Trust**.

## Gerenciamento do Ciclo de Vida do Usuário

A gestão do ciclo de vida do usuário inclui o que acontece após a exclusão de uma conta.

* **Exclusão Reversível (Soft-Delete):** Quando um usuário é deletado, ele entra em um estado de "exclusão reversível". Ele pode ser totalmente restaurado com todas as suas propriedades e grupos.
* **Período de Retenção:** Por padrão, os usuários deletados permanecem nesse estado por **30 dias**. Após esse período, a exclusão é permanente e irreversível.

## Conclusão

Proteger o Azure é um exercício contínuo que começa com uma base sólida de identidade no Entra ID, reforçada por controles de acesso rigorosos como MFA e Acesso Condicional, e mantida através de monitoramento vigilante de logs e um ciclo de vida de identidade bem gerenciado.
