# AI Weekend 201 — Langflow Flows

Hands-on flows for the **AI Weekend 201** Day 1 sessions. Each session
is a [Langflow](https://www.langflow.org) flow: you import a **starter** with one critical piece
missing, follow the yellow Note on the canvas to complete it, and test it in the Playground.
Everything runs on the shared Langflow server (`langflow.aiweekend.net`); nothing is installed on your machine.

Together the six sessions build one assistant, layer by layer:

> **reason → orchestrate → remember → tools → deploy → observe**


## Hızlı başlangıç (Türkçe)

1. Kurulum yok: Langflow (1.13.3) ortak sunucuda (`langflow.aiweekend.net`) çalışır. Kendi hesabınla tarayıcıdan gir.
2. Eğitmenden `XAI_API_KEY`, `OPENAI_API_KEY` (embedding) ve `TAVILY_API_KEY` anahtarlarını al. Langflow'da *Settings > Global
   Variables* altında **Credential** türünde, tam bu adlarla ekle.
3. Bir track seç: `mutfak` (ana track), `hafta-sonu`, `finans` veya `seyahat`.
4. Oturumun starter dosyasını (`<track>/0N-….json`) Langflow'a yükle, tuvaldeki sarı Note'u oku,
   eksik parçayı tamamla ve Playground'da dene. Takılırsan bir sonraki oturumun starter'ı önceki katmanları hazır getirir.
   Hazır metinler (Prompt, router kuralları, hakem talimatı) sarı Note'un içinde, ayrıca `<track>/kopyala-yapistir.md` dosyasında.
5. Dosya seçicileri (File) içe aktarmadan sonra boş gelir: dosyaları `assets/<track>/` klasöründen
   yeniden seç.

### Tuvaldeki renkler

Her akış öncekinin üstüne yeni bir katman ekler. Neyin yeni olduğunu şöyle ayırt edersin:

| Renk | Anlamı |
|---|---|
| 🟨 **Sarı Note** (solda) | Senin yapacağın eksik parça; adımlar ve hazır metin burada. |
| 🟩 **Yeşil Note** | Bu oturumda yeni gelen bir bileşenin ne olduğunu ve ne işe yaradığını 2-3 cümleyle anlatır. Bileşenin hemen altındadır. |
| 🟦 **Mavi kutu** | Önceki oturumlardan kalan, hazır bir bileşen. Başlığında hangi oturumdan geldiği ve ne işe yaradığı yazar; dokunman gerekmez. |

## Before the event

Langflow (1.13.3, the version the flow JSONs were aligned to) runs on the shared server `langflow.aiweekend.net`, one account per
participant, so participants install nothing. What has to be ready before the session:

| What | How |
|---|---|
| **Account** | Each participant signs up on the shared Langflow server. |
| **Node.js** | Needed on the server for `npx`, which starts the filesystem MCP server (session 04 onward). |
| **API keys** | Get `XAI_API_KEY` (xAI, model `grok-4.3`), `OPENAI_API_KEY` (embeddings, model `text-embedding-3-small`) and `TAVILY_API_KEY` (web search) from the instructor. Keys live only in Langflow, never in a flow file. |

### Add the keys to Langflow

*Settings > Global Variables > Add New*, type **Credential**, one variable per key, with these exact names:

- `XAI_API_KEY`
- `OPENAI_API_KEY`
- `TAVILY_API_KEY`

### If xAI fails

- `'str' object has no attribute 'get'` almost always means the `XAI_API_KEY` global variable is missing, misspelled or empty.
  Check its name and value under *Settings > Global Variables*.
- A new xAI component dragged from the sidebar defaults to `grok-2-latest`, which no longer exists (404). Set *Model Name* to `grok-4.3`.

## Pick a track

All four tracks teach the same six layers on a different everyday scenario. Pick one and stay on it;
the deck screenshots use **mutfak**.

| Track | Folder | Scenario |
|---|---|---|
| **Mutfak** (main) | `mutfak/` | A home-kitchen assistant: what to cook from what you have, shopping lists, nutrition, family allergies and house rules from a recipe book. |
| **Hafta sonu** | `hafta-sonu/` | A weekend planner for İzmir: places to go, weather, transport, and your stated preferences. |
| **Finans** | `finans/` | A personal-budget coach: reads your expenses (CSV), compares them with your targets, and suggests where to cut. |
| **Seyahat** | `seyahat/` | A trip preparer for Lisbon: day-by-day plans plus visa and document checks against a checklist PDF. |

All input data is synthetic and lives in `assets/<track>/`.

## Sessions

| Flow | Deck | Layer added | Starter's missing piece |
|---|---|---|---|
| `01-temel` | Advanced LLMs | Prompt with chain-of-thought | The Prompt component. |
| `02-akis` | Agentic Workflows | Smart Router + specialist Agents | The router's routes. |
| `03-hafiza` | Advanced RAG & Memory | Knowledge base retrieval + chat memory | The knowledge base (and its embedding model). |
| `04-araclar` | MCP & Tool Calling | Web search, calculator, filesystem MCP | The MCP Tools node. |
| `05-yayin` | Deploy the Agent | API endpoint + shareable chat URL | The endpoint name. |
| `06-izleme` | LLMOps | LLM-as-judge + Traces | The judge prompt. |

For each session: *Upload a flow* with `<track>/0N-….json`, read the yellow Note, finish the
missing piece, then test in the Playground. Each session starts from the previous session's solution
logic, so the flows grow session by session. If you fall behind, import the next session's starter: it ships
with every earlier layer already complete.

### What to do after every import

- **File pickers are empty.** Uploaded paths are machine-specific, so every `Read File` component
  comes in empty. Re-pick the files from `assets/<track>/` (the Note names them).
- **The xAI key may look blank.** On the first open of an imported flow, Langflow 1.13 can blank the
  xAI *API Key* field. Click the globe icon on the field and pick `XAI_API_KEY` again. Opening
  *Settings > Global Variables* before the flow avoids it.
- **"Setup Provider" button.** Agent and Smart Router can show a black *Setup Provider* button even
  when a model is wired in. Ignore it; the flow runs.

### Off-topic questions (Else branch)

From session 02 the Smart Router has its **Else** output on: a message that matches no route goes to a fixed *Konu dışı istemi*
Prompt and a *Konu dışı cevabı* Chat Output, which tells the user what the assistant can help with. Without it an off-topic
question got no answer at all.

### From session 03: create and fill the knowledge base

Starting at `03-hafiza`, the flow retrieves from a local knowledge base (SQLite, no server). Its
embeddings come from OpenAI, so `OPENAI_API_KEY` must be set first.
Then open *Settings > Model Providers > OpenAI* and switch on `text-embedding-3-small` under
*Embedding Models*: it is off by default, and until it is on, *Add Knowledge* shows "No models enabled".
Neither the starter nor the solution JSON carries it, so on each machine:

1. Open the **Knowledge** page (left sidebar, bottom) and choose *Add Knowledge*.
2. Name it for your track and choose **OpenAI `text-embedding-3-small`** as the embedding model (not the
   chat model). Names the flows expect:

   | Track | Knowledge base | Source file(s) |
   |---|---|---|
   | mutfak | `mutfak_tarifler` | the four recipe PDFs in `assets/mutfak/` |
   | hafta-sonu | `hafta_sonu_mekanlar` | `assets/hafta-sonu/mekanlar.pdf` |
   | finans | `finans_hedefler` | `assets/finans/notlar/butce-hedefleri.md` (the CSV is a separate input) |
   | seyahat | `seyahat_belgeler` | `assets/seyahat/vize-belge-kontrol-listesi.pdf` |

3. Back in the flow, select that knowledge base on **both** Knowledge components, pick the source
   file(s) in `Read File`, and press the play button on the **Ingest** component once.

The knowledge base name must match the table **exactly**: the flows select it by name, and a different or re-created name makes the
Knowledge component return 404. If its list is empty in a later session, refresh the field and pick the knowledge base again.

In `mutfak` the chat memory persists across Playground sessions (`session_id` is fixed to `kalici-hafiza` on the Chat Input, every Chat Output and
Message History, from 03 to 06), so what the user said in an earlier session, such as a diet or allergy, is remembered. Other tracks keep
memory within one Playground session.

Use the Knowledge page, not the Knowledge component's own *Create new Knowledge Base* dialog: in 1.13
that dialog cannot be submitted. Later sessions keep the same knowledge base, so you only do this once.

### From session 04: register the MCP server

The filesystem server is registered **by name** in Langflow, so no path is stored in a flow file. Once:

*Settings > MCP Servers > Add MCP Server*, **STDIO**:

- **Name:** `<track>-notlar` (for example `mutfak-notlar`)
- **Command:** `npx`
- **Arguments:** `-y`, `@modelcontextprotocol/server-filesystem`, and the **absolute path** to
  `assets/<track>/notlar` on your machine

On the shared server (`langflow.aiweekend.net`) there is no local repo checkout. Use your personal
folder instead: `/app/langflow/notlar/kisisel/<your-username>/<track>` (spaces in the username become
`-`). Every account gets its own copy of the track notes, created automatically within a minute of
signing up, so participants never write to each other's files.

Then add an **MCP Tools** component, select the server, turn on **Tool Mode**, and connect *Toolset*
to the Agent's *Tools*. In *Actions* keep only the four you need: `list_allowed_directories`,
`read_text_file`, `append_file`, `edit_file`. This applies to the **solutions too**: a solution from
`04` onward runs only after its MCP server and knowledge base exist.

### Session 05: deploy

There is no new component in this session; the flow is session 04's, published three ways.

- **Endpoint name (the missing piece):** the starter ships without one. In *Share > API access > Input Schema* the
  participant sets `<track>-asistani` (for example `mutfak-asistani`). A second flow with the same name gets a `-1` suffix;
  use the name shown in the panel.
- **API:** the cURL example in the same panel calls the flow. The API key comes from *Settings > Langflow API Keys*
  and goes into `LANGFLOW_API_KEY`, never into the command.
- **Shareable chat page:** *Share > Shareable Playground* gives the flow its own chat page at `/playground/<flow-id>`.
- **Per-user URL:** the yellow Note tells each participant to reach their bot at
  `https://KULLANICI-ID.ALAN-ADI/playground/<flow-id>`. That host is served by the instructor-side reverse proxy,
  which routes by user id. Replace `KULLANICI-ID.ALAN-ADI` in the `05-yayin` flows once the real domain is known
  (the same string appears in all four tracks' notes).

### Session 06: observe

Langflow 1.13 has a built-in **Traces** view (left rail of a flow): every Playground or API run shows
its span tree with latency, tokens and inputs/outputs. It needs no key and is on by default. The judge
branch in `06-izleme` is an ordinary part of the flow, so its score appears in the trace too.

Optional external tracers: set the variables in Langflow Desktop's `.env` (macOS
`~/.langflow/data/.env`, Windows `%APPDATA%\com.LangflowDesktop\data\.env`) and restart Langflow.

- **Langfuse:** `LANGFUSE_SECRET_KEY`, `LANGFUSE_PUBLIC_KEY`, `LANGFUSE_BASE_URL`.
- **LangSmith:** the Langflow docs list `LANGSMITH_TRACING`, `LANGSMITH_ENDPOINT`,
  `LANGSMITH_API_KEY`, `LANGSMITH_PROJECT`, but the 1.13 code only starts the tracer when
  `LANGCHAIN_API_KEY` is set and reads the project from `LANGCHAIN_PROJECT`. Set the `LANGCHAIN_*`
  pair; neither external tracer was exercised end to end for this workshop.

## Notes for instructors

- **Expect 10–20 seconds per reply.** The router and the answer are two model calls, and xAI latency
  varies. One early Playground reply took over two minutes while several people shared one key.
- **Shared keys:** if everyone uses the instructor's keys, run a load dry-run with the full group size
  before the event.
- **Reverse proxy:** session 05 only works end to end if the per-user host in the Note resolves to that
  participant's flows. Test one participant's URL before the session.
