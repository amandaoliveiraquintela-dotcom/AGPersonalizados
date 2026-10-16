# AG Personalizados: painel de gestão

Painel de pedidos, preços, investimentos e divisão entre sócios da AG Personalizados.

- **Página:** hospedada no GitHub Pages, de graça.
- **Dados:** guardados no Firebase (Firestore), do Google. O plano gratuito sobra para o volume de vocês.
- **Acesso:** só entra quem fizer login com uma conta Google autorizada.

O código fica público no GitHub, mas os dados não: eles ficam no Firebase, protegidos pelo login e pelas regras de acesso.

## Arquivos

| Arquivo | Para que serve |
|---|---|
| `index.html` | O painel inteiro |
| `config.js` | A "chave" do seu projeto Firebase (você preenche no passo 5) |
| `firestore.rules` | Modelo das regras de acesso (você cola no Firebase no passo 3) |
| `README.md` | Este passo a passo |

---

## Instalação (uns 20 minutos, uma vez só)

Os nomes dos botões podem variar um pouco, porque o Google e o GitHub mudam as telas de vez em quando.

### Parte 1: Firebase (o banco de dados)

**1. Criar o projeto**
Entre em https://console.firebase.google.com com a sua conta Google e clique em **Criar projeto**. Dê o nome `ag-personalizados`. O Google Analytics pode ficar desativado.

**2. Criar o banco**
No menu, abra **Firestore Database** e clique em **Criar banco de dados**.
- Local: `southamerica-east1 (São Paulo)`.
- Modo: **produção**.

**3. Colar as regras de acesso**
Ainda no Firestore, abra a aba **Regras**. Apague o que estiver lá e cole o conteúdo do arquivo `firestore.rules`. Troque os dois e-mails de exemplo pelos e-mails Google de vocês e clique em **Publicar**.

Para dar acesso a mais alguém no futuro, basta incluir o e-mail na lista e publicar de novo.

**4. Ligar o login com Google**
No menu, abra **Authentication**, clique em **Vamos começar** e depois em **Google**. Ative a opção, escolha o seu e-mail de suporte e salve.

**5. Pegar a configuração do app**
Clique na engrenagem ao lado de "Visão geral do projeto" e entre em **Configurações do projeto**. Em **Seus apps**, clique no ícone **`</>`** (Web), dê o nome `painel` e registre. **Não** precisa marcar o Firebase Hosting.

O Firebase vai mostrar um bloco `const firebaseConfig = { ... }`. Copie os valores para o arquivo `config.js`, no lugar de cada `COLE_AQUI`.

### Parte 2: GitHub (a página)

**6. Criar o repositório e enviar os arquivos**
Em https://github.com/new, crie um repositório chamado `ag-personalizados`, do tipo **Public**. O GitHub Pages gratuito só funciona com repositório público.

Depois, clique em **Add file > Upload files**, arraste `index.html`, `config.js` (já preenchido), `firestore.rules` e `README.md`, e clique em **Commit changes**.

**7. Ligar o GitHub Pages**
No repositório, abra **Settings > Pages**. Em "Source", escolha **Deploy from a branch**, a branch `main` e a pasta `/ (root)`, e salve.

Em 1 ou 2 minutos aparece o link: `https://SEU-USUARIO.github.io/ag-personalizados/`

**8. Autorizar o endereço no Firebase**
Volte ao Firebase e abra **Authentication > Configurações > Domínios autorizados**. Clique em **Adicionar domínio** e coloque `SEU-USUARIO.github.io`, sem `https://` e sem o `/ag-personalizados`.

**9. Entrar e trazer os dados do Claude**
Abra o link, clique em **Entrar com Google** e escolha a conta autorizada.

Para trazer o que vocês já lançaram no painel do Claude:
1. No painel do Claude, entre em **Financeiro e sócios > Exportar para Excel**.
2. No painel novo, entre em **Financeiro e sócios > Importar backup**, escolha a planilha e use a opção **Juntar**.

Pronto. É só passar o link para o sócio; ele entra com a conta Google dele, que precisa estar nas regras do passo 3.

---

## Uso no dia a dia

- **Pelo celular:** abra o link no navegador e use "Adicionar à tela inicial". Ele vira um ícone, como um aplicativo.
- **Sem internet:** o que for lançado fica guardado no aparelho e é enviado quando a conexão voltar.
- **Backup:** o plano gratuito do Firebase não faz cópia automática. Usem **Exportar para Excel** toda semana e guardem no Google Drive. O painel avisa na Visão geral quando o último backup tem mais de 7 dias.
- **Mudar o painel:** quando o `index.html` for atualizado, basta enviar o arquivo novo no repositório (Add file > Upload files). Os dados não são afetados, porque ficam no Firebase.

## Problemas comuns

| O que aparece | O que fazer |
|---|---|
| "Falta conectar o banco de dados" | O `config.js` ainda tem `COLE_AQUI`. Refaça o passo 5. |
| "Este endereço ainda não foi autorizado no Firebase" | Refaça o passo 8. |
| "Esta conta não tem acesso" | O e-mail não está nas regras. Refaça o passo 3. |
| Página do GitHub mostra erro 404 | Espere 2 minutos depois do passo 7 e confira se o arquivo se chama exatamente `index.html`. |

## Limites do plano gratuito (Spark)

Por dia: 50 mil leituras e 20 mil gravações, com 1 GB de armazenamento. Para dois sócios lançando pedidos, isso dá folga por muito tempo.

Cada vez que o painel abre, ele lê todos os registros. Se um dia passarem de alguns milhares de pedidos, vale arquivar os antigos depois de exportar o backup.
