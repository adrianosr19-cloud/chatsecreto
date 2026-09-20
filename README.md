# Chat Secreto

Calculadora que esconde um chat em tempo real (Firebase Realtime Database).

## Como usar

### Quem participa do chat

1. Digite `1234` e toque em `=` para sair da calculadora.
2. Digite a senha da sala que o admin enviou.
3. Escolha um nome e converse.

Nao ha nenhuma dica na tela: so entra quem conhece o codigo e a senha.

### Admin (painel de controle)

1. Digite `4321` e toque em `=` para abrir o painel do admin.
2. Na primeira vez, a senha digitada vira a senha do admin (minimo 6 caracteres). Guarde-a: nao ha recuperacao e so existe um admin.
3. No painel voce cria salas (nome + senha, ou botao **Gerar**), ve/copia as senhas e apaga salas com todas as mensagens.

Somente o admin cria salas. Quem digitar uma senha que nao existe ve "Senha incorreta".

## Configurar as regras do Firebase (obrigatorio)

Sem estas regras, qualquer pessoa com o link consegue ler todas as mensagens e criar salas.

1. Abra o [console do Firebase](https://console.firebase.google.com/), projeto `meuchatsecreto-ec2e9`.
2. Menu **Realtime Database** > aba **Regras**.
3. Substitua todo o conteudo pelo arquivo [`firebase-rules.json`](firebase-rules.json) e clique em **Publicar**.
4. Abra o site, digite `4321` `=` e defina a senha do admin logo em seguida (a primeira senha cadastrada vira a do admin).

Com as regras publicadas:

- A raiz do banco nao pode ser lida nem listada, entao ninguem descobre quais salas existem.
- A sala so pode ser acessada por quem conhece a senha (o caminho da sala e o SHA-256 da senha).
- Somente o admin cria e apaga salas; a lista de salas e senhas fica em `admin_rooms/<chave do admin>`, legivel apenas com a chave.
- Mensagens nao podem ser editadas nem apagadas pelo site, e precisam ter texto (ate 500 caracteres), nome (ate 20) e horario.
- Salas antigas criadas antes desta versao (sem `info`) ficam inacessiveis; apague-as no console ou recrie pelo painel.

Para trocar a senha do admin, apague o no `admins` no console e defina a nova senha pelo painel.

## Publicar

Arquivo unico e estatico (`index.html`). Funciona no GitHub Pages, Netlify ou Vercel. Precisa ser servido por HTTPS (ou `localhost`) porque a senha usa `crypto.subtle`.
