# nebx-miner

NVIDIA GPU miner for **NEB (NeuralEngineByte)**, built by [NurseryPool](https://neb.nurserypool.com).

- nebhash v1, then **KEP1** and **RET2** from block 8800, switch is automatic, no restart
- RTX 30, 40 and 50 series, multi-GPU rigs
- Linux and Windows 10/11
- only a recent NVIDIA driver is needed, no CUDA install
- every share is recomputed with the reference code before it is sent

Current version: **0.9.0** (see [Releases](../../releases)).

## Measured hashrates

RTX 5060 Ti 16 GB, power limit 150 W, Linux, measured on 2026-11-13 with the built-in self-test.

| Engine | Hashrate |
|---|---|
| KEP1, fork-day model | 31.35 MH/s |
| KEP1, simulated model after 200 training steps | 32.52 MH/s |
| RET2, fork-day model | 8.10 MH/s |
| nebhash v1, Kepler jobs (before block 8800) | 45 to 52 MH/s |
| nebhash v1, retina jobs (before block 8800) | 10.8 MH/s |

More cards will be added as benchmarks come in. Every figure in this table is a measurement, none is an estimate.

## Quick start

You need the file `neb-datasets.bin` from NEB 0.3.0 (259,897,080 bytes).

### Linux

```
tar xzf nebx-0.9.0-linux.tar.gz && cd nebx-0.9.0-linux && chmod +x nebx-miner
./nebx-miner --essai --dataset /path/to/neb-datasets.bin
./nebx-miner --pool 162.19.84.16:3461 --user YOUR_NEB1_ADDRESS.RIG_NAME --dataset /path/to/neb-datasets.bin --suggest-diff 300000000
```

Requires a 64-bit Linux with glibc 2.38 or newer (Ubuntu 24.04 for example).

### Windows

1. Unzip `nebx-0.9.0-windows.zip` and copy `neb-datasets.bin` into the folder.
2. Double-click `essai.bat` to run the self-test.
3. Edit `miner.bat` with Notepad, set the NEB address and the rig name, then double-click it.

The Windows build is new: feedback is welcome.

## Self-test

`--essai` runs without a pool. For each card it checks the KEP1 and RET2 engines against the CPU reference and prints the hashrate. It takes about one minute per card. Every line must end with `CONFORME` and the last line must read `ESSAI : TOUT CONFORME`.

## Options

| Option | Meaning |
|---|---|
| `--pool HOST:PORT` | pool address (JSON stratum) |
| `--user ADDRESS.RIG` | NEB address and rig name |
| `--dataset FILE` | path to `neb-datasets.bin` |
| `--devices 0,1` | cards to use, default is all, numbered in PCI bus order like nvidia-smi |
| `--suggest-diff N` | starting share difficulty |
| `--essai` | self-test, no pool |

## Developer fee

1 %: one minute out of 100 is mined for NurseryPool. The miner says so at startup and prints the start and the end of each fee minute.

## Verify your download

Compare the SHA-256 of the archive with `SHA256SUMS.txt`:

```
sha256sum nebx-0.9.0-linux.tar.gz
```

On Windows: `certutil -hashfile nebx-0.9.0-windows.zip SHA256`

---

# nebx-miner (français)

Mineur GPU NVIDIA pour **NEB (NeuralEngineByte)**, réalisé par [NurseryPool](https://neb.nurserypool.com).

- nebhash v1, puis **KEP1** et **RET2** à partir du bloc 8800, bascule automatique, sans redémarrage
- RTX séries 30, 40 et 50, rigs multi-cartes
- Linux et Windows 10/11
- un pilote NVIDIA récent suffit, aucune installation de CUDA
- chaque share est recalculé par le code de référence avant envoi

Version actuelle : **0.9.0** (voir [Releases](../../releases)).

## Débits mesurés

RTX 5060 Ti 16 Go, limite de puissance 150 W, Linux, mesurés le 13/11/2026 avec l'essai intégré.

| Moteur | Débit |
|---|---|
| KEP1, modèle du jour du fork | 31,35 MH/s |
| KEP1, modèle simulé après 200 pas d'entraînement | 32,52 MH/s |
| RET2, modèle du jour du fork | 8,10 MH/s |
| nebhash v1, jobs Kepler (avant le bloc 8800) | 45 à 52 MH/s |
| nebhash v1, jobs rétine (avant le bloc 8800) | 10,8 MH/s |

D'autres cartes seront ajoutées à mesure que les bancs arrivent. Chaque chiffre de ce tableau est une mesure, aucun n'est une estimation.

## Démarrage rapide

Il faut le fichier `neb-datasets.bin` de NEB 0.3.0 (259 897 080 octets).

### Linux

```
tar xzf nebx-0.9.0-linux.tar.gz && cd nebx-0.9.0-linux && chmod +x nebx-miner
./nebx-miner --essai --dataset /chemin/vers/neb-datasets.bin
./nebx-miner --pool 162.19.84.16:3461 --user ADRESSE_NEB1.NOM_DU_RIG --dataset /chemin/vers/neb-datasets.bin --suggest-diff 300000000
```

Il faut un Linux 64 bits avec glibc 2.38 ou plus (Ubuntu 24.04 par exemple).

### Windows

1. Dézipper `nebx-0.9.0-windows.zip` et copier `neb-datasets.bin` dans le dossier.
2. Double-cliquer `essai.bat` pour lancer l'essai.
3. Ouvrir `miner.bat` avec le Bloc-notes, mettre l'adresse NEB et le nom du rig, puis double-cliquer.

La version Windows est nouvelle : les retours sont bienvenus.

## Essai

`--essai` fonctionne sans pool. Pour chaque carte, il vérifie les moteurs KEP1 et RET2 face à la référence CPU et affiche le débit. Il prend environ une minute par carte. Chaque ligne doit finir par `CONFORME` et la dernière doit dire `ESSAI : TOUT CONFORME`.

## Frais développeur

1 % : une minute sur 100 est minée pour NurseryPool. Le mineur l'annonce au démarrage et affiche le début et la fin de chaque minute de frais.

## Vérifier le téléchargement

Comparer le SHA-256 de l'archive avec `SHA256SUMS.txt` :

```
sha256sum nebx-0.9.0-linux.tar.gz
```

Sous Windows : `certutil -hashfile nebx-0.9.0-windows.zip SHA256`
