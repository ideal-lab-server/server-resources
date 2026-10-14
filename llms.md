#  IIT Kanpur IDEAL Lab Server                     

## Pretrained and Fine-Tuned LLM Storage Guide

### 1. Pretrained LLMs
---

Pretrained LLMs are stored centrally on the server under:

```
/data/shared/models/llms/
```

For example:

```
/data/shared/models/llms/
├── Qwen3-8B-Base/
└── Qwen3-8B/
```

These directories contain the original pretrained model parameters and associated model files downloaded from the model provider. Do not modify, overwrite, delete, or replace files inside `/data/shared/models/llms/`. These models are maintained as shared reference copies so that 
multiple researchers can use the same pretrained models and obtain reproducible results. You can load these models directly from their locations in your Python programs.

---
### 2. Fine-Tuned and Modified Models
---

Fine-tuning changes the model parameters, either by updating the original model parameters or by creating additional trainable parameters such as LoRA adapters. Do not save modified parameters back into `/data/shared/models/llms/`. Instead, save the results of your experiments in a location appropriate for your intended use. 

---
#### 2.1. Shared Storage 
---

If you want to share the results with other members of the `researchers` group, use a project-specific directory under:

```
/data/shared/projects/
```

For example:

```
/data/shared/projects/my-llm-project/
├── scripts/
├── data/
├── checkpoints/
└── models/
```

A fine-tuned model or LoRA adapter can therefore be stored under:

```
/data/shared/projects/my-llm-project/models/
```
---
#### 2.2. Private Storage
---

If you want to keep the results private, store them in your home directory `~`. For example:

```
~/llm-project/
├── scripts/
├── checkpoints/
└── models/
```

Alternatively, you can also privately store your models under `/data/users/username`. For example:

```
/data/users/username/llm-project/
├── scripts/
├── checkpoints/
└── models/
```

Note that your home directory `~` is stored in a `1.8T NVMe` while `/data` is stored in a `4T HDD`. Therefore, use `~` to privately store active projects that require fast access, and use `/data/users/username` to privately archive old projects that do not require fast access.

---
### 3. Summary
---

| Directory                     | Intended Use                                | Storage     |
| ----------------------------- | ------------------------------------------- | ----------- |
| `/data/shared/models`         | Pretrained Models                           | `4T HDD`    |
| `/data/shared/projects`       | Fine-tuned Shared Models                    | `4T HDD`    |
| `~`                           | Fine-tuned Private Models (Active Projects) | `1.8T NVMe` |
| `/data/shared/users/username` | Fine-tuned Private Models (Archived)        | `4T HDD`    |
