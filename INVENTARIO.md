# Inventário de skills e plugins para Claude Code

Data da varredura: 2026-11-21. Scanner: SkillSpector v2.12.0, modo heurístico (`--no-llm`), `timeout 600`.

## Como ler

- **Varredura (URL):** `skillspector scan https://github.com/<repo> --no-llm` sobre o repositório inteiro.
- **Varredura (unidade):** quando a varredura da URL falhou (orçamento de bytes ou tempo), repeti a varredura só sobre o que seria instalado. Para um plugin com fonte `./`, a unidade é `.claude-plugin/`, `skills/`, `commands/`, `agents/`, `hooks/` e `.mcp.json`. Para uma skill solta, é a pasta da skill.
- **Regra de instalação:** só entra item com MEDIUM ou melhor, licença livre para uso comercial e código das skills e scripts executáveis lido.
- **Status:** `instalado`, `pendente` (pode entrar depois de nova varredura ou decisão) ou `excluído`.

## Instalados

| Item | Fonte | Licença | Varredura | Como foi instalado | Commit revisado |
|---|---|---|---|---|---|
| humanizer | [blader/humanizer](https://github.com/blader/humanizer) | MIT | URL: MEDIUM 49/100, CAUTION | Plugin: marketplace `humanizer`, plugin `humanizer@humanizer` em `.claude/settings.json` | `a32f244` |
| explainer-studio | [reedodev/explainer-studio](https://github.com/reedodev/explainer-studio) | MIT | URL: byte_budget_exhausted. Unidade: LOW 17/100, SAFE | Plugin: marketplace `explainer-studio`, plugin `explainer-studio@explainer-studio` em `.claude/settings.json` | `05fdbab` |
| motion-kit (skill `motion-designer`) | [hughminhphan/motion-kit](https://github.com/hughminhphan/motion-kit) | MIT (LICENSE copiada junto) | URL: MEDIUM 28/100, CAUTION | Skill solta: `.claude/skills/motion-designer/` | `6173e5c` |

Notas da revisão manual:

- **humanizer:** só Markdown (`SKILL.md`, 504 linhas). Sem hooks, sem MCP, sem scripts carregados pelo plugin (`scripts/validate-package.py` só roda na CI do autor). Os dois achados HIGH "AR2 Anti-Refusal" (SKILL.md:208 e :211) são falso positivo: são regras de estilo sobre travessões e qualificadores.
- **explainer-studio:** a skill só traz instruções. Quem roda é o motor do repositório (`src/`, TypeScript), via `npm ci` e `npm run es`, sempre a pedido do usuário. Li os pontos de risco: `.npmrc` com `ignore-scripts=true`. As dependências vêm só do registro npm. Os processos são `ffmpeg`/`ffprobe` com argumentos em lista e o provedor TTS `cmd`, opcional, que só roda com `WV_TTS_CMD` definido e usa escape POSIX correto. A rede só é usada pelo TTS `edge`, opcional, que envia o texto da narração a um endpoint não oficial da Microsoft. A escrita é feita só em `output/` e em arquivos temporários. Requer Node 20+ e FFmpeg.
- **motion-kit:** `motion-kit.js` é uma biblioteca GSAP para o navegador, copiada para dentro das composições. Sem rede, `eval`, cookies, `localStorage` ou APIs de Node. Os 5 achados MEDIUM estão no README (instruções de symlink e `npx hyperframes` sem versão) e em um falso positivo dentro de um `.mp4`. Atenção: existem vários repositórios chamados "motion-kit". Escolhi o de hughminhphan porque é feito para HyperFrames e a nota (MEDIUM 28/100) confere com a varredura anterior.

## Todos os itens

| # | Item | Fonte | Licença | Varredura | Status | Motivo |
|---|---|---|---|---|---|---|
| **Design** | | | | | | |
| 1 | impeccable | pbakaus/impeccable | Apache-2.0 | URL: byte_budget_exhausted (2ª vez). Unidade `plugin/`: CRITICAL 100/100, DO NOT INSTALL | excluído | CRITICAL. Era o par exclusivo com UI/UX Pro Max e nenhum dos dois passou. |
| 2 | ui-ux-pro-max-skill | nextlevelbuilder/ui-ux-pro-max-skill | MIT | URL: timeout (2ª vez). Unidade: timeout | pendente | Varredura incompleta. Não instalar até completar. Traz `stack/.mcp.json`. |
| 3 | taste-skill | Leonxlnx/taste-skill | MIT | URL: byte_budget_exhausted. Unidade: timeout | pendente | Varredura incompleta. |
| 4 | agent-skills (Vercel) | vercel-labs/agent-skills | MIT (README e frontmatter; sem LICENSE na raiz) | URL: timeout. Unidade `skills/`: CRITICAL 100/100 | excluído | CRITICAL. |
| 5 | awesome-design-md | VoltAgent/awesome-design-md | MIT | URL: timeout | pendente | Coleção de arquivos DESIGN.md, sem SKILL.md nem plugin. Usar como referência caso a caso. |
| 6 | playwright-cli | microsoft/playwright-cli | Apache-2.0 | URL: HIGH 80/100, DO NOT INSTALL | excluído | HIGH. |
| 7 | diagram-design | cathrynlavery/diagram-design | MIT | URL: CRITICAL 100/100 | excluído | CRITICAL. |
| 8 | Ponytail | DietrichGebert/ponytail | não verificada | CRITICAL, DO NOT INSTALL (varredura anterior; achado principal em `benchmarks/agentic/judge.py`) | excluído | CRITICAL. Só reavaliar após revisão manual do código. |
| **Vídeo e animação** | | | | | | |
| 9 | vox-director | Alisa0808/vox-director | MIT | URL: CRITICAL 100/100 | excluído | CRITICAL. Exige `ATLASCLOUD_API_KEY`. |
| 10 | paint-mv-skills | lintsinghua/paint-mv-skills | MIT no repositório; motor PDoomVideo sem licença | URL: HIGH 70/100 | excluído | HIGH. A premissa "sem licença" vale só para o motor PDoomVideo; as skills têm LICENSE MIT. |
| 11 | explainer-studio | reedodev/explainer-studio | MIT | Unidade: LOW 17/100, SAFE | **instalado** | Ver notas acima. |
| 12 | anything2explainer | Vincentwei1021/anything2explainer | licença própria, só uso não comercial | URL: CRITICAL 100/100 | excluído | CRITICAL e não comercial. |
| 13 | bang-motion | bangtutorial/bang-motion | MIT | URL: HIGH 54/100 | excluído | HIGH. |
| 14 | claude-remotion-skill | haidrrrry/claude-remotion-skill | MIT | URL: HIGH 57/100 | excluído | HIGH. |
| 15 | video-shotcraft | Vincentwei1021/video-shotcraft | Apache-2.0 | URL: byte_budget_exhausted. Repositório local: timeout | pendente | Varredura incompleta. |
| 16 | cinetic | Leonxlnx/cinetic | MIT | URL: timeout. Unidade: timeout | pendente | Varredura incompleta. |
| 17 | hyperframes | heygen-com/hyperframes | Apache-2.0 | URL: byte_budget_exhausted. Unidade: CRITICAL 100/100 | excluído | CRITICAL. |
| 18 | anatomy | wheresryan22/anatomy | MIT | URL: timeout. Repositório local: timeout | pendente | Varredura incompleta. |
| 19 | motion-kit | hughminhphan/motion-kit | MIT | URL: MEDIUM 28/100, CAUTION | **instalado** | Código lido. Ver notas acima. |
| 20 | lemo-opuscar | [lemomo-ai/lemo-opuscar](https://github.com/lemomo-ai/lemo-opuscar) (confirmada por busca) | código MIT; prompts e docs CC BY-NC 4.0 | não varrido | excluído | Fora por decisão do usuário. Os prompts de estilo são não comerciais. |
| **Produtividade e memória** | | | | | | |
| 21 | humanizer | blader/humanizer | MIT | URL: MEDIUM 49/100, CAUTION | **instalado** | Ver notas acima. |
| 22 | last30days-skill | mvanhorn/last30days-skill | MIT | URL: byte_budget_exhausted (2ª vez). Unidade: CRITICAL 100/100 | excluído | CRITICAL. |
| 23 | Scrapling | D4Vinci/Scrapling | BSD-3-Clause | URL: timeout. Unidade `agent-skill/Scrapling-Skill`: HIGH 54/100 | excluído | HIGH. |
| 24 | caveman | JuliusBrussee/caveman | Apache-2.0 | URL: timeout. Unidade: CRITICAL 100/100 | excluído | CRITICAL. |
| 25 | superpowers | obra/superpowers | MIT | URL: CRITICAL 100/100 (parcial) | excluído | CRITICAL. Traz `hooks/hooks.json`. |
| 26 | claude-mem | thedotmack/claude-mem | Apache-2.0 | URL: byte_budget_exhausted. Unidade `plugin/`: timeout | pendente | Varredura incompleta. O plugin traz `hooks/hooks.json` e `.mcp.json`: conferir conflito com a regra de não criar hook de sessão. |
| 27 | oh-my-claudecode | Yeachan-Heo/oh-my-claudecode | MIT | URL: timeout. Unidade: CRITICAL 100/100 | excluído | CRITICAL. |
| 28 | career-ops | career-ops-hq/career-ops | MIT | URL: byte_budget_exhausted. Unidade (só `.claude-plugin`, `hooks`): LOW 9/100 | excluído | O plugin registra um hook `SessionStart` que roda `node` e instala pacotes npm a cada sessão. Isso conflita com a regra de não criar hook de sessão, e as skills em `.agents/skills/` não foram varridas. Usa Apify. |
| 29 | scroll-craft | nateherkai/scroll-craft | MIT | URL: CRITICAL 91/100 | excluído | CRITICAL. |
| 30 | Pake | tw93/Pake | GPL-3.0 | URL: timeout | instalado (ambiente do usuário), incompleto | `pake-cli` 3.20.0 via npm. Para gerar apps faltam Rust e bibliotecas do sistema (WebKitGTK), que exigem `sudo apt`. |
| 31 | Understand-Anything | Egonex-AI/Understand-Anything | MIT | URL: CRITICAL 100/100 | excluído | CRITICAL. |
| 32 | i-have-adhd | ayghri/i-have-adhd | MIT | URL: CRITICAL 100/100 | excluído | CRITICAL. |
| 33 | pstack | backnotprop/pstack | MIT | URL: CRITICAL 100/100 | excluído | CRITICAL. |
| 34 | linkedin-skills | sergebulaev/linkedin-skills | MIT | URL: CRITICAL 100/100 | excluído | CRITICAL. Usa Apify e Publora. |
| **Custo e ferramentas** | | | | | | |
| 35 | rtk | rtk-ai/rtk | Apache-2.0 | URL: timeout | instalado (ambiente do usuário) | Já estava instalado: `rtk` 1.2.1 em `~/.local/bin`. |
| 36 | ccusage | ryoppippi/ccusage | MIT | URL: timeout | instalado (ambiente do usuário) | `ccusage` 20.0.51 via npm. Pronto para uso. |
| 37 | OmniRoute | diegosouzapw/OmniRoute | MIT | URL: byte_budget_exhausted | instalado (ambiente do usuário), sem configurar | `omniroute` 3.8.54 via npm. `postinstall` lido; npm 11 não executou scripts de instalação, mas o better-sqlite3 carrega. Precisa de chaves de provedores para rotear. |
| 38 | claude-code-router | musistudio/claude-code-router | MIT | URL: byte_budget_exhausted | instalado (ambiente do usuário), sem configurar | `ccr` 3.1.6 via npm. Responde "No available models": precisa de um provedor com chave. |
| 39 | freellmapi | tashfeenahmed/freellmapi | MIT | URL: timeout | parcial | Cliente `freellmapi` 0.8.2 via npm (configuração de agentes e chaves). O servidor exige Docker, ausente. O instalador oficial é `curl … \| bash` e não foi executado. Aviso: o pacote pede Node < 25 (instalado: 26). |
| 40 | Agent-Reach | Panniantong/Agent-Reach | MIT | URL: CRITICAL 100/100 | excluído | CRITICAL. |
| 41 | markitdown | microsoft/markitdown | MIT | URL: timeout | instalado (ambiente do usuário) | `markitdown[all]` 0.1.9 via `uv tool install`. Pronto para uso. |
| 42 | SkillSpector | NVIDIA/SkillSpector | BSD-3-Clause | não se aplica | ferramenta | Usado só como scanner. Instalado em `~/.local/bin` com `uv tool install`, fora deste repositório. |
| **Fora por decisão** | | | | | | |
| 43 | claude-code-game-studios | — | — | não varrido | excluído | Template de projeto, não plugin. Só referência. |
| 44 | Apps de referência: next-forge, Expo Skills, Instant, Nhost, Puck, assistant-ui, RN Reusables, Lago | — | Lago é AGPL | não varrido | excluído | Apps de referência, fora do escopo. |

## Testes

| Item | Teste | Resultado |
|---|---|---|
| motion-kit (`motion-designer`) | Carregar a skill do projeto numa sessão do Claude Code | OK: a skill apareceu na lista e carregou de `.claude/skills/motion-designer/` |
| humanizer | `claude plugin validate`; `/humanizer` em sessão headless com um parágrafo curto | OK: removeu travessão, contraposição "não é apenas X" e metáfora |
| explainer-studio | `claude plugin validate`; `npm ci --ignore-scripts`; `init` e `styleframes` (whiteboard, blueprint) | OK: storyboard e quadros PNG gerados. MP4 não testado: falta FFmpeg (`sudo apt install ffmpeg`) |

## Ambiente do usuário (instalado em 2026-11-21, sem sudo)

Todos em `~/.local` (binários em `~/.local/bin`). Os plugins foram instalados com `claude plugin install … --scope project`, e os marketplaces ficaram registrados também nas configurações de usuário do Claude Code.

| Ferramenta | Versão | Origem | Verificação |
|---|---|---|---|
| gh | 2.105.0 | Release oficial cli/cli | SHA-256 conferido |
| Node.js / npm | v26.13.1 / 11.20.0 | Release oficial nodejs.org (LTS) | SHA-256 conferido. Prefixo global do npm: `~/.local` |
| SkillSpector | 2.12.0 | `uv tool install` do repositório da NVIDIA | — |
| rtk, ccusage, omniroute, ccr, pake-cli, freellmapi, markitdown | ver tabela acima | npm, uv | `--version` ou `--help` respondem |

Não instalado (precisa de você): FFmpeg e bibliotecas do Pake (`sudo apt`), Rust (a instalação via rustup foi bloqueada pelo modo automático), Docker (servidor do freellmapi). Chaves de provedores para OmniRoute, claude-code-router e freellmapi.

## Pendências

- **Chaves de API (não pedidas no chat):** `ATLASCLOUD_API_KEY` (vox-director), Apify (linkedin-skills e career-ops), Publora (linkedin-skills). Os três itens estão excluídos, então nenhuma chave é necessária agora.
- **Varredura incompleta (6):** ui-ux-pro-max-skill, taste-skill, video-shotcraft, cinetic, anatomy e claude-mem. Próximo passo: rodar com mais tempo (sem paralelismo) ou com o modo LLM do SkillSpector, e depois revisar o código.
- **Ferramentas:** instaladas no ambiente do usuário, a pedido (ver seção acima). Faltam FFmpeg, Rust, as bibliotecas do Pake e Docker. awesome-design-md segue como referência (sem SKILL.md).

## Riscos

- **Scanner heurístico:** o SkillSpector sem LLM marca padrões, não intenção. Houve falsos positivos (humanizer, motion-kit) e quase todos os itens grandes saíram CRITICAL ou estouraram tempo/orçamento. CRITICAL aqui significa "não instalar sem revisão manual", não "malicioso confirmado".
- **Plugins por marketplace não estão fixados em commit.** Os commits revisados estão na tabela acima. Uma atualização do autor chega sem nova revisão. Fixar `ref` no `.claude/settings.json` ou revisar a cada atualização.
- **Configuração persistente:** `extraKnownMarketplaces` e `enabledPlugins` em `.claude/settings.json` oferecem esses plugins a todo mundo que abrir este repositório no Claude Code.
- **Rede no explainer-studio:** o TTS `edge` envia o texto da narração a um endpoint não oficial da Microsoft. Use `--tts silent` ou `cmd` para evitar.
- **Licenças:** itens não comerciais (anything2explainer, prompts do lemo-opuscar) e sem licença (motor PDoomVideo) ficaram fora.
