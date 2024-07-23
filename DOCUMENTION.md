
[![Dependencies Status](https://img.shields.io/badge/dependencies-up%20to%20date-brightgreen.svg)](https://github.com/Vortex5Root/NatNetSDK_4.1.0/pulls?utf8=%E2%9C%93&q=is%3Apr%20author%3Aapp%2Fdependabot)

[![Security: bandit](https://img.shields.io/badge/security-bandit-green.svg)](https://github.com/PyCQA/bandit)
[![Pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/Vortex5Root/NatNetSDK_4.1.0/blob/master/.pre-commit-config.yaml)
[![Semantic Versions](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--versions-e10079.svg)](https://github.com/Vortex5Root/NatNetSDK_4.1.0/releases)
[![License](https://img.shields.io/github/license/Vortex5Root/NatNetSDK_4.1.0)](./LICENSE)


# Index

| Topics | Sub Topics | Examples |
|--------|------------|----------|
| [NatNet-SDK](#NatNet-SDK) | [What is NatNet-SDK?](#What-is-NatNet-SDK?) | |
| | [What Function i have in NatNet-SDK?](#What-Function-i-have-in-NatNet-SDK?) | |
| | [How to imported?](#How-to-imported?) | [How to set the connection parameter's ?](#How-to-set-the-connection-parameter's-?) | |
| | | [How to reive the data from the Server?](#How-to-reive-the-data-from-the-Server?) |

## NatNet-SDK

### What is NatNet-SDK?

NatNet SDK is a library that allows you to communicate with the NatNet Server and retrieve data from the server. This library has been created to work with the NatNet protocol and is used to retrieve data from the server and display it in your application

## What Function i have in NatNet-SDK?

### How to imported?
```python
from natnetsdk.NatNetClient import NatNetClient

client = NatNetClient()
```

### How to set the connection parameter's ?

```python
client.set_client_address(optionsDict["clientAddress"]) # Set local IPv4 from the machine you are using to communicate to the NatNet Server 
client.set_server_address(optionsDict["serverAddress"]) # Set the server IPv4 from the machine running the NatNet Server
client.set_use_multicast(optionsDict["use_multicast"]) # MultiCast (True) / UniCast (False)
```

### How to reive the data from the Server?

NatNet Client work's based on callback function and to set the function is:

```python
def receive_new_frame(data_dict : Dict) -> None:
    '''
    {
        "frame_number" : int  # Contains the frame ID of the current iteration
        "marker_set_count" : int  # Number of marker sets in the data
        "unlabeled_markers_count" : int  # Number of unlabeled markers in the data
        "rigid_body_count" : int  # Number of rigid bodies in the data
        "skeleton_count" : int  # Number of skeletons in the data
        "asset_count" : int  # Number of assets in the data
        "labeled_marker_count" : int  # Number of labeled markers in the data
        "timecode" : float  # Timecode of the data
        "timecode_sub" : float  # Subtimecode of the data
        "timestamp" : float  # Timestamp of the data
        "is_recording" : bool  # Indicates if the data is being recorded
        "tracked_models_changed" : tracked_models_changed  # Indicates if the tracked models have changed
        "mocap_data" : MoCapData  # Mocap data for the current frame (all the information send by the system)
    }
    '''

client.new_frame_listener = receive_new_frame
```

How to start retrieving data from the server

```python
is_running = streaming_client.run() # -> bool
```
