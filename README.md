# La Fresque oubliée — PaléoShell

Un **escape game en ligne de commande** pour apprendre les bases de **Linux** en
s'amusant. Tu es à la tête d'une fouille dans une grotte oubliée : salle après
salle, de petites énigmes te font dégager les fragments d'une fresque
mystérieuse. Quand les 25 fragments sont réunis, la fresque complète se révèle…

> Promo 2026 · B1 · **Coda Avignon**

---

## 1. Prérequis

- **Docker** installé et lancé :
  - Linux : `docker` (paquet de ta distribution) ;
  - macOS / Windows : [Docker Desktop](https://www.docker.com/products/docker-desktop/)
    (sur Windows, via **WSL2**).
- Rien d'autre : le jeu est entièrement dans l'image Docker (multi-arch, il
  tourne sur PC Intel **et** Mac Apple Silicon).

## 2. Lancer le jeu

```bash
docker pull ghcr.io/coda-avignon/paleoshell:latest
docker run -it --rm ghcr.io/coda-avignon/paleoshell
```

- `-it` → **indispensable** : sans ça, le terminal se ferme aussitôt.
- `--rm` → le conteneur repart **propre** à chaque lancement.

> **Besoin de s'authentifier ?** Si `docker pull` réclame un login (image
> privée), connecte-toi une fois avec un *Personal Access Token* GitHub
> (scope `read:packages`) :
> ```bash
> echo "TON_TOKEN" | docker login ghcr.io -u TON_USER_GITHUB --password-stdin
> ```

Pour **rejouer** : relance simplement la même commande `docker run …`.

## 3. À connaître avant de jouer

Quelques commandes de base, à voir en cours, ne sont **pas** enseignées par le
jeu : `pwd`, `cd`, `ls`, `cat`, et les redirections `>` / `>>`. Tout le reste
s'apprend en jouant, **une commande par salle**.

## 4. Comment on joue

Chaque salle contient une petite **énigme** qui te fait récupérer **un
fragment** (une ligne) de la fresque. Tu ajoutes chaque fragment, dans l'ordre,
à ton **relevé** `fresque` :

```bash
<ta commande> >> ../../fresque
```

*(À la salle 1 seulement, tu **crées** le relevé avec un simple `>`.)*

Le vocabulaire du chantier :

| Terme | Sens |
|-------|------|
| **fragment** | une ligne de la fresque (le but de chaque salle) |
| **`fragment.txt`** | un fichier qui contient **un seul** fragment |
| **`eclat.txt`** | un fichier de plusieurs lignes d'où il faut **extraire** le bon fragment |
| **`burin`** | l'outil (un programme) qui dégage le fragment |

Dans chaque salle :

- `mission.txt` — l'énigme ;
- `indice1.txt` — un coup de pouce (le concept + la page de `man` à consulter) ;
- `indice2.txt` — un second coup de pouce (seulement dans certaines salles).

Quand les **25 fragments** sont réunis, admire la fresque complète :

```bash
cat ~/fresque
```

Pour démarrer, une fois dans le conteneur :

```bash
cat BIENVENUE.txt
cd salle1
cat mission.txt
```

## 5. Commandes d'aide (disponibles partout dans le jeu)

| Commande | Effet |
|----------|-------|
| `verifier` | contrôle ton relevé salle par salle, dit où ça coince, et **sauvegarde** ta progression |
| `restaurer` | recharge ta dernière sauvegarde (rattrape un `>` mis à la place d'un `>>`) |
| `reparer [N]` | remet une salle à neuf (fichier supprimé, écrasé, droits cassés…) ; depuis une salle, `reparer` tout court suffit |
| `reprendre N` | efface le relevé à partir du fragment N, pour refaire la salle N |

> 💡 **Lance `verifier` après chaque salle** : c'est lui qui sauvegarde ta
> progression.

## 6. Un souci ?

- Un fichier abîmé dans une salle → la commande `reparer` du jeu (remet la salle
  à neuf).
- Bloqué sur une énigme → relis `indice1.txt`, teste, et demande à ton
  formateur.
- Le terminal devient illisible → tape `clear`, ou `tput reset` si c'est
  vraiment brouillé.

---

<sub>Coda Avignon — Promo 2026 · B1 · *La Fresque oubliée (PaléoShell)*</sub>
