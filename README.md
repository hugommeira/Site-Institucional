Site Institucional Acadêmico com Sistema de Notícias e Autenticação

Este projeto consiste no desenvolvimento de um site institucional acadêmico, inspirado em universidades de grande porte, desenvolvido como trabalho do curso técnico em Tecnologia da Informação.
A aplicação foi construída utilizando PHP procedural, PDO, MySQL, HTML5, CSS3 e JavaScript, com foco em organização de código, segurança básica, dinamismo de conteúdo e experiência do usuário.
O sistema integra conteúdo institucional dinâmico, sistema de autenticação, gerenciamento e exibição de notícias, além da separação entre áreas públicas e administrativas.

⚙️ Funcionalidades Principais

🔐 Sistema de Autenticação

Login com verificação segura de senha (password_verify)
Controle de sessão com $_SESSION
Diferenciação de usuários por tipo (admin / usuário)
Redirecionamento automático conforme o perfil do usuário
Logout seguro com destruição completa da sessão

📰 Sistema de Notícias

Listagem dinâmica de notícias armazenadas no banco de dados
Exibição das notícias mais recentes na página inicial
Página dedicada para visualização completa das notícias
Sistema de busca por título ou conteúdo
Destaque visual do termo pesquisado
Resumo automático do conteúdo das notícias
Exibição automática de posts relacionados

🧩 Conteúdo Dinâmico

Conteúdo da página inicial carregado diretamente do banco de dados
Fallback automático para conteúdo padrão em caso de erro no banco
Uso de PDO com prepared statements, evitando SQL Injection

🎨 Interface e UX

Layout responsivo (desktop e mobile)
Menu de navegação dinâmico com JavaScript
Estilização moderna com CSS customizado
Uso de ícones via Font Awesome
Organização visual clara entre seções (Cursos, Campus, Notícias, Depoimentos, etc.)

🗂️ Estrutura do Projeto
/public
 ├─ Páginas públicas (index, notícias, post, login, logout)
 └─ Redirecionamentos de segurança para páginas restritas
/admin
 └─ Área administrativa (painel do administrador)
/config
 └─ Arquivo de conexão com o banco de dados
/assets
 └─ Estilos CSS, imagens e ícones

🔒 Boas Práticas Aplicadas

Uso de htmlspecialchars() para evitar XSS
Prepared Statements com PDO
Validação de parâmetros via GET e POST
Separação lógica entre frontend e backend
Controle de acesso por sessão
Tratamento de erros com fallback de conteúdo

🧪 Dados de Acesso (Ambiente de Teste)

🔑 Acesso ao login
Troque o final da URL para /admin
Exemplo:
site-institucional/public/index.php → site-institucional/public/admin.php

👤 Usuário administrador
Email: adm@gmail.com
Senha: 1234

🧠 Objetivo do Projeto

Este projeto teve como objetivo consolidar conhecimentos do curso técnico em TI, aplicando conceitos fundamentais de:
Programação Web com PHP
Banco de dados relacional
Segurança básica em aplicações web
Estruturação de sistemas reais
Boas práticas de desenvolvimento

🚀 Tecnologias Utilizadas

PHP
MySQL
PDO
HTML5
CSS3
JavaScript
Font Awesome
Google Fonts
