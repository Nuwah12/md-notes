[Applying interpretable machine learning in computational biology—pitfalls, recommendations and opportunities for new developments](https://www.nature.com/articles/s41592-024-02359-7)

### Interpretable Machine Learning (IML) Methods and Evaluations in computational biology
Two primary IML approaches are used to exlain prediction models in computational biology applications
* *Post-hoc explanations* are flexibile and typically model-agnostic due to their application *after* the design and training of a prediction model
	* *Feature importance* methods are commonly used in comp. bio applications, and assign each input feature an importance value based on its contribution to the model prediction. Importance values can be calculated with *gradient-based* methods or *perturbation-based* methods.
* *By-design methods* are models that are naturally interpretable, for example, a linear model's coefficient weights are able to be interpreted as the importance of each feature, and decision trees are interpretable by examining the splits in the tree.

#### Biologically Informed Networks
Biologically informed networks encode domain knowledge, where, in the context of deep learning, the hidden nodes correspond to biological entities, such as genes and pathways.The relative importance of the entities is often interpreted using a self-defined measure within the network. *Post-hoc* explanations can still be applied to the by-design neural networks.