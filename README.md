📊 Gestor de Cobranças e Rotas
Aplicação web responsiva e leve para gestão de devedores e planejamento de rotas de cobranças. O app se conecta ao Supabase para persistência de dados e se integra ao Google Maps para navegação.

🚀 Funcionalidades
Gestão de Devedores: Cadastro de clientes com dívida total, saldo restante e endereço.
Planejamento de Rotas: Selecione clientes e adicione à "Rota do Dia" com valores planejados.
Navegação: Integração direta com o Google Maps para roteamento até o cliente.
Controle Financeiro:
Registro de Valor Planejado vs. Valor Real Recebido.
Campo de observações para anotações específicas (ex: "Pagou com cheque").
Atualização automática do saldo devedor.
Relatório Diário: Ao finalizar a rota, gera um resumo visual com barra de progresso de meta e botão para envio via WhatsApp.
Modais de Detalhes: Visualização completa do cliente, histórico de pagamentos (calculado) e opções de edição/exclusão.
🛠 Tecnologias Utilizadas
Frontend: HTML5, CSS3, JavaScript (Vanilla)
Backend/Database: Supabase (PostgreSQL)
Deploy Recomendado: Vercel ou GitHub Pages
⚙️ Como Instalar e Rodar
1. Clonar o Repositório
Clone ou faça o download deste projeto para sua máquina.

git clone https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.gitcd NOME-DO-REPOSITORIO
2. Configuração do Banco de Dados (Supabase)
Crie uma conta no Supabase.com.
Crie um novo projeto.
No SQL Editor, execute o código abaixo para criar a tabela necessária:
sql

-- Criação da tabela de devedores
create table debtors (
  id uuid default gen_random_uuid() primary key,
  created_at timestamp with time zone default timezone('utc'::text, now()) not null,
  name text not null,
  address text,
  total numeric default 0,
  remaining numeric default 0,
  lat numeric,
  lng numeric,
  in_route boolean default false,
  due_today numeric default 0,
  observations text
);

-- Ativar Segurança (RLS)
alter table debtors enable row level security;

-- Política de acesso público (para funcionar sem login complexo)
create policy "Acesso Público" on debtors
  for all
  using (true)
  with check (true);
3. Conectar o App ao Banco
Abra o arquivo index.html e procure pelo bloco de script no final (linhas 430+ aproximadamente). Substitua as constantes vazias pelas suas chaves do Supabase (encontradas em Settings > API):

javascript

const SUPABASE_URL = 'SUA_URL_DO_PROJETO_AQUI';
const SUPABASE_ANON_KEY = 'SUA_KEY_ANONIMA_AQUI';
4. Executar Localmente
Como é um projeto estático (HTML/CSS/JS puro), basta abrir o arquivo index.html no seu navegador:

bash

# No macOS
open index.html

# No Windows
start index.html

# Ou utilize o Live Server (VS Code Extension)
🌐 Deploy (Hospedagem)
Opção 1: Vercel (Recomendado)
Acesse Vercel.com e faça login com o GitHub.
Clique em "Add New..." > "Project".
Importe o repositório deste projeto.
O Vercel detectará automaticamente como um projeto estático.
Clique em Deploy.
Opção 2: GitHub Pages
No seu repositório no GitHub, vá em Settings.
Na aba lateral, clique em Pages.
Em Source, selecione main branch.
Salve e aguarde o site ficar online.
📱 Uso
Cadastre os devedores: Vá na aba "Cadastrar" e insira os dados dos clientes.
Planeje a Rota: Na aba "Devedores", clique em "Cobrar" para adicionar à rota do dia.
Inicie: Na aba "Rota", clique em "Iniciar Navegação".
Execute: Visite cada cliente, clique em "Abrir Navegação" para chegar até ele, insira o valor real recebido e as observações.
Finalize: Ao chegar no fim, confira o relatório e envie para seu chefe via WhatsApp.
📝 Contribuindo
Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou pull requests.

📄 Licença
Este projeto está sob a licença MIT.
