## MLflow Proto To GraphQL

### What is this

The system in `dev/proto_to_graphql` parses proto rpc definitions and generates graphql schema based on the proto rpc definition. The goal of this system is to quickly generate base GraphQL schema and resolver code so that we can easily take advantage of the data joining functionalities of GraphQL.

The autogenerated schema and resolver are in the following file: `mlflow/server/graphql/autogenerated_graphql_schema.py`

You can run `./dev/proto_to_graphql/code_generator.py` to trigger the codegen process.

We use Graphene as the library to run our GraphQL server.

### FAQs

#### How to onboard a new rpc to GraphQL

- In `mlflow/server/handlers.py`, identify the handler function for your rpc, for example `_get_run`, make sure there exists a corresponding `get_run_impl` function that takes in a `request_message` and returns a response messages that is of the generated service_pb proto type.
- In your proto rpc definitino, add `option (graphql) = {};` and re-run `./dev/generate-protos.sh` and `./dev/proto_to_graphql/code_generator.py`. You should see the changes in the generated schema.

TODO: Add more bullet points after we create some example PRs