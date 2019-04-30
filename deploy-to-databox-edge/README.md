# Azure ML Hardware Accelerated Models - Deploy to Databox Edge
This notebook and sample code to showcase the use of Azure ML HW Accelerated Models on the Databox Edge machine. 

## Getting Started
These samples assume you have are familiar with the Azure ML HW Accelerated Models product. If not, you can read more [here](https://docs.microsoft.com/en-us/azure/machine-learning/service/concept-accelerate-with-fpgas).

### Prerequisites
- You must first have created an Azure ML BrainwaveContainerImage using the [Quickstart](https://github.com/Microsoft/aml-fpga-preview/blob/master/notebooks/project-brainwave-quickstart.ipynb) notebook. You can use Azure ML FPGA Images that were not built from the Quickstart, but you will have to update the input and output tensor names when deploying your sample client.
- Follow [these instructions](https://docs.microsoft.com/en-us/azure/databox-online/data-box-edge-deploy-configure-compute) to enable the Linux Compute VM on your Databox Edge Machine.

### Quickstart
```
git clone https://github.com/Azure-Samples/aml-real-time-ai.git
cd aml-real-time-ai/deploy-to-databox-edge
jupyter notebook
```

### Sample Client
The sample client iterates through images, sends a gRPC request to the Azure ML host module, prints the response, and also sends the response to IoT Hub as a message. The run.py script that is called on startup of the module takes the following parameters, which can be modified using Cmd argument in IoT Hub's Create Container options. 

```
usage: run.py [-h] [-d IMAGE_DIR] [-i INPUT_TENSORS] [-o OUTPUT_TENSORS]
              [-a ADDRESS] [-p PORT] [-w WAIT] [-s]

optional arguments:
  -h, --help            show this help message and exit
  -d IMAGE_DIR, --image-dir IMAGE_DIR
                        The file path of the image to inference. Default:
                        './assets/'
  -i INPUT_TENSORS, --input-tensors INPUT_TENSORS
                        The name of the input tensor you specified when
                        converting your model. Default for Brainwave resnet50:
                        'Placeholder:0'
  -o OUTPUT_TENSORS, --output-tensors OUTPUT_TENSORS
                        The name of the output tensor you specified when
                        converting your model. Default for Brainwave resnet50:
                        'classifier/resnet_v1_50/predictions/Softmax:0'
  -a ADDRESS, --address ADDRESS
                        The address of the inferencing container. For IOT
                        Edge, this is name of the inferencing host module on
                        the IOT Edge device. Default: azureml-fpga-host
  -p PORT, --port PORT  The port of the inferencing container. Default: 50051.
  -w WAIT, --wait WAIT  Time to wait between each inference call. Default: 10.
  -s, --suppress-messages
                        Flag to suppress IOT Hub messages. Default: False. Use
                        --wait flag to lessen or this flag to turn off IOT hub
                        messaging to avoid reaching your limit of IOT Hub
                        messages.
```
#### Example of Create Container Options with parameters
```
{
  "Tty": true,
  "Cmd": [
    "--input-tensors",
    "Placeholder:0",
    "--output-tensors",
    "classifier/resnet_v1_50/predictions/Softmax:0",
    "--wait",
    "0", 
    "-s"
  ]
}
```