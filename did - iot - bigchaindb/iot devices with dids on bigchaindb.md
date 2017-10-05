# Representing IoT devices in BigchainDB using DID

This document defines key methods for registering and maintaining identity of "things" (IoT devices) in BigchainDB (BDB) using Decentralized Identifiers (DIDs).

## 1. Representation of a device

### 1.1 Relationship with the registrant

The devices' DID will have the _guardian_ control from the user. Which means the device or thing being registered will be a dependent of the registrant user.

Example:
```
{
    "@context": "https://example.org/did/v1",
    "id": "did:example:21tDAKCERh95uGgKbJNHYp",
    "guardian": "did:example:8uQhQMGzWxR8vw5P3UWH1j"

    ...
}
```

> Here the user with DID `did:example:8uQhQMGzWxR8vw5P3UWH1j` is expected to be already registered in the ledger.

### 1.2 Inside a BDB Transaction

The DDO of the device/thing will be wrapped in the metadata of the asset in BDB transaction. Also, in the metadata, device specific details can be stored.

Example:
> The following metadata object has the device details (here a car) in the __data_ field and the DDO under the __did_ field.

```
"metadata": {
        "_data": {
            "capacity": 4,
            "color": "white",
            "oem": "BMW",
            "vehicletype": "car_sedan",
            "model": "X12017"
            "vin": "WBA7F2C51GGE12249"
        },
        "_did": {
            "@context": "https://example.org/did/v1",
            "id": "did:example:21tDAKCERh95uGgKbJNHYp",
            "guardian": "did:example:8uQhQMGzWxR8vw5P3UWH1j",
            "created": "2017-08-21T08:00:13.370Z",
            "updated": "2017-08-21T08:00:13.370Z",
            "signature": {
                "type": "",
                "created": "",
                "creator": "",
                "signatureValue": ""
            }
        }
    }
```

The asset of the BDB transaction will have the schema and namespace for this device representation.

```
"asset": {
        "data": {
            "ns": "bdb.assets.did.car",
            "schema": "https://example.org/did/v1"
        }

```

## 2 Registration of a new device in BDB

The registration of a new device will be a _CREATE_ transaction operation with the data and DDO wrapped in metadata (see section 1, above)

### 2.1 Control of device by administrators

The _control_ field of the DDO can be used for assigning one or more administrators to the device which can change the DDO of the device - in case of a admin override when keys are expired or lost.

> The control DID(s) should also be checked/validated in BDB.

### 2.2 Owner property of DDO

The devices will be _**associated**_ with the registrant using the _guardian_ field of the DDO, however the _owner_ field of the DDO will have the public key of the device itself. This will be used for verifying messages coming from the device which are signed by the device's private key. Hence, **both guardian and owner fields of the DDO will be utilized**.

### 2.3 Service property of DDO

The _service_ property of the device DDO can be used for,

1. Identification of the endpoint where the device will publish messages

2. Identification of the schema uri for the device messages

Example:
```
"service": {
        "node": "10:20:30:40:443/iot/messages",
        "schema": "https://example.message.schema"
    }

```

## 3. Device Messages

The messages/telemetry coming from the devices will have the device DID and the payload will be signed by the device's private key.

Example:
```
{
    "deviceId": "did:example:21tDAKCERh95uGgKbJNHYp"
    "payload": "<signed payload>"
}

```

## 4. DID method spec translation for BDB

1. **Create** - Create will be a BDB Create Transaction as defined above in section 2.

2. **Read/Resolve** - It will be a query on BDB with the asset Id corresponding to the DID of the device.

3. **Update** - Transfer transaction with same to and from public keys, this will be used to update the metadata of the asset in the said transaction, which also holds the DDO.

4. **Control** - Can be implemented using a crypto condition and fullfillment - similar to how inputs and outputs work for assets. For example: if the condition is fulfilled, then th e DDO can be changed.


## 5. Note

1. This is a work in progress.

2. This is not a full DID method spec.

3. The DID spec underwent a revamp in RWOT 5 and this document/spec needs to be updated accordingly.
