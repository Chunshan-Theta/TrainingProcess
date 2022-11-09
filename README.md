# TrainingProcess

``` python
  ### () => ENV
  def buildENV() => ENV
  
  ### () => Dataset
  def pullSourceData() => List[RowData]
  
  def buildTrainingUnit(
  		content: RowData,
  		tokenizer: transformers.tokenizer
  	)
  	=> TrainingUnit
  
  def buildDataset(
  		sourceAllData: List[TrainingUnit]
  	) => Dataset:
  	pass
  
  
  ### ENV.Label_HF, ENV.Label_tokenizer => Model_HF
  def pullTokenizer(tokenizerLabel: Label_tokenizer) => transformers.tokenizer
  def pullModel(
  		modelLabel: Label_HF, 
  		tokenizer: transformers.tokenizer
  	) => Model_HF:
  	pass
  
  
  ### () => TrainingArgs
  def buildTrainingArgs (
  		epoch?: int,
  		...
  	) => TrainingArgs:
  	pass
  
  
  ### ENV.TrainingSetProb, Dataset => DatasetSuit
  def buildTrainAndTest(
  		trainingSetProb: TrainingSetProb
  		dataset: Dataset
  	) => DatasetSuit:
  	pass
  
  
  ### TrainingSetProb, DatasetSuit, Model_HF => transformers.Trainer
  def buildTrainer (
  		trainBase: Model_HF, 
  		trainArgus: TrainingArgs, 
  		trainDatasets: DatasetSuit	
  	) => transformers.Trainer:
  	pass
  
  
  ### (Trainer) => Model_HF	
  def upTraining(trainer: Trainer) => Model_HF :
  	pass
  
  
  ### Types
  
  RowData: NewType('RowData', int)
  TrainingSetProb: NewType('TrainingSetProb', float)
  Label_HF: NewType('Label_HF', str)
  TrainingArgs: NewType('TrainingArgs', transformers.TrainingArguments)
  Dataset: NewType('Dataset', torch.utils.data.Dataset)
  
  class Model_HF(TypedDict):
  	modelLabel: Label_HF
  	tokenizer: transformers.tokenizer
  	model: transformers.AutoModel | None
  
  class TrainingUnit(TypedDict):
  	Input: List[str]
  	Ans: List[int | float ]
  
  class DatasetSuit(TypedDict):
  	trainSet: Dataset, 
  	testset: Dataset
  
  class ENV(TypedDict):
  	Label_tokenizer: str
  	Label_HF: Label_HF
  	TrainingSetProb: TrainingSetProb
```