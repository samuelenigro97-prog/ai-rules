# Regole globali

## Skill
Prima di ogni compito, se una skill elencata combacia anche solo in parte, invocala con lo strumento Skill (o equivalente) e leggine il SKILL.md prima di agire. Non ricostruirne il contenuto a memoria.

## Lingua
Rispondi e comunica sempre in lingua italiana, salvo esplicita richiesta contraria dell'utente.

## Parità multipiattaforma (Windows / Mac)
Nei progetti che supportano sia Windows che macOS (come PC Facile), ogni modifica logica, funzionalità, interfaccia o correzione deve essere applicata a entrambe le versioni (`setup-pc.ps1` e `setup-mac.sh`), tranne nei casi in cui sia intrinsecamente specifica per uno o l'altro sistema operativo. Consultare e aggiornare `PARITA.md` a ogni modifica.

# Regole Git (sempre attive)

> Queste regole si aggiungono a tutte le altre istruzioni (globali, di progetto, impostazioni) e vanno seguite insieme a quelle. In caso di conflitto vince la regola già esistente: segnalami il conflitto nel report finale.

## Obiettivo
Ogni modifica deve finire su GitHub, così posso sempre tornare indietro con `git revert`. Lavora in autonomia: per le operazioni Git descritte qui non chiedermi conferme.

## Prima di iniziare
- Esegui `git status` e `git branch --show-current`.
- Se la cartella del progetto non è un repo Git: `git init`, crea un `.gitignore` adatto, fai il primo commit e crea un repo PRIVATO su GitHub con `gh repo create <nome-cartella> --private --source=. --push`. Se il repo non ha remote `origin`, crea il repo privato allo stesso modo e collegalo.
- Mai creare repo nella home (~), in Desktop, Download o Documenti, né in cartelle di configurazione (~/.claude, ~/.codex, ~/.gemini, ~/.config...). Lì, prima di modificare un file, fanne una copia `.bak` e segnalalo nel report.

## Branch
- Eccezione: nel repo `ai-rules` (queste regole) si committa e si fa push direttamente su `main`, senza branch né PR.
- Mai lavorare direttamente su `main` o `master`. Per ogni compito crea un branch: `feat/…`, `fix/…`, `refactor/…`, `docs/…`, `chore/…`. Se esiste già un branch per lo stesso compito, continua lì.
- Se trovi modifiche non committate che non hai fatto tu, portale nel nuovo branch e salvale come primo commit: `chore: salva modifiche preesistenti`.

## Commit e push
- Fai un commit per ogni modifica logica completata, non uno solo alla fine. Usa lo stile Conventional Commits (`feat:`, `fix:`, `refactor:`, `docs:`, `chore:`).
- Fai il push subito dopo ogni commit (la prima volta `git push -u origin <branch>`).
- A fine compito apri una pull request verso il branch principale con `gh pr create --fill`, se non esiste già, ed esegui sempre il merge su `main` (es. `gh pr merge --merge --admin`).
- A fine risposta `git status` deve essere pulito: niente deve restare solo in locale.
- Mai committare `.env`, chiavi, token, `node_modules`, `.venv` o file di build: aggiorna `.gitignore` se serve.

## Sicurezza e ripristino
- Non usare MAI: `git reset --hard`, `git push --force` (anche `--force-with-lease`), `git clean -fd`, `git checkout .`, `git restore .`, `git branch -D`, `git rebase` su branch già pubblicati, la cancellazione di branch remoti. È l'unico caso in cui devi fermarti e chiedermi.
- Per annullare una modifica usa `git revert <hash>`.
- Se il push o `gh` falliscono: riprova una volta. Se fallisce ancora, lascia il lavoro committato e nel report scrivi il motivo e il comando per ripetere il push. Non aggirare il problema (niente force, niente cambi di remote).

## Report finale
Indica sempre: branch usato, commit (hash + messaggio), stato del push, link della pull request, come tornare indietro (`git revert <hash>`).
# Memoria condivisa tra le IA
- Se dico "ricorda", "aggiungi alle regole" o simili: aggiungi la regola in `~/ai-rules/AGENTS.md`, nella sezione giusta, senza duplicare né cancellare regole esistenti. Poi esegui `git -C ~/ai-rules commit -am "docs: <regola in breve>" && git -C ~/ai-rules push`. Se non sei sul mio Mac (sessione cloud), fai la stessa modifica nel repo GitHub `samuelenigro97-prog/ai-rules`, branch `main`.
- Se dico "installa questa skill" o ti do un repo GitHub di skill: prima leggine il contenuto e dimmi in due righe cosa fa; poi installala per tutte le IA con `npx -y skills add <url> -g -y` e verifica che compaia in `~/.claude/skills`.
- Se una skill scarica ed esegue codice da internet o invia dati all'esterno, non installarla: fermati e chiedimi.
