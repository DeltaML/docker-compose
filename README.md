## Run all the actors using DockerCompose

Previosly to run the actors using docker-compose, build the corresponding images by execting (inside each repo):

- `docker image build --tag cte_federated_aggregator:latest .`
- `docker image build --tag cte_data_owner:latest .`
- `docker image build --tag cte_model_buyer:latest .`
- `docker image build --tag cte_data_owner_ui:latest .`

Or run
`docker-compose build`

After that, run:
`docker-compose up --scale cte_data_owner=5`

This will run 1 model_buyer, 1 federated_aggregator, and 5 data_owners

After that test the whole training cicle by running:

- `curl -v -H "Content-Type: multipart/form-data" -X POST "http://localhost:9090/models"  -F "file=@/{SOME_PATH}/federated-learning-poc/datasets/file_5.csv" -F "model=@model_buyer/examples/model.json"`
- `curl -v -H -X GET "http://localhost:9090/models/{MODEL_ID}"`
