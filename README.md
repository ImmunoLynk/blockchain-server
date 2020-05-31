# COVID19 Anonymized Immunity Testing Results on public IPFS

This is a simple but effective implementation of a peer-to-peer descentralized test results validator.

App users can opt to donate their processed data to a public IPFS node so healthcare researchers can employ it on COVID-focused solutions.


## Immuno Lynk backend (server)

Server built on Flask using an HTTP API. All requests are handled then sent to an IPFS node instance running on AWS EC2. Infura's [API](https://infura.io/docs) was used to connect to a public IPFS node and register the data permanently or temporarily (depends on the PIN variable in server.py).

For production, a private node implementation example is providade in the /private_ipfs_node folder, courtesy of [dfile.app](dfile.app).

The endpoins are:

#### Image upload

Endpoint:
```bash
http://ec2-3-15-190-197.us-east-2.compute.amazonaws.com/image
```

Response:
```bash
{
    "Hash": "Qme9vV3FULEMiggF3i3fecvD8JQ5ysiAoZhyuTQDFkViWR",
    "Size": "9940",
    "id": "milos",
    "link": "https://ipfs.infura.io:5001/api/v0/cat?arg=Qme9vV3FULEMiggF3i3fecvD8JQ5ysiAoZhyuTQDFkViWR",
    "timestamp": "2020-04-05 13:16:16.393551",
    "type": "IMG"
}
```

#### Data upload

Endpoint:
```bash
http://ec2-3-15-190-197.us-east-2.compute.amazonaws.com/json
```

Response:
```bash
{
    "Hash": "Qme9vV3FULEMiggF3i3fecvD8JQ5ysiAoZhyuTQDFkViWR",
    "Size": "9940",
    "id": "milos",
    "is_immune": true,
    "link": "https://ipfs.infura.io:5001/api/v0/cat?arg=Qme9vV3FULEMiggF3i3fecvD8JQ5ysiAoZhyuTQDFkViWR",
    "scan_hash": "6c8whrnwr8w9eb6wb8erw",
    "timestamp": "2020-04-05 13:16:16.393551",
    "type": "IMG",
    "user_name": "Lon"
}
```

## Result recognition network (Deep Learning Model)

Model built using Keras and OpenCV2 to detect stripes on the image and determine the test results automatically from the uploaded and processes image.

Full code found in [Veeresh Shringar's repo](https://github.com/VeereshShringari/COVID-testing).

A very simple legacy implementation done at the MIT Hackathon is located at result_recognition_old/, though it's not used anymore.

