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


Guia de Testes – Site Institucional Acadêmico

Este guia mostra, passo a passo, como baixar o projeto, instalar o que é preciso, configurar o banco de dados e testar todas as funcionalidades do site. Foi escrito para quem nunca abriu o projeto.

Sobre os testes: o projeto não possui testes automatizados (não há PHPUnit nem package.json). Por isso, a validação é feita por uma checagem de sintaxe (seção 8) e por um roteiro de testes manuais (seção 9).

Sumário
O que você vai precisar
Baixar o projeto
Extrair os arquivos
Instalar o PHP e o servidor local
Criar o banco de dados
Configurar a conexão com o banco
Abrir o site
Checagem de sintaxe
Roteiro de testes manuais
Problemas conhecidos
Problemas comuns
Registro de falhas
1. O que você vai precisar
Computador com Windows 10 ou 11
Navegador (Chrome, Edge ou Firefox)
XAMPP (inclui Apache e PHP)
7-Zip ou WinRAR (para abrir o arquivo .rar)
Um banco PostgreSQL: pode ser um projeto gratuito no Neon ou um PostgreSQL instalado no computador
Opcional: VS Code para editar arquivos
2. Baixar o projeto
Abra a página do repositório no GitHub.
Clique no botão verde Code.
Clique em Download ZIP.
O arquivo Site-Institucional-main.zip será salvo na pasta Downloads.
3. Extrair os arquivos

O projeto vem em duas camadas compactadas: primeiro o .zip do GitHub e, dentro dele, um arquivo .rar.

Clique com o botão direito em Site-Institucional-main.zip e escolha Extrair Tudo....
Abra a pasta Site-Institucional-main. Dentro dela há o README.md e o arquivo site-institucional.rar.
Clique com o botão direito em site-institucional.rar e escolha 7-Zip > Extrair aqui (ou WinRAR > Extrair aqui).
Será criada a pasta site-institucional com esta estrutura:
site-institucional/
├── admin/        Área administrativa (painel, editar/excluir posts, mensagens)
├── config/       Conexão com o banco (conexao.php) e upload
├── public/       Páginas públicas (index, sobre, noticias, post, contato, login, logout)
└── publico/
    └── uploads/  Imagens enviadas nas notícias
4. Instalar o PHP e o servidor local
Instale o XAMPP com as opções padrão.
Copie a pasta site-institucional para C:\xampp\htdocs\.
Habilite as extensões do PostgreSQL:
Abra o XAMPP Control Panel.
Na linha do Apache, clique em Config > PHP (php.ini).
Procure as linhas ;extension=pdo_pgsql e ;extension=pgsql e apague o ; do início de cada uma.
Salve o arquivo.
No XAMPP Control Panel, clique em Start no Apache.

Para confirmar que as extensões estão ativas, abra o Prompt de Comando e execute:

bash
C:\xampp\php\php.exe -m | findstr pgsql

Devem aparecer pdo_pgsql e pgsql.

5. Criar o banco de dados

O site lê e grava em quatro tabelas. O script abaixo foi montado a partir das consultas do código; se o projeto tiver um script oficial, use o oficial.

Crie um banco PostgreSQL (no Neon: New Project).
Abra o editor SQL (no Neon: SQL Editor) e execute:
sql
CREATE TABLE clientes (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100) NOT NULL,
  email VARCHAR(150) UNIQUE NOT NULL,
  senha VARCHAR(255) NOT NULL,
  tipo VARCHAR(20) NOT NULL DEFAULT 'usuario'
);

CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  titulo VARCHAR(255) NOT NULL,
  conteudo TEXT NOT NULL,
  imagem VARCHAR(255) DEFAULT '',
  data_criacao TIMESTAMP DEFAULT NOW()
);

CREATE TABLE paginas_conteudo (
  id SERIAL PRIMARY KEY,
  pagina VARCHAR(50) NOT NULL,
  secao VARCHAR(50) NOT NULL,
  conteudo TEXT,
  ultima_atualizacao TIMESTAMP DEFAULT NOW(),
  UNIQUE (pagina, secao)
);

CREATE TABLE mensagens_contato (
  id SERIAL PRIMARY KEY,
  nome VARCHAR(100) NOT NULL,
  email VARCHAR(150) NOT NULL,
  assunto VARCHAR(150) NOT NULL,
  mensagem TEXT NOT NULL,
  data_envio TIMESTAMP DEFAULT NOW(),
  lida BOOLEAN DEFAULT FALSE
);
Criar o usuário administrador de teste

A senha é guardada com hash, então não dá para inserir 1234 direto. Gere o hash no Prompt de Comando:

bash
C:\xampp\php\php.exe -r "echo password_hash('1234', PASSWORD_DEFAULT);"

Copie o resultado (começa com $2y$) e execute no SQL, trocando COLE_O_HASH_AQUI:

sql
INSERT INTO clientes (nome, email, senha, tipo)
VALUES ('Administrador', 'adm@gmail.com', 'COLE_O_HASH_AQUI', 'admin');

Se quiser testar também o login de usuário comum, repita com outro e-mail e tipo = 'usuario'.

Credenciais de teste: e-mail adm@gmail.com e senha 1234. Use somente em ambiente de teste. Nunca use essa senha em um site publicado.

6. Configurar a conexão com o banco

Abra o arquivo config/conexao.php e troque os dados pelos do seu banco:

php
$host        = 'SEU_HOST';
$user        = 'SEU_USUARIO';
$password    = 'SUA_SENHA';
$dbname      = 'SEU_BANCO';
$endpoint_id = 'SEU_ENDPOINT';   // só no Neon; veja a connection string do projeto

O arquivo admin/mensagens.php tem uma segunda cópia desses dados, escrita direto no código. Edite os mesmos campos nele também.

Segurança: não envie senhas reais para o GitHub. Se o repositório for público, qualquer pessoa consegue ler o que estiver escrito nesses arquivos. O ideal é ler os dados de variáveis de ambiente (por exemplo, getenv('DB_PASSWORD')) e, se uma senha já foi publicada, trocá-la no painel do banco.

7. Abrir o site

Com o Apache ligado, acesse no navegador:

Página	Endereço
Início	http://localhost/site-institucional/public/index.php
Sobre	http://localhost/site-institucional/public/sobre.php
Notícias	http://localhost/site-institucional/public/noticias.php
Contato	http://localhost/site-institucional/public/contato.php
Login	http://localhost/site-institucional/public/login.php
Painel admin	http://localhost/site-institucional/admin/painel.php
Mensagens	http://localhost/site-institucional/admin/mensagens.php

Dica: o endereço .../public/admin.php redireciona automaticamente para o login.

Se a página inicial abrir sem erro, o ambiente está pronto.

8. Checagem de sintaxe

Verifica se algum arquivo PHP tem erro de escrita. No PowerShell, dentro da pasta site-institucional:

powershell
Get-ChildItem -Recurse -Filter *.php | ForEach-Object { C:\xampp\php\php.exe -l $_.FullName }

Resultado esperado: No syntax errors detected in ... para todos os arquivos.

9. Roteiro de testes manuais

Marque cada item ao concluir. Em caso de falha, anote na seção 12.

9.1 Páginas públicas
 A página inicial abre e mostra as seções (cursos, campus, notícias, depoimentos)
 As páginas Sobre, Notícias e Contato abrem sem erro
 O menu de navegação leva à página correta
 Layout responsivo: pressione F12, ative o modo dispositivo e teste 375 px (celular), 768 px (tablet) e 1280 px (desktop)
 Nenhuma imagem aparece quebrada
9.2 Login e logout
 Login com adm@gmail.com / 1234 leva ao painel (admin/painel.php)
 Senha errada mostra "Email ou senha inválidos."
 Campos vazios mostram "Preencha todos os campos."
 Usuário comum (tipo = usuario) é levado a contato.php
 public/admin.php redireciona para login.php
 Logout encerra a sessão e volta para a página inicial
 Depois do logout, voltar com a seta do navegador não dá acesso ao painel
9.3 Controle de acesso (sem estar logado)

Abra uma janela anônima e tente acessar diretamente:

 admin/painel.php redireciona para o login
 admin/editarpost.php?id=1 redireciona para o login
 admin/excluirpost.php?id=1 redireciona para o login e não exclui o post
 admin/mensagens.php pede login (veja o item 1 dos problemas conhecidos)
9.4 Notícias (logado como administrador)
 Criar post com título, conteúdo e imagem
 Criar post sem imagem
 Tentar criar post sem título ou sem conteúdo mostra "Preencha título e conteúdo!"
 O post novo aparece na página inicial (mostra os 3 mais recentes) e em noticias.php
 Abrir o post completo (post.php?id=...) mostra título, texto e imagem
 post.php?id=abc e post.php?id=99999 não quebram a página
 A seção de posts relacionados aparece
 Editar um post (título e texto) e salvar
 Trocar a imagem de um post
 Marcar "remover imagem" em um post
 Excluir um post: ele some da lista e da página pública
9.5 Busca de notícias
 Buscar por uma palavra do título encontra o post
 Buscar por uma palavra do conteúdo encontra o post
 O termo pesquisado aparece destacado
 Buscar algo que não existe mostra mensagem de "nenhum resultado" sem erro
 Buscar com letra maiúscula e minúscula (por exemplo Campus e campus) dá o mesmo resultado
9.6 Upload de imagem
 Arquivo .jpg, .png e .gif é aceito
 Arquivo .pdf ou .txt é recusado com "Tipo de arquivo não permitido..."
 A imagem enviada aparece na pasta publico/uploads/
9.7 Formulário de contato
 Preencher todos os campos e enviar mostra mensagem de sucesso
 Enviar com campos vazios é bloqueado
 Enviar com e-mail inválido (teste@) é bloqueado
 A mensagem enviada aparece em admin/mensagens.php
 O botão marcar como lida altera o status da mensagem
9.8 Conteúdo dinâmico das páginas
 No painel, editar o texto de uma seção da página e salvar mostra sucesso (veja o item 2 dos problemas conhecidos)
 O texto novo aparece na página pública
 Com a tabela paginas_conteudo vazia, a página abre com os textos padrão, sem erro
9.9 Segurança básica
 Criar um post com o título <script>alert(1)</script>: o texto deve aparecer como texto, sem abrir janela de alerta (XSS)
 Buscar por ' OR '1'='1 em Notícias: não pode dar erro nem listar tudo indevidamente (SQL Injection)
 Na tela de login, usar ' OR '1'='1 como e-mail: não pode autenticar
10. Problemas conhecidos

Pontos encontrados ao ler o código. Confirme durante os testes e, se forem reais, corrija antes da entrega.

admin/mensagens.php não verifica login. O arquivo não inicia sessão nem confere se o usuário é administrador. Qualquer pessoa que souber o endereço consegue ler as mensagens de contato. Correção: acrescentar no início o mesmo bloco de verificação usado em painel.php.
Salvar conteúdo de página no painel pode dar erro. O painel.php usa ON DUPLICATE KEY UPDATE, que é sintaxe do MySQL, mas o banco configurado é PostgreSQL. Erro esperado: syntax error at or near "DUPLICATE". Correção:
sql
   INSERT INTO paginas_conteudo (pagina, secao, conteudo)
   VALUES (:pagina, :secao, :conteudo)
   ON CONFLICT (pagina, secao)
   DO UPDATE SET conteudo = EXCLUDED.conteudo, ultima_atualizacao = NOW()
Redirecionamento para pasta inexistente. editarpost.php e excluirpost.php mandam o visitante sem login para ../publico/login.php, mas o login fica em public/ (sem o "o" final). Resultado: erro 404 em vez da tela de login.
Credenciais do banco dentro do código. Usuário e senha do banco aparecem em config/conexao.php e em admin/mensagens.php.
README original diverge do código. O README fala em MySQL, mas o código conecta em PostgreSQL (pgsql).
Exclusão por link simples. excluirpost.php?id=... apaga o post com uma requisição GET, sem confirmação nem proteção contra CSRF.
11. Problemas comuns

could not find driver As extensões pdo_pgsql e pgsql não estão habilitadas. Refaça o passo 3 da seção 4 e reinicie o Apache.

Erro na conexão com o banco de dados Confira host, usuário, senha, nome do banco e endpoint_id em config/conexao.php. No Neon, copie os dados da connection string do projeto.

Login não funciona com a senha correta Verifique se o usuário existe na tabela clientes, se a coluna senha guarda o hash (e não 1234 puro) e se tipo é exatamente admin.

Apache não inicia (porta 80 em uso) Outro programa está usando a porta. Feche-o (Skype e IIS são comuns) ou mude a porta em Config > httpd.conf.

Imagem do post não aparece Confirme que a pasta publico/uploads/ existe e que o arquivo foi salvo nela. O banco guarda o caminho uploads/arquivo.jpg.

Página em branco Abra C:\xampp\apache\logs\error.log e leia a última linha: ela indica o arquivo e a linha do erro.
