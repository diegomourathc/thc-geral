# 🎉 Aniversário do Kalel — App de Confirmação de Presença

Mini-app de RSVP (confirmação de presença) para o aniversário do Kalel, na Argeus Pizzaria em Gravataí, dia 28/08.

Cada convidado digita o nome (ou nome da família) e a quantidade de pessoas — nada de lista fixa no código, então dá pra confirmar gente de última hora sem precisar mexer no site.

## Como configurar (leva ~5 minutos)

### 1. Crie um projeto no Firebase

1. Acesse [console.firebase.google.com](https://console.firebase.google.com) e clique em **Adicionar projeto**.
2. Dê um nome (ex: `aniversario-kalel`) e conclua a criação (pode desativar o Google Analytics, não é necessário).
3. No menu lateral, vá em **Firestore Database** → **Criar banco de dados** → escolha um local (ex: `southamerica-east1`) → inicie em **modo de teste**.

### 2. Libere a escrita/leitura no Firestore

Como o evento é em poucos dias, libere o acesso temporariamente. Em **Firestore Database → Regras**, cole:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

⚠️ Isso deixa o banco aberto para qualquer pessoa com o link. É aceitável para um evento pontual e de curta duração, mas **não deixe assim depois da festa** — depois volte para regras restritas ou apague o projeto.

### 3. Gere a configuração do App Web

1. No painel do projeto, clique no ícone de engrenagem → **Configurações do projeto**.
2. Em **Seus apps**, clique no ícone `</>` (Web) e registre um app (ex: `kalel-rsvp`).
3. Copie o objeto `firebaseConfig` que aparece.
4. Abra `index.html` neste repositório e substitua o objeto `firebaseConfig` (procure por `SUA_API_KEY`) pelos valores copiados.

### 4. Publique com GitHub Pages

1. Faça commit e push das alterações no `index.html`.
2. No GitHub, vá em **Settings → Pages**.
3. Em **Branch**, escolha a branch onde está o `index.html` (ex: `main`) e a pasta `/ (root)`.
4. Salve. Em ~1 minuto o link estará disponível (algo como `https://SEU_USUARIO.github.io/thc-geral/`).
5. Compartilhe esse link com os convidados.

## Acompanhando as confirmações

- O próprio site já mostra, ao clicar em **"Ver quem já confirmou"**, a lista de nomes e o total de pessoas confirmadas em tempo real.
- Você também pode abrir o painel do Firestore no Firebase (**Firestore Database → Dados**) e ver a coleção `confirmacoes_kalel` com todos os registros.

## Detalhes do evento (editáveis no `index.html`)

- **Data:** 28/08 (sexta-feira)
- **Horário:** 20:00
- **Local:** Argeus Pizzaria — Gravataí
- **Prazo para confirmar:** até 26/08
