# Cronograma de estudo - Unity

## Objetivo

Documentar a jornada de aprendizado de desenvolvimento de jogos com Unity, registrando conceitos estudados, exercícios resolvidos e evolução técnica ao longo do processo. Serve como registro versionado no GitHub e como prova de consolidação real, não de exposição passiva ao conteúdo.

Regras do método
Nenhuma etapa termina só com exercício green-field — a partir da Etapa 3, todo bloco de conteúdo ganha pelo menos 1 exercício de debug (código já pronto e quebrado de propósito).
Checkpoints de consolidação a cada 3 etapas — volto num exercício antigo e uso com o conteúdo novo. Etapa sem checkpoint feito não conta como concluída.
Testes automatizados (Unity Test Framework) entram a partir da Etapa 9 e ficam sendo hábito contínuo dali em diante, não tópico isolado no fim.
Leitura de código real (repositório open source de jogo/projeto Unity) entra a partir do Checkpoint 4 (pós-Etapa 12) em diante.
Critério de avanço: não é "li o conteúdo", é "consigo explicar pra alguém leigo E cometo menos erros óbvios quando aplico por conta própria".
Estrutura

## Etapa 1 - Fundamentos do Editor e Ecossistema Unity

Conceitos: Unity Hub, estrutura de projeto (Assets/Scenes/Packages), Scenes, GameObjects, Components, Inspector, Project/Hierarchy/Console windows, ciclo Editor vs Play Mode.
Exercícios: green-field.

## Etapa 2 - Scripting com MonoBehaviour

Conceitos: ciclo de vida (Awake, OnEnable, Start, Update, FixedUpdate, OnDisable, OnDestroy), [SerializeField] vs public, referências configuradas no Inspector, GetComponent/GetComponentInChildren.
Exercícios: green-field.

## Etapa 3 - Transform e Movimento

Conceitos: Transform (position, rotation, scale), Vector3/Quaternion básico, Time.deltaTime, Translate vs manipulação direta de position, espaço local vs world.
Exercícios: green-field + [DEBUG].

Checkpoint 1 (obrigatório antes de seguir pra Etapa 4)

Revisitar o exercício de movimento da Etapa 3, mas agora reescrever usando referências e ciclo de vida corretos da Etapa 2 (nada de Find custoso em Update, nada de lógica de movimento fora do método certo do ciclo de vida).

## Etapa 4 - Input System

Conceitos: Input Manager legado vs Input System novo (pacote), InputAction, PlayerInput, polling vs abordagem orientada a evento, Axis/Button.
Exercícios: green-field + [DEBUG].

## Etapa 5 - Física (Rigidbody e Colliders)

Conceitos: Rigidbody/Rigidbody2D, Colliders vs Triggers, OnCollisionEnter/OnTriggerEnter e variantes, por que física fica em FixedUpdate.
Exercícios: green-field + [DEBUG].

## Etapa 6 - Prefabs e Instanciação

Conceitos: Prefabs, Prefab Variants, prefabs aninhados, Instantiate/Destroy, introdução a object pooling (motivação, não implementação completa ainda).
Exercícios: green-field + [DEBUG].

Checkpoint 2 (obrigatório antes de seguir pra Etapa 7)

Revisitar o exercício de física da Etapa 5, convertendo os objetos envolvidos em Prefabs e instanciando-os dinamicamente em runtime, mantendo o comportamento de colisão correto.

## Etapa 7 - ScriptableObjects e Arquitetura de Dados

Conceitos: ScriptableObject, separação entre dados e comportamento, event channels implementados via SO.
Exercícios: green-field + [DEBUG].

## Etapa 8 - UI com UGUI (Canvas)

Conceitos: Canvas (Screen Space vs World Space), RectTransform, anchors/pivots, Button/Text/Image, EventSystem.
Exercícios: green-field + [DEBUG].

## Etapa 9 - Gerenciamento de Cena e Testes Automatizados

Conceitos: SceneManager, cenas aditivas, persistência de dados entre cenas (Singleton vs SO — discussão crítica de trade-offs, não "Singleton sempre"), introdução ao Unity Test Framework (EditMode vs PlayMode tests).
Exercícios: green-field + [DEBUG] + [TESTE].

Checkpoint 3 (obrigatório antes de seguir pra Etapa 10)

Revisitar o exercício de UI da Etapa 8, movendo o estado que ele controla para persistir entre duas cenas, e escrever um teste automatizado que valide esse estado após a troca de cena.

## Etapa 10 - Animação

Conceitos: Animator Controller, Animation Clips, states e transitions, parâmetros do Animator, Animation Events.
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 11 - Áudio

Conceitos: AudioSource/AudioClip, AudioMixer, som 3D (spatial blend), pooling de AudioSources para SFX repetitivo.
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 12 - Sistema de Eventos e Desacoplamento

Conceitos: UnityEvent vs Action/delegate C# puro, padrão Observer aplicado a Unity, event bus centralizado, quando desacoplar é necessário vs over-engineering.
Exercícios: green-field + [DEBUG] + [TESTE].

Checkpoint 4 (obrigatório antes de seguir pra Etapa 13)

Revisitar o event channel da Etapa 7 e o sistema de UI da Etapa 8: substituir qualquer acoplamento direto restante por um dos padrões de eventos da Etapa 12. Além disso: ler o código-fonte de um projeto Unity open source real (ex: repositório de um jogo pequeno no GitHub) e identificar qual padrão de desacoplamento ele usa.

## Etapa 13 - Coroutines e Assincronia

Conceitos: IEnumerator/yield return, WaitForSeconds vs WaitForFixedUpdate vs WaitForEndOfFrame, Coroutines vs async/await em Unity, cancelamento de coroutine.
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 14 - Padrões de Arquitetura em Unity

Conceitos: State Machine para gameplay (ex: máquina de estados de personagem), Service Locator vs injeção de dependência leve, por que Singleton abusivo quebra testabilidade.
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 15 - Save/Load e Persistência

Conceitos: serialização JSON (JsonUtility e alternativas), PlayerPrefs e suas limitações reais, escrita/leitura de arquivo, versionamento de save (migração quando o formato muda).
Exercícios: green-field + [DEBUG] + [TESTE].

Checkpoint 5 (obrigatório antes de seguir pra Etapa 16)

Revisitar o estado persistido entre cenas da Etapa 9 e torná-lo persistente entre sessões (save em arquivo), com teste automatizado cobrindo o caso de save corrompido ou ausente.

## Etapa 16 - 2D: Sprites e Tilemaps

Conceitos: Sprite Renderer, Sorting Layers e Order in Layer, Tilemap, Colliders 2D compostos, pixel-perfect (Pixel Perfect Camera).
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 17 - 3D: Câmeras e Navegação

Conceitos: Cinemachine (follow, framing), NavMesh/NavMeshAgent, pathfinding básico, bake de NavMesh.
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 18 - Performance e Profiling

Conceitos: Unity Profiler (CPU/GPU/Memory), Garbage Collector e alocações em Update, object pooling implementado de fato (retomando a motivação da Etapa 6), draw calls e batching básico.
Exercícios: green-field + [DEBUG] + [TESTE].

Checkpoint 6 (obrigatório antes de seguir pra Etapa 19)

Rodar o Profiler no projeto acumulado até aqui, identificar pelo menos uma alocação desnecessária em Update e corrigi-la com pooling. Ler o código-fonte de um segundo projeto open source, focando em como ele lida com performance (pooling, caching de referência).

## Etapa 19 - Build e Deploy

Conceitos: Build Settings, Player Settings por plataforma, Addressables (introdução conceitual), pipeline de build básico.
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 20 - Networking (Introdução)

Conceitos: visão conceitual client-server vs peer-to-peer, Netcode for GameObjects (introdução), sincronização de estado — o que sincronizar e o que não sincronizar.
Exercícios: green-field + [DEBUG] + [TESTE].

## Etapa 21 - Workflow de Versionamento em Equipe

Conceitos: .gitignore específico pra Unity, Git LFS, conflitos em cenas/prefabs (formato YAML), Smart Merge do Unity.
Exercícios: green-field + [DEBUG] + [TESTE].

🔁 Checkpoint 7 (obrigatório antes de seguir pra Etapa 22)

Simular um conflito de merge real em uma cena ou prefab (duas branches editando o mesmo objeto) e resolvê-lo, documentando o processo.

## Etapa 22 - Projeto Consolidado

Critério de conclusão - não é "features implementadas":

Jogo completo e jogável (mesmo que pequeno em escopo) usando pelo menos: scripting, física ou input customizado, UI, gerenciamento de cena, save/load, e pelo menos um sistema de arquitetura desacoplada (event bus ou SO).
Testes automatizados cobrindo a lógica de gameplay não-trivial (não apenas getters/setters).
Capacidade de explicar cada decisão de arquitetura sem consultar o código (por que Singleton aqui e não lá, por que Coroutine e não async, etc).
Resiliência: alguém de fora tenta ativamente quebrar o jogo (input absurdo, sequência de ações fora de ordem, save corrompido) e o projeto não crasha silenciosamente.
