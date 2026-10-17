<div align="center">



\# ⚡ HeroCode



\*\*Assistant de programmation IA en un seul fichier Python.\*\*



\[!\[Python](https://img.shields.io/badge/python-3.10%2B-blue?style=flat-square)](https://python.org)

\[!\[License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)

\[!\[Version](https://img.shields.io/badge/version-2.1-purple?style=flat-square)](CHANGELOG.md)

\[!\[PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](CONTRIBUTING.md)



\[Installation](#-installation) · \[Fonctionnalités](#-fonctionnalités) · \[Commandes](#-commandes) · \[Plugins](docs/plugins.md) · \[MCP](docs/mcp.md)



</div>



\---



HeroCode est un agent de code IA qui vit dans ton terminal. Il lit ton projet,

édite tes fichiers, cherche sur Internet, donne la météo, pilote Roblox Studio,

écoute ta voix et se branche sur Ollama en local. \*\*Un seul fichier, zéro télémétrie.\*\*



Créé par \[Herobrinepft](https://herobrinepft.netlify.app/).



\## ✨ Fonctionnalités



\- 🧠 \*\*Multi-LLM\*\* — Ollama local, llama.cpp, OpenAI, Gemini, Claude, Grok

\- 🔌 \*\*MCP natif\*\* — stdio + HTTP, connecteurs Gmail, Slack, Roblox Studio

\- 🎤 \*\*Dictée vocale Windows\*\* — API native WinRT, français

\- 🧩 \*\*Plugins\*\* — dépose un `.py` dans `\~/.herocode/plugins/`

\- 👥 \*\*Agents\*\* — reviewer, teacher, devops, roblox… + agents custom

\- 💾 \*\*Sessions persistantes\*\* — reprends où tu t'es arrêté

\- 🌐 \*\*Recherche web\*\* — DuckDuckGo + sources citées

\- 🌤️ \*\*Météo\*\* — Open-Meteo, sans clé API

\- 🛡️ \*\*Permissions granulaires\*\* — chaque action sensible demande `\[o/N]`

\- 🔒 \*\*Privacy-first\*\* — 0 télémétrie, clés API en mémoire de session uniquement



\## 🚀 Installation



\*\*Prérequis :\*\* Python 3.10+



```bash

\# 1. Télécharger

git clone https://github.com/herobrinepft/herocode.git

cd herocode



\# 2. (Optionnel) installer les dépendances

pip install mcp                                          # MCP

pip install winrt-Windows.Media.SpeechRecognition winrt-Windows.Globalization winrt-runtime   # /voice (Windows)



\# 3. Lancer

python herocode.py

