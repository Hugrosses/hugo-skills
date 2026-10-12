# hugo-skills

Ma marketplace Claude Code perso : une sélection de skills et de plugins, installable en deux commandes sur n'importe quelle machine.

## Installer sur une nouvelle machine

Dans une session Claude Code :

```
/plugin marketplace add <ton-compte-github>/hugo-skills
```

Puis installe les plugins :

```
/plugin install design-kit@hugo-skills
/plugin install dev-kit@hugo-skills
/plugin install superpowers@hugo-skills
/plugin install persistent-memory@hugo-skills
/plugin install impeccable@hugo-skills
/plugin install img2threejs@hugo-skills
```

Ensuite, ajoute ce bloc dans `~/.claude/settings.json`. S'il y a déjà un bloc `env`, fusionne les lignes dedans.

```json
{
  "env": {
    "DO_NOT_TRACK": "1",
    "CLAUDE_MEM_FILE_READ_GATE_ENABLED": "false"
  }
}
```

- `DO_NOT_TRACK` coupe la télémétrie de claude-mem (PostHog) et celle d'impeccable.
- `CLAUDE_MEM_FILE_READ_GATE_ENABLED=false` empêche claude-mem de bloquer la lecture complète des fichiers qu'il a déjà vus. L'historique du fichier reste ajouté au contexte.

Pour recevoir les mises à jour automatiquement, ouvre `/plugin`, va dans **Marketplaces**, choisis `hugo-skills`, puis **Enable auto-update**. Sinon, lance `/plugin marketplace update hugo-skills`.

## Prérequis par plugin

| Plugin | Ce qu'il faut sur la machine |
| --- | --- |
| design-kit | Rien |
| dev-kit | `npm install -g @playwright/cli@latest` |
| superpowers | bash. Node seulement pour le compagnon de brainstorming |
| persistent-memory (claude-mem) | Node ≥ 20.12 et Bun ≥ 1.1.31. Aussi `uv` pour la recherche sémantique Chroma (activée par défaut) |
| impeccable | curl, et internet au premier lancement : il télécharge son moteur dans `~/.impeccable/bin/` |
| img2threejs | Node ≥ 18. Python pour certains scripts de vérification |

## Contenu

**design-kit** (19 skills, copiés ici)
- taste-skill (Leonxlnx) : `taste-skill`, `redesign-skill`, `minimalist-skill`, `soft-skill`
- Emil Kowalski : `animate`, `improve-animations`, `review-animations`, `animation-performance`, `emil-design-eng`, `apple-design`, `break-ui`, `prototype`, `pick-ui-library`, `mobile-native`
- awesome-design-skills (Bergside), renommés `style-*` : `style-power`, `style-premium`, `style-refined`, `style-enterprise`, `style-shadcn`

**dev-kit** (1 skill, copié ici) : `playwright-cli` (Microsoft)

**Tirés directement des repos d'origine** (ils se mettent à jour avec eux) :
- `superpowers` (obra/superpowers) : 15 skills, plus un hook au démarrage de chaque session
- `persistent-memory` (thedotmack/claude-mem) : 23 skills, 8 hooks, un serveur MCP et un worker local sur 127.0.0.1
- `impeccable` (pbakaus/impeccable) : 1 skill (24 sous-commandes), 4 agents, 3 hooks
- `img2threejs` (img2threejs/img2threejs) : 1 skill

## Ce qui n'est pas dedans, et pourquoi

- **addyosmani/agent-skills** : fait doublon avec superpowers (TDD, revue de code, plans).
- **Le reste de taste-skill** : les variantes v1 et gpt font doublon. Les générateurs d'images sont pensés pour Codex.
- **Les 62 autres styles de Bergside** : ils alourdiraient la liste des skills que Claude charge à chaque session.
- **write-swift, animate-expo, ask-sonner** (Emil) : spécifiques au natif iOS/React Native ou à une seule librairie.
- **morluto/rea** : rétro-ingénierie de binaires, et il faut aussi son serveur MCP.
- **code-review** (claude-plugins-official) : `/code-review` est déjà intégré à Claude Code.
- **lenis, react-bits, gsap** : ce sont des librairies JavaScript, pas des skills.
- **scroll-world** : payant (vidéos générées via Monid et Higgsfield, environ 27 $ par séquence).
- **graphify** : il installe son propre skill. Sur chaque machine, lance `uv tool install graphifyy` puis `graphify install`.

## Limites

- Rien ici n'est payant. claude-mem fait ses résumés avec Claude Haiku, ce qui consomme ton quota d'abonnement Claude, sans frais en plus. N'utilise pas son skill `cloud-sync` : il sert à l'offre payante cmem.ai.

- Les plugins sont installés par machine. Les sessions cloud de Claude Code et les tâches planifiées dans le cloud ne chargent pas les plugins de tes réglages utilisateur.
- Coût en contexte : environ 6 000 tokens ajoutés à chaque session pour l'ensemble. Pour en retirer un temporairement : `/plugin disable <nom>@hugo-skills`.
- Pour mettre à jour les skills copiés dans design-kit et dev-kit, il faut les recopier depuis leurs repos d'origine et augmenter `version` dans leur `plugin.json`.

## Licences

Les skills copiés gardent leur licence d'origine : MIT pour taste-skill, Emil Kowalski et awesome-design-skills ; Apache-2.0 pour playwright-cli. Les fichiers de licence sont dans `plugins/*/licenses/`.
