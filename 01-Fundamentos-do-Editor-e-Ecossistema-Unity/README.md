# Etapa 1 - Fundamentos do Editor e Ecossistema Unity

## 1. Conteúdo teórico

### 1.1 Unity Hub e versão do Editor

O Unity Hub é o laucher que gerencia instalações de Editor e projetos. Você não instala "o Unity", você instala uma **versão específica** do Editor via Hub, e cada projeto fica travado numa versão (definida em `ProjectSettings/ProjectVersion.txt`).

Isso importa porque um projeto criado numa versão LTS (Long Term Support) pode não abrir corretamente numa versão diferente, e o Hub vai te avisar disso. Para estudo, use a versõa LTS mais recente disponível, não a Beta/Tech Stream.

**Armadilha:** trocar a versão do Editor de um projeto já em andamento (via Hub) pode migrar automaticamente arquivos de projeto de forma irreversível sem aviso claro. Não faço isso sem entender o que está migrando.

### 1.2 Estrutura de pastas do projeto

Um projeto Unity, na raiz, tem (entre outras) três pastas que importam desde já:

```
MeuProjeto/
├── Assets/          ← tudo que você cria/importa: scripts, scenes, sprites, prefabs
├── Packages/        ← dependências gerenciadas pelo Package Manager (via manifest.json)
├── ProjectSettings/ ← configurações do projeto (versão, input, build settings, etc)
└── Library/         ← cache gerado pelo Editor — NUNCA versiona isso no Git
```

`Assets/` é a única pasta que você edita diretamente na prática do dia a dia. Tudo dentro dela é visível na aba **Project** do Editor, e o caminho física no disco corresponde 1:1 à hierarquia visual do painel.

**Armadilha:** mover ou renomear arquivos dentro de `Assets/` usando o explorador de arquivos do sistema operacional (fora do Editor) quebra referências internas, Unity rastreia arquivos por um `.meta` file com GUID, não por caminho. Sempre move/renomeie *dentro* do painel project.

### 1.3 Scenes

Um **Scene** é um arquivo (`.unity`) que representa um "estado" jogável, pode ser uma fase, um menu, uma tela de loading. Um projeto normalmente tem várias Scenes, mas só um é ativa por vez em Play Mode (a não ser que você carregue cenas aditivas, o que vem na Etapa 9).

Uma Scene contém uma árvore de **GameObjects**, visível na aba **Hierarchy**.

### 1.4 GameObjects e Components

Um **GameObject** é um contêiner vazio por padrão, ele só existe no espaço (tem posição/rotação/escala via `Transform`, que é obrigatório em todo GameObject) e não faz nada até você anexar **Compoenents** a ele.

Um **Components** é um bloco de comportamento ou dado que você anexa a um GameObject: `Rigidbody` dá física, `SpriteRenderer` dá aparência visual, um script seu (que vira um Component quando herda de `MonoBehaviour`) dá lógica customizada.

```
GameObject "Player"
├── Transform          (sempre presente, não pode ser removido)
├── SpriteRenderer      (aparência)
├── Rigidbody2D         (física)
└── PlayerController    (seu script, adicionado como Component)
```

**isso é o mesmo padrão de composição que você já usou implicitamente em Clean Architeture**: Um GameObject não *é* um jogador por herança, ele *tem* não te dá uma classe `Player` que você estende, você monta comportamento anexando peças.

### 1.5 Inspector

A aba **Inspector** mostra os Components do GameObject selecionado na Hierarchy, e permite editar seus campos publicamente expostos (posição valores de script, referências a outras objetos) **sem recompilar código**.

**Armadilha crítica, o que mais gera erro silencioso:** valores editados no Inspector durante o Play Mode **Não persistem** quando você sai do Play, Unity restaura o estado salvo do projeto. Valores editados no Inspector **fora** do Play Mode persistem normalmente (são salvos na Scene). Se você "ajustar" um valor em runtime pra testar e sair satisfeito, e depois entrar em Play de novo e o valor "voltou", não é bug, é o comportamento esperado, e é a armadilha #1 de quem começa em Unity.

### 1.6 Project, Hierarchy, Console

- **Project**: todos os assets do projeto (arquivos em disco, dentro de `Assets/`).
- **Hierarchy**: os GameObjects da Scene atualmente aberta (estrutura em memória/runtime daquela cena).
- **Console**: onde aparecem erros de compilação, warnings, e qualquer `Debug.Log` que você escrever no código.

Um erro comum de quem confunde os dois primeiros: arrastar um item do project pra dentro da Hierarchy **instancia** aquele asset como GameObject na cena (se for um Prefab ou modelo), não é o mesmo objeto "linkado", é uma cópia posicionada na cena.

### 1.7 Ciclo Editor vs Play Mode

Existem três "modos": Edit Mode (default, editando a Scene), Play Mode (o jogo está executando dentro do Editor) e Pause (Play Mode congelado, pra inspecionar estado frame a frame).

Entrar em Play Mode não é "rodar o jogo" no sentido de processo separado, é o próprio Editor executando a lógica em cima do estado atual da Scene, com a diferença de que qualquer mudança de estado feita ali é descartada ao sair (ver 1.5).

## 2. Checklist antes de ir pros exercícios

Se qualquer resposta for "não tenho certeza", relê só a seção específica, não o documento inteiro.

1. Eu sei explicar por que mover um arquivo pelo explorador do Windows (fora do Editor) pode quebrar uma referência, mesmo que o arquivo continue "no mesmo lugar" visualmente no Project?
2. Eu sei dizer a diferença entre "editar um valor no Inspector em Play Mode" e "editar o mesmo valor em Edit Mode", em termos do que persiste?
3. Eu sei explicar por que um GameObject sem nenhum script customizado ainda tem pelo menos um Component?
4. Eu sei dizer por que arrastar um asset do Project pra Hierarchy não é "referenciar", e sim "instanciar"?
5. Eu sei nomear qual pasta do projeto eu NUNCA deveria versionar no Git, e por quê?

## 3. Exercícios

1. Crie um novo projeto Unity (template 3D ou 2D, sua escolha, isso não tem impacto nessa etapa). Abra a Scene padrão. Na Hierarchy, crie um GameObject vazio via `GameObject > Create Empty`, renomeie-o para `Sandbox`. No Inspector, confirme que ele já tem um Transform e nada mais.

2. Adicione um segundo GameObject (um Cube, via `GameObject > 3D Object > Cube` ou equivalente 2D com um Sprite). Entre em Play Mode, mude a posição dele arrastando no Inspector ou na Scene view. Saia do Play Mode. Documente (por escrito, no seu README de resposta) o que aconteceu com a posição e por quê, sem eu confirmar antes se está certo.

3. Repita o exercício 2, mas agora mude a posição **fora** do Play Mode (Edit Mode) e não entre em Play depois. Confirme se a mudança persistiu ao salvar a Scene (`Ctrl+S`) e reabrir o projeto.

4. Na aba Project, dentro de `Assets`, crie uma subpasta chamada `Scripts`. Depois, usando o explorador de arquivos do Windows (fora do Unity), renomeie essa pasta para `Scripts_v2`. Volte ao Unity e observe o Console. Documente o que aconteceu (erro, warning, ou nada) e por quê, isso é sobre `.meta` files, mesmo que você não tenha lido a explicação técnica completa deles ainda.
