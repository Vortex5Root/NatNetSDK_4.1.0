<h1 align="center"> NatNet-SDK (4.1.0.0) </h1>

<p align="center">
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/releases"><img alt="Dynamic TOML Badge" src="https://img.shields.io/badge/dynamic/toml?url=https%3A%2F%2Fraw.githubusercontent.com%2FVortex5Root%2FNatNetSDK_4.1.0%2Fmain%2Fpyproject.toml&query=%24.tool.poetry.version&logo=data%3Aimage%2Fpng%3Bbase64%2CiVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAMAAAAolt3jAAAAtFBMVEVHcEyWYTihdkuXYzrBjlqhbkHepWuzglG8hFGWYjmzglHepmz3z5iygVCWYjmWYjmxgVDsvorMlmDepmybaD2oe02ufU2leUzdpWqzglGfdUrgqnH616j%2F4LKWYjmvf1C3hVPepmyWYjmWZDuWYjmzglGWYjmwfk7fp22aZjz93a7VoGmpfFKdbEe4hlTFkFzwxZH30aDpuYO%2BnICUbUbGkl3jrnbjr3eSYjuuiWzNq4fjvI5PAatoAAAAJXRSTlMA4v34FBH4Jwwn4l8IXFG6%2FrWcv2PCZqdJxeX291Ci4uVQ5eQoZPLoqAAAAIxJREFUCNdFzscCgjAQBNA1JIAGVMDeW0iEAPb6%2F%2F9lCuqc9s1eBkDHpxTDN8E8mroJ9S1G0Sw7noSbrAMAHLvidshMERPwVlUuxF0Vb7ltgtdi5VUV%2BetcNAwZKyv%2BeP7J%2BD6VRaq5rKmiOUGoW3OzAzxEF2npLIgaGPbN1%2Bm07S4SjvkPOnjQI%2Bb4AGCaEYNClUKKAAAAAElFTkSuQmCC&label=Package%20Version"></a>
</p>

-------

<p align="center">
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/blob/master/LICENSE"><img src="https://img.shields.io/github/license/Vortex5Root/NatNetSDK_4.1.0.svg" alt="License">
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/releases"><img src="https://img.shields.io/github/downloads/Vortex5Root/NatNetSDK_4.1.0/total.svg" alt="GitHub all releases"></a><br>
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/network"><img src="https://img.shields.io/github/forks/Vortex5Root/NatNetSDK_4.1.0.svg" alt="GitHub forks"></a>
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/stargazers"><img src="https://img.shields.io/github/stars/Vortex5Root/NatNetSDK_4.1.0.svg" alt="GitHub stars"></a>
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/watchers"><img src="https://img.shields.io/github/watchers/Vortex5Root/NatNetSDK_4.1.0.svg" alt="GitHub watchers"></a><br>
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/issues"><img src="https://img.shields.io/github/issues/Vortex5Root/NatNetSDK_4.1.0.svg" alt="GitHub issues"></a>
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/pulls"><img src="https://img.shields.io/github/issues-pr/Vortex5Root/NatNetSDK_4.1.0.svg" alt="GitHub pull requests"></a>
    <a href="https://github.com/Vortex5Root/NatNetSDK_4.1.0/commits/master"><img src="https://img.shields.io/github/last-commit/Vortex5Root/NatNetSDK_4.1.0.svg" alt="GitHub last commit"></a><br>
</p>


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
