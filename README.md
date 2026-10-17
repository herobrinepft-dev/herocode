# HeroCode

**Assistant de programmation intelligent** — terminal, interface graphique et web.

Créé par [Herobrinepft](https://herobrinepft.netlify.app/)

![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-Proprietary-lightgrey)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-green)

---

## Présentation

HeroCode est un agent de code local qui combine :

- un **terminal** interactif riche
- un **panneau graphique** (`/panel`) style app moderne
- une **interface web** (`/web`) avec fond animé
- des **outils système** (fichiers, dossier, processus) avec **autorisation explicite**
- des **plugins**, des **agents** (personas) et la **sauvegarde de conversations**

Il se connecte à tes propres modèles : **llama.cpp**, **Ollama**, OpenAI, Gemini, Claude, Grok.

---

## Fonctionnalités

| Domaine | Détails |
|--------|---------|
| **IA** | llama.cpp (2 serveurs), Ollama local, OpenAI, Gemini, Claude, Grok |
| **Fichiers** | Créer dossiers/fichiers, lire, déplacer, supprimer (avec accord) |
| **Web** | Recherche DuckDuckGo + sources, lecture d’URL, météo Open-Meteo |
| **MCP** | Connexion Roblox Studio et serveurs MCP (stdio / HTTP) |
| **UI** | Terminal, Tkinter `/panel`, navigateur `/web` |
| **Voix** | Dictée Windows WinRT (`/voice`) |
| **Plugins** | Dossier `~/.herocode/plugins/` |
| **Agents** | Personas configurables (`/agent`) |
| **Historique** | `/save`, `/load`, `/conversations` |

---

## Installation

### Prérequis

- **Python 3.9+**
- (Optionnel) [Ollama](https://ollama.com/) pour l’IA locale
- (Optionnel) `pip install mcp` pour les outils MCP / Roblox
- (Windows, voix)  
  `pip install winrt-Windows.Media.SpeechRecognition winrt-Windows.Globalization winrt-runtime`

### Lancer

```bash
git clone https://github.com/TON_USER/HeroCode.git
cd HeroCode
python HeroCode.py
```

Sous Windows :

```powershell
python HeroCode.py
```

---

## Configuration rapide

### Ollama (recommandé en local)

```bash
ollama serve
ollama pull llama3.2
```

Dans HeroCode :

```
/provider
```

Choisis **Ollama (local)**.  
Variables d’environnement optionnelles :

| Variable | Défaut | Description |
|----------|--------|-------------|
| `OLLAMA_BASE_URL` | `http://127.0.0.1:11434` | URL du serveur Ollama |
| `OLLAMA_MODEL` | `llama3.2` | Modèle par défaut |
| `LLAMA_BASE_URL` | — | Serveur llama.cpp |
| `OPENAI_API_KEY` | — | Clé OpenAI |
| `ANTHROPIC_API_KEY` | — | Clé Claude |
| `GEMINI_API_KEY` | — | Clé Google |
| `XAI_API_KEY` | — | Clé Grok |
| `HEROCODE_MAX_TOKENS` | `4096` | Tokens de sortie max |

Les clés saisies dans l’app restent **en mémoire de session** (jamais écrites sur le disque par HeroCode).

---

## Commandes principales

```
/help                 Aide
/provider             Changer d’IA
/model <id>           Changer de modèle
/panel                Interface graphique
/web                  Interface web (http://127.0.0.1:8765)
/web stop             Arrêter le serveur web
/voice                Dictée vocale (Windows)
/agent                Configurer un agent / persona
/plugins reload       Recharger les plugins
/search <requête>     Recherche web (+ sources)
/weather <ville>      Météo
/fetch <url>          Lire une page web
/tree                 Arborescence du projet
/read <fichier>       Ajouter un fichier au contexte
/write                Créer / modifier un fichier (avec diff)
/save [nom]           Sauvegarder la conversation
/load [nom]           Recharger une conversation
/conversations        Lister les sauvegardes
/license              Licences et attributions
/stats                Statistiques
/clear                Effacer la conversation
/quit                 Quitter
```

### MCP (Roblox, etc.)

```
/mcp-connect stdio <cmd> [args…]
/mcp-connect http <url>
/mcp
/mcp-status
/mcp-disconnect
```

Tu peux aussi écrire naturellement :  
*« connecte-toi à Roblox Studio »*

---

## Outils système (avec autorisation)

Quand tu demandes par exemple :

> crée un dossier bonjour sur mon bureau

HeroCode propose un outil (`mkdir`, `write_text`, …) et **demande ton accord** avant d’exécuter.

| Outil | Rôle |
|-------|------|
| `mkdir` | Créer un dossier |
| `list_dir` | Lister un dossier |
| `write_text` | Écrire un fichier |
| `read_text` | Lire un fichier |
| `delete_path` | Supprimer (dossier vide uniquement) |
| `move_path` | Déplacer / renommer |
| `open_path` | Ouvrir dans l’explorateur |
| `web_search` | Recherche Internet (auto) |
| `get_weather` | Météo (auto) |
| `fetch_url` | Lire une URL |
| `process_list` / `process_terminate` | Processus |

Zones autorisées : **dossier utilisateur**, **bureau**, **projet courant**.  
Les chemins système sensibles sont refusés.

---

## Interface web (`/web`)

```
/web
```

Ouvre une page locale avec :

- fond bleu animé (orbes + grille)
- chat en direct
- menu **IA ▾** pour changer de fournisseur
- suggestions au démarrage
- même historique que le terminal

---

## Plugins

Place des fichiers Python dans :

```
~/.herocode/plugins/        # Linux / macOS
%USERPROFILE%\.herocode\plugins\   # Windows
```

Exemple minimal :

```python
NAME = "hello"

def on_load(ctx):
    print("Plugin hello chargé")

def on_command(cmd, arg, ctx):
    if cmd == "/hello":
        print(f"  Bonjour {arg or 'monde'} !")
        return True
    return False

def on_message(text, ctx):
    return None  # None = laisser l’IA répondre
```

Puis :

```
/plugins reload
```

Des exemples sont fournis dans le dossier `plugins/` du dépôt (`utils.py`, `hello.py`).

---

## Agents

```
/agent
```

Personas intégrés : **default**, **code-reviewer**, **teacher**, **roblox**, **devops**.  
Tu peux en créer d’autres (sauvegardés dans `~/.herocode/agents/`).

---

## Structure du projet

```
HeroCode/
├── HeroCode.py          # Application principale
├── README.md
└── plugins/             # Exemples de plugins
    ├── hello.py
    └── utils.py
```

Données utilisateur (créées à l’exécution) :

```
~/.herocode/
├── plugins/
├── agents/
└── conversations/
```

---

## Sécurité

- Pas de shell arbitraire
- Actions fichiers / processus **confirmées** par l’utilisateur
- Suppression de dossiers limitée aux dossiers **vides**
- Recherche web et pages externes traitées comme **données non fiables**
- Clés API uniquement en mémoire de session

---

## Dépannage

| Problème | Solution |
|----------|----------|
| Ollama inaccessible | `ollama serve` puis `/provider` → Ollama |
| `/voice` ne marche pas | Windows uniquement + packages WinRT |
| Plugins vides | Copier les `.py` dans `~/.herocode/plugins/` puis `/plugins reload` |
| Port web occupé | `/web 9000` |
| MCP Roblox | Activer le serveur MCP dans Studio + `/mcp-connect` ou phrase « connecte-toi à Roblox Studio » |

---

## Licence & attributions

Voir la commande `/license` dans l’application.

Services tiers utilisés selon ta config : DuckDuckGo, Open-Meteo, Ollama, APIs cloud (OpenAI, Anthropic, Google, xAI), MCP SDK, WinRT (Windows).

---

## Auteur

**Herobrinepft**  
Portfolio : [herobrinepft.netlify.app](https://herobrinepft.netlify.app/)

---

*HeroCode — code localement, reste aux commandes.*
'''
Path = __import__("pathlib").Path
Path("/home/workdir/artifacts/README.md").write_text(
    Path("/home/workdir/artifacts/README.md").read_text(encoding="utf-8") if False else open("/home/workdir/artifacts/README.md", encoding="utf-8").read() if False else "",
    encoding="utf-8",
)
print("skip")
