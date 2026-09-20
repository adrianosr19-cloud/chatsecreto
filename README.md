# Chat Secreto

Calculadora que esconde um chat em tempo real (Firebase Realtime Database).

## Como usar

1. Digite `1234` e toque em `=` para sair da calculadora.
2. Digite a senha da sala. Cada senha corresponde a uma sala diferente; na primeira vez o site pergunta se deseja criar a sala.
3. Escolha um nome e converse.

## Configurar as regras do Firebase (obrigatorio)

Sem estas regras, qualquer pessoa com o link consegue ler todas as mensagens.

1. Abra o [console do Firebase](https://console.firebase.google.com/), projeto `meuchatsecreto-ec2e9`.
2. Menu **Realtime Database** > aba **Regras**.
3. Substitua todo o conteudo pelo arquivo [`firebase-rules.json`](firebase-rules.json) e clique em **Publicar**.

Com as regras publicadas:

- A raiz do banco nao pode ser lida nem listada, entao ninguem descobre quais salas existem.
- A sala so pode ser acessada por quem conhece a senha (o caminho da sala e o SHA-256 da senha).
- Mensagens nao podem ser editadas nem apagadas pelo site, e precisam ter texto (ate 500 caracteres), nome (ate 20) e horario.
- O no antigo `secret_chat_messages` fica inacessivel; pode ser apagado no console.

## Publicar

Arquivo unico e estatico (`index.html`). Funciona no GitHub Pages, Netlify ou Vercel. Precisa ser servido por HTTPS (ou `localhost`) porque a senha usa `crypto.subtle`.
