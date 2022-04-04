# ibp-fabric-toolchain

- Chaincode Repository - a git repository for the chaincode/smart contract code.
- Tekton is used as the CI pipeline engine


## One Org - Peer Managed Chaincode

Single organization implies that the is not a separate organization(s) that must also approve updates of the Chaincode 
Definition. Outside the scope of a Tekton Pipeline - requires business process workflow!

Peer Managed Chaincode implies that the binary logic of the smart contract is included within the chaincode package linked to the chaincode definition. i.e. this is not the as-a-service model.


? How are endorsement policies, and collection configurations handled.
? Sole update of these parts of the configuration
? Need to spec peers that the chaincode needs to be installed on

? Sequence and Version number; going to need a query of the current state

## Assumed workflow

*Pull Requests*.  Creating a PR on the chaincode repository, should build and test the code, but does not deploy to a running IBP or Fabric.

*Release* Creating a git release/tag on the chaincode repository triggers the start of the deployment processes.

`pr-pipeline.yml`
- extracts the git repository,
- runs a build task
- (should include the test task)

`one-org-deploy-pipeline.yml`
- extracts the git repository,
- runs a build task
- runs a test task
- runs a chaincode-install-approve task
- runs a chaincode-commit-task


`task-chaincode-install-approve`
- 