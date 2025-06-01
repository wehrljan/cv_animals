# Computer Vision Animals
## Projektbeschreibung
Dieses Projekt beschäftigt sich mit der Klassifikation von Bildern in 90 verschiedene Tierklassen. Ziel ist es, zwei unterschiedliche Ansätze zu vergleichen:
- Transfer Learning mit einem vortrainierten Vision Transformer (ViT) Modell, das auf das eigene Datenset feinabgestimmt wurde.
- Zero-Shot Learning mit dem OpenAI CLIP Modell, welches in der Lage ist, ohne direktes Training auf dem Datensatz Klassifikationen durchzuführen.

Datensatz (Ordner "animals") war zu gross für github und musste auf SwitchDrive hochgeladen werden:
https://drive.switch.ch/index.php/s/dnrrhuMHJppOHMq

## Name & URL
| Name | URL |
|-|-|
| Huggingface | [Huggingface Space](https://huggingface.co/spaces/Dalmatiner/cv_animals) |
| Model Page | [Huggingface Model Page](https://huggingface.co/Dalmatiner/cv_animals) |
| Code | [GitHub](https://github.com/wehrljan/cv_animals) |

## Labels
Das Model kann die folgenden 90 Tierarten unterscheiden und klassifizieren: 

['antelope', 'badger', 'bat', 'bear', 'bee', 'beetle', 'bison', 'boar', 'butterfly', 'cat', 'caterpillar', 'chimpanzee', 'cockroach', 'cow', 'coyote', 'crab', 'crow', 'deer', 'dog', 'dolphin', 'donkey', 'dragonfly', 'duck', 'eagle', 'elephant', 'flamingo', 'fly', 'fox', 'goat', 'goldfish', 'goose', 'gorilla', 'grasshopper', 'hamster', 'hare', 'hedgehog', 'hippopotamus', 'hornbill', 'horse', 'hummingbird', 'hyena', 'jellyfish', 'kangaroo', 'koala', 'ladybugs', 'leopard', 'lion', 'lizard', 'lobster', 'mosquito', 'moth', 'mouse', 'octopus', 'okapi', 'orangutan', 'otter', 'owl', 'ox', 'oyster', 'panda', 'parrot', 'pelecaniformes', 'penguin', 'pig', 'pigeon', 'porcupine', 'possum', 'raccoon', 'rat', 'reindeer', 'rhinoceros', 'sandpiper', 'seahorse', 'seal', 'shark', 'sheep', 'snake', 'sparrow', 'squid', 'squirrel', 'starfish', 'swan', 'tiger', 'turkey', 'turtle', 'whale', 'wolf', 'wombat', 'woodpecker', 'zebra']


## Datenquellen
| Datenquelle | Beschreibung |
|-|-|
| [Kaggle - Animal Image Dataset](https://www.kaggle.com/datasets/iamsouravbanerjee/animal-image-dataset-90-different-animals) | Der Datensatz stammt von Kaggle und enthält 5’400 Tierbilder aus 90 verschiedenen Arten, die von Google stammen. Der Datensatz ist auf Kaggle bereits gut strukturiert indem es pro Tierart einen Ordner gibt. Die Daten wurde auch hier auf SwitchDrive hochgeladen: https://drive.switch.ch/index.php/s/dnrrhuMHJppOHMq 
 | Weitere Testdaten | Es wurden weitere 5 Tierbilder von Google heruntergeladen und manuell gelabelt. Davon sind einige Tierarten nicht trainiert worden.
 
### Data Augmentation

| Augmentation             | Beschreibung                                                                                  |
|--------------------------|-----------------------------------------------------------------------------------------------|
| RandomHorizontalFlip()   | Spiegelt das Bild mit einer Wahrscheinlichkeit von 50 % horizontal.                             |
| RandomRotation(25)       | Rotiert das Bild zufällig um bis zu ±25 Grad.                                   |
| ColorJitter(brightness=0.2, contrast=0.2, saturation=0.2, hue=0.2) | Verändert Helligkeit, Kontrast, Sättigung und Farbton zufällig um bis zu ±20 %.. |

## Model Training

### Data Splitting Methode - Train/Validation/Test
Es wurden insgesamt 90 Tierkategorien mit 5400 Bilder als Daten für Training, VAlidierung und Testing genutzt. Aufgeteilt wurden sie wie folgt: 

80% für Training, 10% für Validation und 10% für Test

| Split      | Anzahl Daten |
|------------|-------------------|
| Train      | 4'320             |
| Validation | 540               |
| Test       | 540               |


### Training

| Epoch | Training Loss | Validation Loss | Accuracy |
|-|-|-|-|
|	1.0	| 1.1803	| 0.3215	| 0.9630
|	2.0 |	0.2779	| 0.1634	| 0.9648
|	3.0	| 0.1745	| 0.1407	| 0.9648
|	4.0	| 0.1608	| 0.1322	| 0.9630
|	5.0	| 0.1486	| 0.1281	| 0.9648

### TensorBoard
Details of training can be found on [Huggingface TensorBoard](https://huggingface.co/Dalmatiner/cv_animals/tensorboard)
| Model/Method | TensorBoard Link |
|-|-|
| Transfer Learning mit `google/vit-base-patch16-224` (ohne data augmentation) | runs/May29_20-53-28_ip-10-192-12-231 |
| Transfer Learning mit `google/vit-base-patch16-224` (mit data augmentation) | runs/May31_22-34-33_ip-10-192-12-38 |

<img width="858" alt="eval_accuracy" src="https://github.com/user-attachments/assets/0ddd7673-f0b5-45e1-b701-0a598e62fcaf" />


## Resultate aus Transfer Learning und CLIP
| Model/Methode | Accuracy | Precision | Recall |
|-|-|-|-|
| Transfer Learning with `google/vit-base-patch16-224` (ohne data augmentation) | 97.2% | - | - |
| Transfer Learning with `google/vit-base-patch16-224` (mit data augmentation) | 98.7% | - | - |
| Zero-shot Image Classification with `openai/clip-vit-large-patch14` | 96.3% | 97.1% | 96.3% |


## Referenzen
![Label_distribution](https://github.com/user-attachments/assets/69c22c0f-43e0-442c-91cf-a9eb8ad4ff8f)

![predicted_labels](https://github.com/user-attachments/assets/caa6618e-0ded-4a47-bf0f-2ea2c32eeb75)



