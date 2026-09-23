# CHIME: Causal Human-in-the-Loop Model Explanations

Research code for constructing causal model explanations from human annotations. The repository includes an annotation interface, data processing notebooks, and evaluation code.

**Paper:** Shreyan Biswas, Lorenzo Corti, Stefan Buijsman, and Jie Yang. [CHIME: Causal Human-in-the-Loop Model Explanations](https://doi.org/10.1609/hcomp.v10i1.21985). HCOMP 2022, pp. 27–39.

## Where to start

| Directory | Contents |
| --- | --- |
| [`data_collection_app/`](data_collection_app/) | Angular annotation interface and Django API |
| [`data_processing/`](data_processing/) | Annotation preprocessing and graph construction |
| [`demo/`](demo/) | Mediation and confounder notebooks |
| [`evaluation/`](evaluation/) | Coherence, causal verification, and results analysis |
| [`utils/`](utils/) | Model training, predictions, and saliency generation |
| [`data/`](data/) | Data files and data guidance |

The notebooks expose the research workflow. The web application is the tool used to collect annotations; running it alone does not reproduce the paper's results.

## Run the annotation application locally

The application uses the original Angular 13 and Django 3.2 dependency sets. Treat this as a historical research environment. A migration to current framework versions still needs application and study-flow validation.

From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r data_collection_app/services/requirements.txt
cd data_collection_app/services
python manage.py migrate
python manage.py runserver 127.0.0.1:8000
```

In a second terminal:

```bash
cd data_collection_app/AnnotationScreen
npm ci
npm start
```

Open `http://localhost:4200`. The development frontend points to `http://localhost:8000`. The annotation workflow also needs image and task records in the database.

Backend configuration is read from `DJANGO_SECRET_KEY`, `DJANGO_DEBUG`, `DJANGO_ALLOWED_HOSTS`, and `DJANGO_CORS_ORIGINS`. By default, debug mode is off and only local hosts and the local frontend origin are allowed. Set a persistent secret key outside source control for any shared instance; without one, a temporary key is generated on process startup.

## Reproducing the research

Start with the paper and inspect the input paths in each notebook before execution. Model weights, image collections, and external services are not installed by the application setup above. The original notebooks and saved outputs are retained as research artifacts; they are not a claim that the full pipeline has been rerun on current dependencies.

## Citation

```bibtex
@inproceedings{biswas2022chime,
  title={CHIME: Causal Human-in-the-Loop Model Explanations},
  author={Biswas, Shreyan and Corti, Lorenzo and Buijsman, Stefan and Yang, Jie},
  booktitle={Proceedings of the AAAI Conference on Human Computation and Crowdsourcing},
  volume={10},
  number={1},
  pages={27--39},
  year={2022},
  doi={10.1609/hcomp.v10i1.21985}
}
```
