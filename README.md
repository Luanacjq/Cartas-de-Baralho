# Detecção de Cartas de Baralho com YOLOv8

**Disciplina:** Ciência de Dados — Deep Learning  
**Modelo:** YOLOv8n (Ultralytics)  
**Dataset:** [Playing Cards — Roboflow Universe (Augmented Startups)](https://universe.roboflow.com/augmented-startups/playing-cards-ow27d)  
**Repositório:** https://github.com/Luanacjq/Cartas-de-Baralho.git

---

## Descrição do Projeto

Este projeto treina um modelo **YOLOv8** para detectar e classificar as **52 cartas de um baralho** em imagens, utilizando a biblioteca Ultralytics e um dataset sintético publicamente disponível no Roboflow Universe.

Cada classe corresponde a uma carta específica — por exemplo: `AS` (Ás de Espadas), `KH` (Rei de Copas), `10C` (10 de Paus).

**Classe inédita:** nenhuma das 52 classes do dataset faz parte das 80 categorias padrão do COCO usadas no YOLO pré-treinado, tornando esta uma tarefa de detecção completamente nova para o modelo.

---

## Resultados Obtidos

| Métrica | Valor |
|---|---|
| Precision | **0.9514** |
| Recall | **0.9376** |
| mAP@0.5 | **0.9837** |
| mAP@0.5:0.95 | **0.7581** |

> Avaliação realizada no conjunto de teste com 1.010 imagens e 4.040 instâncias anotadas.

---

## Dataset

| Propriedade | Valor |
|---|---|
| Origem | Roboflow Universe — Augmented Startups |
| Total de imagens | ~24.233 (sintéticas) |
| Treino | 21.203 imagens |
| Validação | 2.020 imagens |
| Teste | 1.010 imagens |
| Classes | 52 (uma por carta do baralho) |
| Formato | YOLOv8 (bounding boxes YOLO) |

---

## Como Executar

### Pré-requisitos

- Python 3.9+
- Jupyter Notebook ou VS Code com extensão Jupyter

### Instalação

```bash
pip install ultralytics roboflow
```

### Execução

1. Clone o repositório:
   ```bash
   git clone https://github.com/Luanacjq/YOLO-Cartas-de-Baralho.git
   cd YOLO-Cartas-de-Baralho
   ```

2. Abra o notebook `Deteccao_Cartas_Baralho_YOLO.ipynb` no VS Code ou Jupyter.

3. Execute as células em ordem. O dataset é baixado automaticamente via Roboflow API na primeira execução.

---

## Estrutura do Repositório

```
YOLO-Cartas-de-Baralho/
├── Deteccao_Cartas_Baralho_YOLO.ipynb   # Notebook principal com todo o código
├── Relatorio_Tecnico.pdf                 # Relatório técnico do projeto
├── baralho.png                           # Foto real capturada pelo grupo
├── baralho2.png                          # Segunda foto real capturada pelo grupo
├── predicao_teste/                       # Predições do modelo no conjunto de teste
│   ├── image0.jpg
│   ├── image1.jpg
│   ├── image2.jpg
│   └── image3.jpg
├── dataset/                              # Gerado automaticamente na execução
├── runs/                                 # Gerado automaticamente na execução
└── README.md
```

---

## Hiperparâmetros de Treinamento

| Parâmetro | Valor (CPU) | Valor (GPU) | Justificativa |
|---|---|---|---|
| `epochs` | 20 | 50 | Equilíbrio entre convergência e tempo |
| `imgsz` | 320 | 640 | 320px é 4× mais rápido no CPU |
| `batch` | 16 | 32 | Batch maior compensa imagens menores |
| `fraction` | 0.3 | 1.0 | ~6.300 imagens suficientes em CPU |
| `lr0` | 0.01 | 0.01 | Taxa de aprendizado padrão |
| `optimizer` | SGD | SGD | Robusto para detecção de objetos |
| `patience` | 10 | 15 | Early stopping contra overfitting |

---

## Tecnologias

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics)
- [Roboflow](https://roboflow.com/)
- Python 3.13 · PyTorch · Matplotlib · Pillow
