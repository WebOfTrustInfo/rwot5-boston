# DID Gentle Introduction

By Kim Hamilton Duffy, Learning Machine

IN PROGRESS

The BTCR hackathon in July was my first exposure to DIDs and DDOs. I wrote this very introductory document to help consolidate my understanding. Because my understanding of DIDs/DDOs is largely restricted to BTCR (and relatively new at that), details may be wrong. But I hope it will provide others with a more user-friendly intro to the [DID spec](https://w3c-ccg.github.io/did-spec/).

## Motivation

At a vert high level, DID is solving the same problems as PGP. But PGP does things in a way that's confusing from a usability perspective. The primary concept that's difficult in PGP is key recovery. (Technically, PGP can be set up with a cold storage key, but this is an option that many users overlook).

The goal is to take the lessons from PGP and improve on usage. Decentralized Identifiers (DIDs) are a fundamental tool in accomplishing this.

## Improvements over PGP

DID aims to provide simple key recovery options, including:
- social recovery, i.e. a group of friends you've designated in advance. Examples:
  - uPort
  - Sovrin
- hardware wallets: for secure self-recovery

DID provides a flexible mechanism of proof of control; proof of control can be provided in multiple ways (in contrast to PGP). 

Additionally, use of a blockchain (which is not critical to DID, but is used in many DID methods) provides an advantage over central servers used in PGP.

## Important concepts

### DDOs

DIDs are almost always accompanied by DID description objects (DDOs). DDOs contain additional detail about the DID, including:
- How an individual can cryptographically prove ownership of the DID and DDO.
- How an individual can cryptographically prove control of the DDO. 

To drill into this distinction, proof of control applies to the ability to update the DDO itself. Updating the DDO would be desired, for example, when rotating keys, adding other new keys (e.g. a PGP key), revoking leaked keys.

### Owner vs control and Guardians

Note that an owner of a DID/DDO may want to give some other trusted party the ability to update ("control") the DDO. This is useful, for example, if I want to let someone else update the DDO on my behalf if I lose my private key(s). I can give the trusted party the ability to update the DDO, without them impersonating me, by listing their DID (or DID per trusted party) in the `control` block of my DDO.

Control is also relevant in a "Guardian"-managed DDO, i.e. when a trustee is managing an identity on behalf of a user. Guardian-managed identities take the burden off an individual to manage their own private keys. So this is relevant for usability, but also when a person cannot manage private keys. For the latter, think newborn baby: perhaps we want to assign a decentralized identity, but it cannot reasonably be owned by the baby until it is 6 months? 1 year? I guess it depends on how smart the baby is.

If I allow a guardian to manage my DID, the guardian may sign on my behalf, and another party would trust them when they sign on my behalf (per the DDO rules). However, the guardian is not in a position to impersonate me.

## Key-related FAQs

- A DDO may contain other keys that are useful. In an owner-managed DDO, I will always have at least one primary key, but I may also add other keys that I use in different contexts.
- If the DDO is signed, the `creator` must correspond to a control key
