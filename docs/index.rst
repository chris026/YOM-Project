.. image:: _static/yom-logo.png
   :alt: YOM logo
   :align: center
   :width: 280px

YOM Bundle Recommender System
=============================

.. rst-class:: lead

    YOM Bundle Recommender is a machine learning system that recommends relevant products to bundle
    with a given anchor product at the point of sale. It consists of two independent recommender
    systems, each built on a two-stage architecture: candidate generation followed by ranking with
    LightGBM.

About the Project
-----------------

The project was developed for a B2B trading environment (kiosk and store systems) to provide
personalized product bundle recommendations based on customer order history.

Both systems share the same two-stage architecture: in the first stage, candidate products are
generated using model-specific methods; in the second stage, a LightGBM ranking model scores
and ranks the candidates using similarity and popularity signals. The key difference lies in the
first stage — one system uses embedding-based similarity (Word2Vec), the other uses
association-based co-purchase patterns (Market Basket Analysis).

Work Completed
--------------

- Model development
   - **Word2Vec Recommender** — embedding-based candidate generation using Gensim Word2Vec;
     products are treated as tokens and orders as sentences, enabling similarity-based retrieval.
     Ranked by a LightGBM model with item similarity and multi-level popularity features.
   - **MBA Recommender** — association-based candidate generation using Market Basket Analysis;
     frequent co-purchase patterns drive candidate selection.
     Ranked by a LightGBM LambdaRank model trained on order history.
- Production deployment
   - Both models are deployed on AWS Lambda via Docker, served through a FastAPI/Mangum adapter.
     The MBA serving layer implements a 4-level fallback strategy (model predictions →
     per-anchor MBA → per-category popular → global popular) to guarantee recommendations
     in all edge cases.
- Results dashboard
   - An interactive dashboard was built to visualize model outputs and recommendation quality,
     with data stored persistently for reuse and comparison.
- A/B-test framework
   - A conceptual design and evaluation theory for a live A/B comparison of both recommender
     systems was prepared to guide future production experiments.

Project Team
------------

- Christian
   - Project Manager
   - Developed the Word2Vec Recommender (embedding model, LightGBM ranker, ZenML pipeline)
   - Built and maintained the results dashboard
   - Designed the A/B-test framework and evaluation methodology
- Diana
   - Data Scientist
   - Drove the research and design of the product bundle recommendation model, including
     exploratory analysis of YOM data, assessment of available approaches, and architecture design aligned with computational
     constraints
   - Developed the MBA Recommender (Market Basket Analysis, LightGBM LambdaRank pipeline,
     fallback logic)
   - Supported the dashboard development and evaluation workflow
- Tizian
   - Responsible for production deployment (AWS Lambda, Docker, CI/CD)

Related Projects
----------------

* `YOM-Word2Vec <https://yom-project.readthedocs.io/projects/Word2Vec/en/latest/>`_ — Embedding-based recommender (Word2Vec + LightGBM)
* `YOM-Bundle-Recommender <https://yom-project.readthedocs.io/projects/bundle-recommender/en/latest/>`_ — Association-based recommender (Market Basket Analysis + LightGBM)

.. toctree::
   :maxdepth: 2
   :caption: Contents
