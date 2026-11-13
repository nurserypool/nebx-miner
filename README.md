# nebx-miner

NVIDIA GPU miner for **NEB (NeuralEngineByte)**, built by [NurseryPool](https://neb.nurserypool.com).

- nebhash v1, then **KEP1** and **RET2** from block 8800, switch is automatic, no restart
- RTX 30, 40 and 50 series, multi-GPU rigs
- Linux and Windows 10/11
- only a recent NVIDIA driver is needed, no CUDA install
- every share is recomputed with the reference code before it is sent

Current version: **0.9.0** (see [Releases](../../releases)).

## Measured hashrates

Measured on 2026-11-13 with the built-in self-test (`--essai`), in MH/s. Each range is the lowest and the highest card of that model.

| Card | Cards tested | System | KEP1, fork-day model | KEP1, model after 200 training steps | RET2, fork-day model |
|---|---|---|---|---|---|
| RTX 5060 Ti 16 GB (150 W) | 3 | Linux | 30.20 to 31.35 | 31.58 to 32.52 | 7.85 to 8.10 |
| RTX 3080 Ti | 3 | Windows | 18.67 to 18.76 | 24.99 to 25.77 | 9.30 to 9.43 |
| RTX 3080 | 4 | Windows | 14.53 to 15.09 | 20.32 to 21.71 | 7.77 to 7.89 |
| RTX 3070 | 4 | Windows | 11.26 to 11.32 | 14.66 to 15.01 | 5.51 to 5.64 |
| RTX 3060 Ti | 7 | Windows | 10.36 to 10.48 | 12.30 to 12.72 | 4.63 to 4.79 |

The trained KEP1 model is a simulated one, shipped inside the miner for the self-test. The power limit is given when it is known. More cards will be added as benchmarks come in. Every figure in this table is a measurement, none is an estimate.

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

The Windows build has been run on RTX 30 series cards. Feedback on other cards is welcome.

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

Mesurés le 13/11/2026 avec l'essai intégré (`--essai`), en MH/s. Chaque fourchette donne la carte la plus lente et la plus rapide du modèle.

| Carte | Cartes testées | Système | KEP1, modèle du jour du fork | KEP1, modèle après 200 pas d'entraînement | RET2, modèle du jour du fork |
|---|---|---|---|---|---|
| RTX 5060 Ti 16 Go (150 W) | 3 | Linux | 30,20 à 31,35 | 31,58 à 32,52 | 7,85 à 8,10 |
| RTX 3080 Ti | 3 | Windows | 18,67 à 18,76 | 24,99 à 25,77 | 9,30 à 9,43 |
| RTX 3080 | 4 | Windows | 14,53 à 15,09 | 20,32 à 21,71 | 7,77 à 7,89 |
| RTX 3070 | 4 | Windows | 11,26 à 11,32 | 14,66 à 15,01 | 5,51 à 5,64 |
| RTX 3060 Ti | 7 | Windows | 10,36 à 10,48 | 12,30 à 12,72 | 4,63 à 4,79 |

Le modèle KEP1 entraîné est un modèle simulé, fourni dans le mineur pour l'essai. La limite de puissance est indiquée quand elle est connue. D'autres cartes seront ajoutées à mesure que les bancs arrivent. Chaque chiffre de ce tableau est une mesure, aucun n'est une estimation.

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

La version Windows a tourné sur des cartes RTX série 30. Les retours sur d'autres cartes sont bienvenus.

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
