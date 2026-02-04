# Karvex

Aplicativo móvel universal (Expo + React Native) para gerenciamento de fretes e informações de motoristas/empresas.

**Tecnologias principais:** `Expo`, `React Native`, `Firebase` (Auth, Firestore, Storage), `expo-router`.

**Status:** Desenvolvimento

**Observação rápida:** este `README` descreve como configurar o projeto localmente, rodar em simuladores/dispositivos e como publicar regras do Firestore.

**Descrição**
- **Projeto:** app para gerenciamento de fretes (dashboard, histórico, notificações, perfil, upload de documentos e imagens).

**Pré-requisitos**
- **Node:** versão compatível com `Expo SDK 54` (Node 16+ recomendado; Node 18+ funciona bem).
- **npm** ou **Yarn**.
- **Expo CLI / EAS CLI:** recomendado para builds nativos e publicação.
- **Firebase CLI:** necessário apenas para deploy das regras do Firestore (`deploy:firestore`).

Instale ferramentas essenciais (exemplo):

```bash
npm install -g expo-cli eas-cli firebase-tools
```

**Instalação (local)**

1. Clone o repositório:

```bash
git clone <repo-url>
cd Karvex
```

2. Instale dependências:

```bash
npm install
# ou
# yarn install
```

3. Crie um arquivo de variáveis de ambiente a partir de um exemplo (recomendado):

```bash
cp .env.example .env
```

Preencha as variáveis no `.env` conforme descrito na seção "Configuração do Firebase" abaixo.

**Configuração do Firebase**

O projeto contém `src/firebaseConfig.ts` com a configuração do Firebase atualmente no repositório. Recomenda-se migrar essas chaves para variáveis de ambiente (ou `app.json` → `extra`) para não ter credenciais expostas no controle de versão.

Crie um arquivo `.env` (ou use `app.json` → `extra`) com as seguintes variáveis (exemplo em `.env.example`):

```env
FIREBASE_API_KEY=
FIREBASE_AUTH_DOMAIN=
FIREBASE_PROJECT_ID=
FIREBASE_STORAGE_BUCKET=
FIREBASE_MESSAGING_SENDER_ID=
FIREBASE_APP_ID=
```

Observações:
- Se preferir usar `app.json` `extra`, siga o padrão do Expo e leia os valores com `expo-constants` em `src/firebaseConfig.ts`.
- Se estas chaves já estiverem publicadas, considere rotacioná-las nas configurações do Firebase.

**Rodando o app (desenvolvimento)**

Inicie o Metro/Expo:

```bash
npm start
# ou
npx expo start
```

Com o servidor rodando você pode abrir:
- Android: `npm run android` (requer Android Studio / emulador ou dispositivo).
- iOS: `npm run ios` (macOS + Xcode) ou usar um dispositivo físico via Expo Dev Client.
- Web: `npm run web`.

**Scripts importantes**
- `start`: inicia o servidor Expo.
- `android`: executa `expo run:android`.
- `ios`: executa `expo run:ios`.
- `web`: executa `expo start --web`.
- `lint`: executa `expo lint`.
- `deploy:firestore`: `firebase deploy --only firestore:rules` (necessário `firebase-tools` e estar logado).
- `reset-project`: referência a `node ./scripts/reset-project.js` — verifique se `scripts/reset-project.js` existe (no repositório atual este arquivo não foi encontrado e o comando falhará).

**Deploy das regras do Firestore**

1. Instale o `firebase-tools` (global ou devDependency):

```bash
npm install -g firebase-tools
```

2. Logue e selecione projeto:

```bash
firebase login
firebase use --add
```

3. Rode o deploy das regras (conforme `package.json`):

```bash
npm run deploy:firestore
```

**Boas práticas de segurança**
- Não comite arquivos com credenciais (`.env`) — `.gitignore` já inclui `env`.
- Mova a configuração sensível para variáveis de ambiente, `app.json` `extra` ou use os Secrets do EAS para builds.

**Observações/Issues conhecidas**
- `src/firebaseConfig.ts` contém configurações do Firebase em claro dentro do repositório. Recomendo adaptar para leitura de variáveis de ambiente e remover valores sensíveis do controle de versão.
- `package.json` referencia `scripts/reset-project.js` que não foi encontrado — criar o arquivo ou remover/ajustar o script.

**Contribuição**
- Para contribuir, abra uma issue descrevendo a melhoria ou correção e envie um Pull Request com testes quando aplicável.

**Contato**
- Para dúvidas ou colaboração, contate o mantenedor do repositório.

**Licença**
- Verifique o arquivo `LICENSE` no repositório ou adicione uma licença adequada (ex: MIT).

---

Se quiser, posso:
- Criar um `.env.example` com as variáveis acima.
- Modificar `src/firebaseConfig.ts` para ler das variáveis de ambiente / `expo-constants`.
- Criar o arquivo `scripts/reset-project.js` (se você confirmar o comportamento esperado).

Quer que eu crie algum desses arquivos agora? 
