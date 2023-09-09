<div align="center">

<h1>Retrieval-based-Voice-Conversion-WebUI</h1>
Un framework simple et facile à utiliser pour la conversion vocale (modificateur de voix) basé sur VITS<br><br>

[![madewithlove](https://img.shields.io/badge/made_with-%E2%9D%A4-red?style=for-the-badge&labelColor=orange
)](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI)

<img src="https://counter.seku.su/cmoe?name=rvc&theme=r34" /><br>

[![Open In Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/github/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/Retrieval_based_Voice_Conversion_WebUI.ipynb)
[![Licence](https://img.shields.io/badge/LICENSE-MIT-green.svg?style=for-the-badge)](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/LICENSE)
[![Huggingface](https://img.shields.io/badge/🤗%20-Spaces-yellow.svg?style=for-the-badge)](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/)

[![Discord](https://img.shields.io/badge/RVC%20Developers-Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/HcsmBBGyVk)

[**Journal de mise à jour**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/docs/Changelog_CN.md) | [**FAQ**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E8%A7%A3%E7%AD%94) | [**AutoDL·Formation d'un chanteur AI pour 5 centimes**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/Autodl%E8%AE%AD%E7%BB%83RVC%C2%B7AI%E6%AD%8C%E6%89%8B%E6%95%99%E7%A8%8B) | [**Enregistrement des expériences comparatives**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5%AF%B9%E7%85%A7%E5%AE%9E%E9%AA%8C%C2%B7%E5%AE%9E%E9%AA%8C%E8%AE%B0%E5%BD%95)) | [**Démonstration en ligne**](https://huggingface.co/spaces/Ricecake123/RVC-demo)

</div>

------

[**English**](./docs/en/README.en.md) |[ **中文简体**](./docs/cn/README.md) | [**日本語**](./docs/jp/README.ja.md) | [**한국어**](./docs/kr/README.ko.md) ([**韓國語**](./docs/kr/README.ko.han.md)) | [**Turc**](./docs/tr/README.tr.md) 

Cliquez ici pour voir notre [vidéo de démonstration](https://www.bilibili.com/video/BV1pm4y1z7Gm/) !

> Conversion vocale en temps réel avec RVC : [w-okada/voice-changer](https://github.com/w-okada/voice-changer)

> Le modèle de base est formé avec près de 50 heures de données VCTK de haute qualité et open source. Aucun souci concernant les droits d'auteur, n'hésitez pas à l'utiliser.

> Attendez-vous au modèle de base RVCv3 : plus de paramètres, plus de données, de meilleurs résultats, une vitesse d'inférence presque identique, et nécessite moins de données pour la formation.

## Introduction
Ce dépôt a les caractéristiques suivantes :
+ Utilise le top1 pour remplacer les caractéristiques de la source d'entrée par les caractéristiques de l'ensemble d'entraînement pour éliminer les fuites de timbre vocal.
+ Peut être formé rapidement même sur une carte graphique relativement moins performante.
+ Obtient de bons résultats même avec peu de données pour la formation (il est recommandé de collecter au moins 10 minutes de données vocales avec un faible bruit de fond).
+ Peut changer le timbre vocal en fusionnant des modèles (avec l'aide de l'onglet ckpt-merge).
+ Interface web simple et facile à utiliser.
+ Peut appeler le modèle UVR5 pour séparer rapidement la voix et l'accompagnement.
+ Utilise l'algorithme de pitch vocal le plus avancé [InterSpeech2023-RMVPE](#projets-référencés) pour éliminer les problèmes de voix muette. Meilleurs résultats, plus rapide que crepe_full, et moins gourmand en ressources.
+ Support d'accélération pour les cartes A et I.

## Configuration de l'environnement
Exécutez les commandes suivantes dans un environnement Python de version supérieure à 3.8.

(Windows/Linux)  
Installez d'abord les dépendances principales via pip :
```bash
# Installez Pytorch et ses dépendances essentielles, sautez si déjà installé.
# Voir : https://pytorch.org/get-started/locally/
pip install torch torchvision torchaudio

# Pour les utilisateurs de Windows avec une architecture Nvidia Ampere (RTX30xx), en se basant sur l'expérience #21, spécifiez la version CUDA correspondante pour Pytorch.
# pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117
```

Vous pouvez utiliser poetry pour installer les dépendances :
```bash
# Installez l'outil de gestion des dépendances Poetry, sautez si déjà installé.
# Voir : https://python-poetry.org/docs/#installation
curl -sSL https://install.python-poetry.org | python3 -

# Installez les dépendances avec poetry.
poetry install
```

Ou vous pouvez utiliser pip pour installer les dépendances :
```bash
Cartes Nvidia :

pip install -r requirements.txt

Cartes AMD/Intel :
pip install -

r requirements-dml.txt

```

------
Les utilisateurs de Mac peuvent exécuter `run.sh` pour installer les dépendances :
```bash
sh ./run.sh
```

## Préparation d'autres modèles pré-entraînés
RVC nécessite d'autres modèles pré-entraînés pour l'inférence et la formation.

Vous pouvez télécharger ces modèles depuis notre [espace Hugging Face](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/).

Voici une liste des modèles et autres fichiers requis par RVC :
```
./assets/hubert/hubert_base.pt

./assets/pretrained 

./assets/uvr5_weights

```

Pour tester la version v2 du modèle, téléchargez également :

```
./assets/pretrained_v2

```

Si vous utilisez Windows, vous pourriez avoir besoin de ces fichiers pour ffmpeg et ffprobe, sautez cette étape si vous avez déjà installé ffmpeg et ffprobe. 

Les utilisateurs d'ubuntu/debian peuvent installer ces deux bibliothèques avec apt install ffmpeg. Les utilisateurs de Mac peuvent les installer avec brew install ffmpeg (prérequis : avoir installé brew).


FFMPEG:
	https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/ffmpeg.exe

FFPROBE:
	https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/ffprobe.exe


Si vous souhaitez utiliser le dernier algorithme RMVPE de pitch vocal, téléchargez les paramètres du modèle de pitch et placez-les dans le répertoire racine de RVC.

	https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/rmvpe.pt

    Les utilisateurs de cartes AMD/Intel nécessitant l'environnement DML doivent télécharger :


    https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/rmvpe.onnx
    
Ensuite, exécutez la commande suivante pour démarrer WebUI :
```
python infer-web.py
```

Si vous utilisez Windows ou macOS, vous pouvez télécharger et extraire `RVC-beta.7z`. Les utilisateurs de Windows peuvent exécuter `go-web.bat` pour démarrer WebUI, tandis que les utilisateurs de macOS peuvent exécuter `sh ./run.sh`.

Il y a également un `Guide facile pour les débutants.doc` inclus pour référence.


## Lancer via ligne de commande

Le fichier commander.py sert à lancer les anciens et nouveaux models en ligne de commandes, voici comment faire : 

Pour lancer les premiers modèles : 

```
runtime\python.exe commander.py 0 "C:\ YOUR PATH FOR THE ROOT \INPUTS_VOCAL\vocal.wav" "C:\ YOUR PATH FOR THE ROOT \logs\MODEL_v1.index" harvest "test_v1.wav" "C:\ YOUR PATH FOR THE ROOT \weights\MODEL_V1.pth" 0.66 cuda:0 True 3 0 1 0.33
```

Les nouveaux modèles :
```
 runtime\python.exe commander.py 0 "C:\ YOUR PATH FOR THE ROOT \INPUTS_VOCAL\vocal.wav" "C:\ YOUR PATH FOR THE ROOT \logs\MODEL_v2.index" harvest "test_v2.wav" "C:\ YOUR PATH FOR THE ROOT \weights\MODEL.pth" 0.6 cuda:0 True 5 True 3 0 2 0.33
```

### Explication des arguments :

Pour utiliser ce script via la ligne de commande, vous devez spécifier un certain nombre d'arguments. Voici la structure de la commande et une explication de chaque argument :

```
runtime\python.exe votre_script.py [f0up_key] [input_path] [index_path] [f0method] [opt_path] [model_path] [index_rate] [device] [is_half] [filter_radius] [resample_sr] [rms_mix_rate] [protect]
```

### Explication des arguments :

1. `python commander.py`: Cette commande sert à exécuter votre script Python.

2. `f0up_key` : Une clé pour spécifier la mise à jour de la fréquence fondamentale (F0). (ex : 0)

3. `input_path` : Le chemin du fichier audio d'entrée que vous voulez traiter. (ex : "C:\Chemin\vers\le\fichier\vocal.wav")

4. `index_path` : Le chemin du fichier index qui stocke ou récupère des informations supplémentaires pour le traitement. (ex : "C:\Chemin\vers\le\fichier\index.log")

5. `f0method` : La méthode utilisée pour extraire le pitch (F0) du fichier audio. Les options possibles sont "harvest" ou "pm". (ex : "harvest")

6. `opt_path` : Le chemin où le fichier audio traité sera sauvegardé. (ex : "C:\Chemin\vers\le\fichier\sortie.wav")

7. `model_path` : Le chemin vers le fichier modèle qui sera utilisé pour le traitement. (ex : "C:\Chemin\vers\le\modèle\model.pth")

8. `index_rate` : Le taux d'index utilisé pendant le traitement. Ce doit être une valeur de type float. (ex : 0.6)

9. `device` : Le périphérique sur lequel le traitement sera effectué. Les options possibles sont les identifiants des GPU (comme "cuda:0") ou "cpu". (ex : "cuda:0")

10. `is_half` : Un booléen indiquant si le modèle doit utiliser une précision mixte pendant le traitement. Les options possibles sont True ou False. (ex : True)

11. `filter_radius` : La taille du rayon du filtre, une valeur de type int. (ex : 5)

12. `resample_sr` : Le taux d'échantillonnage pour le rééchantillonnage, une valeur de type int. (ex : 44100)

13. `rms_mix_rate` : Un taux utilisé pour ajuster le mixage RMS pendant le traitement, une valeur de type float. (ex : 0.5)

14. `protect` : Une valeur utilisée pour ajuster un paramètre de protection pendant le traitement, une valeur de type float. (ex : 0.33)

### Exemple d'utilisation :

```
python commander.py 0 "C:\Chemin\vers\le\fichier\vocal.wav" "C:\Chemin\vers\le\fichier\logs\MODEL_v2.index" harvest "C:\Chemin\vers\le\fichier\sortie.wav" "C:\Chemin\vers\le\modèle\model.pth" 0.6 cuda:0 True 5 44100 0.5 0.33
```


## Crédits
+ [ContentVec](https://github.com/auspicious3000/contentvec/)
+ [VITS](https://github.com/jaywalnut310/vits)
+ [HIFIGAN](https://github.com/jik876/hifi-gan)
+ [Gradio](https://github.com/gradio-app/gradio)
+ [FFmpeg](https://github.com/FFmpeg/FFmpeg)
+ [Ultimate Vocal Remover](https://github.com/Anjok07/ultimatevocalremovergui)
+ [audio-slicer](https://github.com/openvpi/audio-slicer)
+ [Extraction de la hauteur vocale : RMVPE](https://github.com/Dream-High/RMVPE)
  + Le modèle pré-entraîné a été formé et testé par [yxlllc](https://github.com/yxlllc/RMVPE) et [RVC-Boss](https://github.com/RVC-Boss).

## Remerciements à tous les contributeurs pour leurs efforts
<a href="https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/graphs/contributors" target="_blank">
  <img src="https://contrib.rocks/image?repo=RVC-Project/Retrieval-based-Voice-Conversion-WebUI" />
</a>
