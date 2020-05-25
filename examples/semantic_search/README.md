Assumption - 
You have installed torchserve and torch-model-archive. If not then follow [quick start guide](https://github.com/pytorch/serve) given on github/serve to install the same

Prerequisites - 
- pip install zipfile
- pip install json
- pip install sentence-transformers

Steps to follow to deploy this example - 

1. git clone https://github.com/pytorch/serve.git; cd serve/
2. git checkout issue_390
2. cd examples/semantic_search
3. ./create-mar.sh
4. Move the generated 'sentence_xformer.mar' file to your model-store
5. start torchserve [start in a different terminal]
torchserve --start --model-store <path_to_your_model_store>
6. register your model zipped inside mar file
curl -v -X POST "http://localhost:8081/models?initial_workers=1&synchronous=true&url=sentence_xformer.mar"
7. now test it
./test_sentence.py
8. Above should print semantic search output similar to given here https://github.com/UKPLab/sentence-transformers/blob/master/examples/applications/semantic_search.py  