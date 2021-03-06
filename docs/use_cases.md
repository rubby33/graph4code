## Example Use Cases<a name="uses"></a>

### Recommendation engine for developers<a name="case1"></a>
CodeBreaker is a coding assistant built on top of Graph4Code to help data scientists write code.  The coding assistant helps users find the most plausible next coding step, finds relevant stack overflow posts based purely on the users' code, and allows users to see what sorts of models other people have constructed for data flows similar to their own.  CodeBreaker uses the Language Server Protocol (LSP) to provide integration with any IDE.  For a detailed description of this use case, see the [demo paper](https://github.com/wala/graph4code/blob/master/papers/CodeBreaker_SigDemo.pdf). A video of this use case is also [here](https://github.com/wala/graph4code/blob/master/docs/figures/demo_v2.mp4).

### Enforcing best practices<a name="case2"></a>
Many best practices for API frameworks can be encoded into query templates over data flow and control flow.  Here we give three such examples for data science code, along with queries which can be templatized.
  
  * Check that users developing data science code create multiple models on the same dataset, since machine learning algorithms vary greatly in terms of performance on different datasets ([see query here](https://github.com/wala/graph4code/blob/master/usage_queries/ensure_multiple_models.sparql)).  Here is an example result from the query.  As shown in the example, only one model is used to train ona  given dataset.

<a name="Example violation of best practice to create multiple models"></a>

<p align="center">
<img align="center" src="figures//ensure_multiple_models.png" width="90%"/>
</p>
<br><br>

  * Check that the users use some sort of libraries for hyper-parameter optimization when building their models ([see query here](https://github.com/wala/graph4code/blob/master/usage_queries/must_not_set_hyperparameters.sparql)).  Here is an example result from the query - the analysis found all three examples of manual sets to hyperparameters.

<a name="Example violation of best practice to not set hyper-parameters manually"></a>

<p align="center">
<img align="center" src="figures//must_not_set_hyperparameters.png" width="90%"/>
</p>
<br><br>

  * Check that users developing data science code create the model with a different dataset than the ones they use to validate the model ([see query here](https://github.com/wala/graph4code/blob/master/usage_queries/train_test_different_data.sparql)).

<a name="Example violation of best practice to use different datasets to train"></a>

<p align="center">
<img align="center" src="figures//train_test_different_data.png" width="90%"/>
</p>
<br><br>

### Learning from big code<a name="case3"></a> 

There has been an explosion of work on mining large open domain repositories for a wide variety of tasks (see [here](https://ml4code.github.io/papers.html)).  We sketch a couple of examples for how Graph4Code can be used in this context.
  * As an example, again, from a data science use case, the arguments flowing into constructors of models govern the behavior of a model to a large extent.   These so-called hyperparameters are often optimized by some sort of search technique over the space of parameters.  Hyperparameter optimization can be seeded with the appropriate values using query here to restrict search, using any of the standard hyper parameter optimization packages ([see query here](https://github.com/wala/graph4code/blob/master/usage_queries/find_hyperparameter_distributions.sparql)).

<a name="Example hyperparameter distributions"></a>

<p align="center">
<img align="center" src="figures//hyperparameter_distributions.png" width="90%"/>
</p>
<br><br>

  * The graphs themselves can be used to perform automated code generation by using them as training sets.  As an example, [Code2seq](https://arxiv.org/pdf/1808.01400.pdf) is a system that generates natural language statements about code (e.g. predicting Java method names) or code captioning (summarizing code snippets).  Code2seq is based on an AST representation of code.  Graph4Code can be used to generate richer representations which may be better suited to generate code captioning.
