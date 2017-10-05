# Universal Resolver - Examples

## did:btcr

	curl -i -X GET  https://uniresolver.danubetech.com/1.0/identifiers/did:btcr:xkrn-xzcr-qqlv-j6sl

	HTTP/1.1 200 
	Server: nginx/1.10.3
	Date: Tue, 19 Sep 2017 08:16:18 GMT
	Content-Type: application/ld+json;charset=UTF-8
	Transfer-Encoding: chunked
	Connection: keep-alive
	
	{
	  "id" : "did:btcr:xkrn-xzcr-qqlv-j6sl",
	  "control" : [ ],
	  "service" : {
	    "agent" : "https://azure.microsoft.com/dif/hub/did:btcr:xkrn-xzcr-qqlv-j6sl",
	    "xdi" : "https://xdi03-at.danubeclouds.com/cl/=!:did:btcr:xkrn-xzcr-qqlv-j6sl"
	  },
	  "owner" : {
	    "id" : "did:btcr:xkrn-xzcr-qqlv-j6sl",
	    "type" : [ "CryptographicKey", "EdDsaSAPublicKey" ],
	    "curve" : "secp256k1",
	    "publicKeyHex" : "024a63c4362772b0fafc51ac02470dae3f8da8a05d90bae9e1ef3f5243180120dd"
	  },
	  "@context" : "https://example.org/did/v1"
	}

## did:sov

	curl -i -X GET  https://uniresolver.danubetech.com/1.0/identifiers/did:sov:WRfXPg8dantKVubE3HX8pw

	HTTP/1.1 200 
	Server: nginx/1.10.3
	Date: Tue, 19 Sep 2017 08:21:03 GMT
	Content-Type: application/ld+json;charset=UTF-8
	Transfer-Encoding: chunked
	Connection: keep-alive
	
	{
	  "id" : "did:sov:WRfXPg8dantKVubE3HX8pw",
	  "control" : [ ],
	  "service" : {
	    "xdi" : "https://xdi03-at.danubeclouds.com/cl/=!:did:sov:WRfXPg8dantKVubE3HX8pw"
	  },
	  "owner" : {
	    "id" : "did:sov:WRfXPg8dantKVubE3HX8pw",
	    "type" : [ "CryptographicKey", "EdDsaSAPublicKey" ],
	    "curve" : "ed25519",
	    "publicKeyBase64" : "H3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
	  },
	  "@context" : "https://example.org/did/v1"
	}

## div:v1
	
	curl -i -X GET  https://uniresolver.danubetech.com/1.0/identifiers/did:v1:testnet:5431fafa-a38f-4e37-96b6-cdeb8e5d1d40

	HTTP/1.1 200 
	Server: nginx/1.10.3
	Date: Thu, 05 Oct 2017 18:20:32 GMT
	Content-Type: application/ld+json;charset=UTF-8
	Transfer-Encoding: chunked
	Connection: keep-alive
	
	{
	  "@context" : "https://w3id.org/veres-one/v1",
	  "id" : "did:v1:testnet:5431fafa-a38f-4e37-96b6-cdeb8e5d1d40",
	  "authorizationCapability" : [ {
	    "permission" : "UpdateDidDocument",
	    "entity" : "did:v1:testnet:5431fafa-a38f-4e37-96b6-cdeb8e5d1d40",
	    "permittedProofType" : [ {
	      "proofType" : "LinkedDataSignature2015"
	    }, {
	      "proofType" : "EquihashProof2017",
	      "equihashParameterAlgorithm" : "VeresOne2017"
	    } ]
	  } ],
	  "authenticationCredential" : [ {
	    "id" : "did:v1:testnet:5431fafa-a38f-4e37-96b6-cdeb8e5d1d40/keys/1",
	    "type" : "CryptographicKey",
	    "owner" : "did:v1:testnet:5431fafa-a38f-4e37-96b6-cdeb8e5d1d40",
	    "publicKeyPem" : "-----BEGIN PUBLIC KEY-----\r\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAjBdn1zUIUFrjoO8ZnHCM\r\nrvvNIoruTW8e5stPJ2Zv8Py0RJiO6N4d/pr3L7AptWo4RDt6kI/KF6iBf8BFiRr/\r\nJw+/ZF8N9r2rXzLuE+P/foQwi5SC51/vKa3STptGc8sRvx5T3++gcIMu6jS0JExZ\r\nasYS3Gw75szL4mRpxXxJOSQwSS5nmPZljMxc9A/SML0vLN0zxuUHjoUXUdRGltfu\r\nzI8lqTvIP2aVSFO8zyAAXCDzky6IFNncSfh3d8PdMYLB2n9yoR8WATO5P+M6jFx3\r\nNSOJ6n/Tv18kYg5oe0BFokhEJEbsXrqjPdi/5oij6HOZQJBw6UfbKW2zDKf0JYNc\r\n4wIDAQAB\r\n-----END PUBLIC KEY-----\r\n"
	  } ]
	}
                                                                