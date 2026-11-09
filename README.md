# Car Doce Car - Agendamentos

App de agendamentos da Car Doce Car em React (Vite) com **Firebase** (Firestore + Authentication).
Permite **adicionar**, **editar**, **excluir**, **favoritar** e **filtrar favoritos**, com os dados
**sincronizados em tempo real** entre celulares e computadores.

## 1. Configurar o Firebase (uma vez só)

1. Em https://console.firebase.google.com, crie um projeto.
2. Na página inicial do projeto, clique em **Web `</>`**, registre o app e copie o `firebaseConfig`.
3. **Criação > Firestore Database > Criar banco de dados** (região `southamerica-east1`, modo de produção).
4. **Criação > Authentication > Primeiros passos > E-mail/senha**: ativar.
5. Em Authentication > **Usuários > Adicionar usuário**: crie seu e-mail e senha (é o login do app).
6. Em Firestore > **Regras**: cole o conteúdo de `firestore.rules` e publique.

## 2. Configurar o projeto

Requisito: [Node.js](https://nodejs.org) 18 ou superior.

```bash
npm install
cp .env.example .env     # no Windows: copy .env.example .env
```

Abra o `.env` e preencha com os valores do `firebaseConfig`. Depois:

```bash
npm run dev
```

Abra http://localhost:3000 e entre com o e-mail e a senha criados no passo 1.5.

## 3. Publicar para usar no celular (Firebase Hosting)

```bash
npm install -g firebase-tools
firebase login
firebase use --add        # escolha o seu projeto
npm run build
firebase deploy
```

O Firebase mostra o link final (`https://SEU-PROJETO.web.app`). No iPhone, abra no Safari e use
**Compartilhar > Adicionar à Tela de Início**. Entre com o mesmo e-mail e senha em todos os aparelhos.

Se publicar em outro serviço (Netlify, Vercel...), cadastre as variáveis `VITE_FIREBASE_*` no painel dele
e adicione o domínio em Authentication > Configurações > **Domínios autorizados**.

## Estrutura

- `src/firebase.js` – inicialização do Firebase (Auth + Firestore com cache offline).
- `src/services/appointments.js` – salvar, listar em tempo real, editar e excluir.
- `src/components/Login` – tela de login.
- `src/components/Appointments` – formulário, filtro e lista.
- `src/components/AppointmentItem` – cartão de cada agendamento, com edição inline e exportação para agenda.
- `firestore.rules` / `firebase.json` – regras de segurança e configuração de deploy.

## Se o `npm install` falhar

1. Confira `node -v` (precisa ser 18+).
2. Apague `node_modules` e `package-lock.json` e rode `npm install` de novo.
3. Limpe o cache: `npm cache clean --force`.
4. Em rede com proxy, configure o proxy do npm ou tente outra rede.
