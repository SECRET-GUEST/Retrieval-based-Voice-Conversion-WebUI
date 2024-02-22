<div align="center">

<h1>Retrieval-based-Voice-Conversion-WebUI</h1>
Un cadre de conversion de voix simple et facile à utiliser basé sur VITS<br><br>

[![madewithlove](https://img.shields.io/badge/made_with-%E2%9D%A4-red?style=for-the-badge&labelColor=orange
)](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI)

<img src="https://counter.seku.su/cmoe?name=rvc&theme=r34" /><br>

[![Open In Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)](https://colab.research.google.com/github/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/Retrieval_based_Voice_Conversion_WebUI.ipynb)
[![Licence](https://img.shields.io/badge/LICENSE-MIT-green.svg?style=for-the-badge)](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/LICENSE)
[![Huggingface](https://img.shields.io/badge/🤗%20-Spaces-yellow.svg?style=for-the-badge)](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/)

[![Discord](https://img.shields.io/badge/RVC%20Developers-Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/HcsmBBGyVk)

[**Journal des mises à jour**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/blob/main/docs/Changelog_CN.md) | [**FAQ**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98%E8%A7%A3%E7%AD%94) | [**Formation de l'IA chanteuse pour 0.5 yuan avec AutoDL**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/Autodl%E8%AE%AD%E7%BB%83RVC%C2%B7AI%E6%AD%8C%E6%89%8B%E6%95%99%E7%A8%8B) | [**Enregistrement d'expériences contrôlées**](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/Autodl%E8%AE%AD%E7%BB%83RVC%C2%B7AI%E6%AD%8C%E6%89%8B%E6%95%99%E7%A8%8B](https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/wiki/%E5%AF%B9%E7%85%A7%E5%AE%9E%E9%AA%8C%C2%B7%E5%AE%9E%E9%AA%8C%E8%AE%B0%E5%BD%95)) | [**Démo en ligne**](https://modelscope.cn/studios/FlowerCry/RVCv2demo)

[**English**](./docs/en/README.en.md) | [**中文简体**](./README.md) | [**日本語**](./docs/jp/README.ja.md) | [**한국어**](./docs/kr/README.ko.md) ([**韓國語**](./docs/kr/README.ko.han.md)) | [**Français**](./docs/fr/README.fr.md)| [**Türkçe**](./docs/tr/README.tr.md)

</div>

> Le modèle de base a été entraîné avec un ensemble de données d'entraînement VCTK open source de près de 50 heures de haute qualité, sans soucis de droits d'auteur, veuillez l'utiliser en toute confiance.

> Attendez-vous au modèle de base RVCv3 avec des paramètres plus grands, plus de données, de meilleurs résultats, une vitesse d'inférence presque équivalente, et nécessitant moins de données d'entraî

nement.

<table>
   <tr>
		<td align="center">Interface d'entraînement et d'inférence</td>
		<td align="center">Interface de conversion vocale en temps réel</td>
	</tr>
  <tr>
		<td align="center"><img src="https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/assets/129054828/092e5c12-0d49-4168-a590-0b0ef6a4f630"></td>
    <td align="center"><img src="https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/assets/129054828/730b4114-8805-44a1-ab1a-04668f3c30a6"></td>
	</tr>
	<tr>
		<td align="center">go-web.bat</td>
		<td align="center">go-realtime-gui.bat</td>
	</tr>
  <tr>
    <td align="center">Vous pouvez librement choisir l'action à exécuter.</td>
		<td align="center">Nous avons réalisé une latence de bout en bout de 170 ms. Avec des appareils d'entrée/sortie ASIO, une latence de bout en bout de 90 ms est réalisable, mais cela dépend beaucoup du support du pilote matériel.</td>
	</tr>
</table>

## Introduction
Ce dépôt a les caractéristiques suivantes :
+ Utilisation du top 1 des recherches pour remplacer les caractéristiques de la source d'entrée par les caractéristiques de l'ensemble d'entraînement pour éviter les fuites de timbre vocal
+ Entraînement rapide même sur des cartes graphiques relativement moins performantes
+ Bon résultats même avec peu de données d'entraînement (au moins 10 minutes de données vocales à faible bruit de fond recommandées)
+ Possibilité de changer le timbre vocal via la fusion de modèles (en utilisant l'option ckpt-merge dans l'onglet de traitement ckpt)
+ Interface web simple et facile à utiliser
+ Utilisation du modèle UVR5 pour une séparation rapide de la voix et de l'accompagnement
+ Utilisation de l'algorithme d'extraction de hauteur vocale de pointe InterSpeech2023-RMVPE pour résoudre le problème de la voix éteinte. Meilleur effet (significativement) mais plus rapide et moins gourmand en ressources que crepe_full
+ Support d'accélération pour les cartes graphiques A et I

Cliquez ici pour voir notre [vidéo de démonstration](https://www.bilibili.com/video/BV1pm4y1z7Gm/) !

## Configuration de l'environnement
Les commandes suivantes doivent être exécutées dans un environnement où la version de Python est supérieure à 3.8.

### Méthodes communes pour Windows/Linux/MacOS
Choisissez l'une des méthodes suivantes.
#### 1. Installer les dépendances via pip
1. Installez Pytorch et ses dépendances principales, sautez cette étape si déjà installé. Référence : https://pytorch.org/get-started/locally/
```bash
pip install torch torchvision torchaudio
```
2. Pour les systèmes Windows + architecture Nvidia Ampere (RTX30xx), spécifiez la version de cuda correspondant à Pytorch selon l'expérience #21
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117
```
3. Installez les dépendances correspondant à votre carte graphique
- Cartes N
```bash
pip install -r requirements.txt
```
- Cartes A/I
```bash
pip install -r requirements-dml.txt
```
- Cartes A ROCM (Linux)
```bash
pip install -r requirements-amd.txt
```
- Cartes I IPEX (Linux)
```bash
pip install -r requirements-ipex.txt
```

#### 2. Installer les dépendances via poetry
Installez le gestionnaire de dépendances Poetry, sautez cette étape si déjà installé. Référence : https://python-poetry.org/docs/#installation
```bash
curl -sSL https://install.python-poetry.org | python3 -
```
Installez les dépendances via poetry
```bash
poetry install
```

### MacOS
Utilisez `

run.sh` pour installer les dépendances
```bash
sh ./run.sh
```

## Préparation d'autres modèles pré-entraînés
RVC nécessite d'autres modèles pré-entraînés pour l'inférence et l'entraînement.

Vous pouvez télécharger ces modèles depuis notre [espace Hugging Face](https://huggingface.co/lj1995/VoiceConversionWebUI/tree/main/).

### 1. Téléchargez les assets
Voici une liste comprenant tous les modèles pré-entraînés et autres fichiers nécessaires pour RVC. Vous pouvez trouver des scripts pour les télécharger dans le dossier `tools`.

- ./assets/hubert/hubert_base.pt

- ./assets/pretrained 

- ./assets/uvr5_weights

Pour utiliser la version v2 du modèle, téléchargez également

- ./assets/pretrained_v2

### 2. Installez ffmpeg
Sautez cette étape si ffmpeg et ffprobe sont déjà installés.

#### Utilisateurs Ubuntu/Debian
```bash
sudo apt install ffmpeg
```
#### Utilisateurs MacOS
```bash
brew install ffmpeg
```
#### Utilisateurs Windows
Téléchargez et placez dans le répertoire racine.
- Téléchargez [ffmpeg.exe](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/ffmpeg.exe)

- Téléchargez [ffprobe.exe](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/ffprobe.exe)

### 3. Téléchargez les fichiers nécessaires pour l'algorithme d'extraction de hauteur vocale RMVPE

Si vous souhaitez utiliser l'algorithme d'extraction de hauteur vocale RMVPE le plus récent, vous devez télécharger les paramètres du modèle d'extraction de hauteur et les placer à la racine de RVC.

- Téléchargez [rmvpe.pt](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/rmvpe.pt)

#### Téléchargez l'environnement dml rmvpe (optionnel, utilisateurs de cartes A/I)

- Téléchargez [rmvpe.onnx](https://huggingface.co/lj1995/VoiceConversionWebUI/blob/main/rmvpe.onnx)

### 4. Cartes graphiques AMD Rocm (optionnel, uniquement pour Linux)

Si vous souhaitez utiliser la technologie Rocm d'AMD pour exécuter RVC sur Linux, installez d'abord les pilotes nécessaires [ici](https://rocm.docs.amd.com/en/latest/deploy/linux/os-native/install.html).

Si vous utilisez Arch Linux, vous pouvez installer les pilotes nécessaires avec pacman :
````
pacman -S rocm-hip-sdk rocm-opencl-sdk
````
Pour certains modèles de cartes graphiques, vous devrez peut-être configurer les variables d'environnement suivantes (par exemple, RX6700XT) :
````
export ROCM_PATH=/opt/rocm
export HSA_OVERRIDE_GFX_VERSION=10.3.0
````
Assurez-vous également que votre utilisateur actuel fait partie des groupes d'utilisateurs `render` et `video` :
````
sudo usermod -aG render $USERNAME
sudo usermod -aG video $USERNAME
````

## Commencer à utiliser
### Démarrage direct
Utilisez la commande suivante pour lancer le WebUI
```bash
python infer-web.py
```
### Utiliser le package intégré
Téléchargez et décompressez `RVC-beta.7z`
#### Utilisateurs Windows
Double-cliquez sur `go-web.bat`
#### Utilisateurs MacOS
```bash
sh ./run.sh
```
### Pour les utilisateurs de cartes I nécessitant la technologie IPEX (uniquement Linux)
```bash
source /opt/intel/oneapi/setvars.sh
```

## Projets de référence
+ [ContentVec](https://github.com/auspicious3000/contentvec/)
+ [VITS](https://github.com/jaywalnut310/vits)
+ [HIFIGAN](https://github.com/jik876/hifi-gan)
+ [Gradio](https://github.com/gradio-app/gradio)
+ [FFmpeg](https://github.com/FFmpeg/FFmpeg)
+ [Ultimate Vocal Remover](https://github.com/Anjok07/ultimatevocalremovergui)
+ [audio-slicer](https://github.com/openvpi/audio-slicer)
+ [Extraction de hauteur vocale : RMVPE](https://

github.com/Dream-High/RMVPE)
  + Le modèle pré-entraîné a été entraîné et testé par [yxlllc](https://github.com/yxlllc/RMVPE) et [RVC-Boss](https://github.com/RVC-Boss).

## Remerciements à tous les contributeurs pour leurs efforts
<a href="https://github.com/RVC-Project/Retrieval-based-Voice-Conversion-WebUI/graphs/contributors" target="_blank">
  <img src="https://contrib.rocks/image?repo=RVC-Project/Retrieval-based-Voice-Conversion-WebUI" />
</a>
