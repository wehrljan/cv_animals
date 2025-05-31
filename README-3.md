# vit-90-animals
## Project Description
This project involves training a Vision Transformer (ViT) model to classify images into 90 different animal species. The model was fine-tuned on a labeled dataset and achieves high accuracy on unseen test data. In addition to training our own model, we evaluate its performance by comparing it to a zero-shot image classification model (CLIP), which predicts labels without prior training on the dataset.

## Artefacts
| Name | URL |
|-|-|
| Huggingface | [Huggingface Space](https://huggingface.co/spaces/maceythm/vit-90-animals) |
| Model Page | [Huggingface Model Page](https://huggingface.co/maceythm/vit-90-animals) |
| Code | [GitHub](https://github.com/maceythm/vit-90-animals) |

## Labels
The model can distinguish between the following 90 animal species:
|          |          |              |             |          |
|----------|----------|--------------|-------------|----------|
| antelope | dog         | hippopotamus | orangutan | seahorse |
| badger   | dolphin     | hornbill     | otter     | seal     |
| bat      | donkey      | horse        | owl       | shark    |
| bear     | dragonfly   | hummingbird  | ox        | sheep    |
| bee      | duck        | hyena        | oyster    | snake    |
| beetle   | eagle       | jellyfish    | panda     | sparrow  |
| bison    | elephant    | kangaroo     | parrot    | squid    |
| boar     | flamingo    | koala        | pelecaniformes | squirrel |
| butterfly| fly         | ladybugs     | penguin   | starfish |
| cat      | fox         | leopard      | pig       | swan     |
| caterpillar | goat     | lion         | pigeon    | tiger    |
| chimpanzee | goldfish  | lizard       | porcupine | turkey   |
| cockroach | goose      | lobster      | possum    | turtle   |
| cow      | gorilla     | mosquito     | raccoon   | whale    |
| coyote   | grasshopper | moth         | rat       | wolf     |
| crab     | hamster     | mouse        | reindeer  | wombat   |
| crow     | hare        | octopus      | rhinoceros| woodpecker |
| deer     | hedgehog    | okapi        | sandpiper | zebra    |

## Data Sources
| Data Source | Description | Features |
|-|-|-|
| [Kaggle - Animal Image Dataset](https://www.kaggle.com/datasets/iamsouravbanerjee/animal-image-dataset-90-different-animals) | The dataset was obtained from Kaggle and contains 5,400 images of animals across 90 different species. According to the dataset creator, the images originally come from Google. The data is already well-structured on Kaggle, which is a major advantage for our project. | - **image**: the image stored in PIL format<br> - **label**: the ID of a folder in the dataset. the folder ist named with the species of the animal and contains corresponding images.|

## Model Training
### Data Augmentation
Data augmentation is used to artificially increase the diversity of the training dataset by applying random transformations to the input images. This helps improve the model's robustness and generalization to unseen data.

| Augmentation             | Description                                                                                   |
|--------------------------|-----------------------------------------------------------------------------------------------|
| RandomHorizontalFlip()   | Randomly flips the image horizontally with a probability of 0.5.                              |
| RandomRotation(30)       | Rotates the image randomly within a range of ±30 degrees.                                     |
| ColorJitter(brightness=0.2, contrast=0.2, saturation=0.2, hue=0.2) | Randomly adjusts brightness, contrast, saturation, and hue by up to ±20%. |

### Data Splitting Method (Train/Validation/Test)
A total of 5400 images of 90 animal species were used for training, validation and testing - split as follows:
| Split      | Number of Samples | Percentage |
|------------|-------------------|------------|
| Train      | 4'320             | 80 %       |
| Validation | 540               | 10 %       |
| Test       | 540               | 10 %       |

### TensorBoard
Details of training can be found on [Huggingface TensorBoard](https://huggingface.co/maceythm/vit-90-animals/tensorboard)
| Model/Method | TensorBoard Link |
|-|-|
| Transfer Learning with `google/vit-base-patch16-224` (without data augmentation) | runs/May17_10-24-11_cs-01jvew10vftebgspfnespgcr4r |
| Transfer Learning with `google/vit-base-patch16-224` (with data augmentation) | runs/May17_14-37-53_cs-01jvf84h4q9vae662f2w6rkkkt |

![Model Accuracy](./doc/accuracy_1and3.png)

Too much or the wrong data augmentation methods can lead to bad model performance, as shown in the following run:
| Model/Method | TensorBoard Link |
|-|-|
| Transfer Learning with `google/vit-base-patch16-224` (with data augmentation) | runs/May17_13-54-12_cs-01jvf84h4q9vae662f2w6rkkkt |

![Model Accuracy](./doc/accuracy_2.png)

I will not go into that run any further in this documentation.

## Results (ViT and CLIP)
| Model/Method | Accuracy | Precision | Recall |
|-|-|-|-|
| Transfer Learning with `google/vit-base-patch16-224` (without data augmentation) | 98.3% | - | - |
| Transfer Learning with `google/vit-base-patch16-224` (with data augmentation) | 97.9% | - | - |
| Zero-shot Image Classification with `openai/clip-vit-large-patch14` | 96.3% | 97.1% | 96.3% |

### Conclusion
The fine-tuned ViT model based on `google/vit-base-patch16-224` achieves the highest classification accuracy at 98.3% without data augmentation. Data augmentation led to a slight performance decrease (97.9%), likely due to the increased variability in training samples. The zero-shot CLIP model (`openai/clip-vit-large-patch14`) performs remarkably well with 96.3% accuracy, despite not being specifically trained on the dataset. This highlights the strength of pretrained multi-modal models, although fine-tuning still offers the best results in this task.

## References
![Label Distribution](./doc/label_distribution.png)
![Label Distribution](./doc/sample_prediction_transferlearning.png)
