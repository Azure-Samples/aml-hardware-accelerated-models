# AzureML FPGA Samples


## Getting Started
These samples assume you have are familiar with the AzureML FPGA product. If not, you can read more [here](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-accelerate-with-fpgas).

### Prerequisites
- You must first have created an AzureML BrainwaveContainerImage using the [Quickstart](https://github.com/Microsoft/aml-fpga-preview/blob/master/notebooks/project-brainwave-quickstart.ipynb) notebook. You can use AzureML FPGA Images that were not built from the Quickstart, but you will have to update the input and output tensor names when deploying your sample client.

### Quickstart
```
git clone https://github.com/Azure-Samples/aml-real-time-ai.git
cd aml-real-time-ai
jupyter notebook
```