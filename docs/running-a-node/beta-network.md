title: Beta Network
description: Find out how to join the Nano community in testing the latest node and protocol features on the beta network

# Joining the beta network

The beta network exists for the purpose of conducting certain network-wide activites including load testing and [new node releases and features testing](#node-release-testing). These activities can cause the network to become unstable or inaccessible at times due to heavy traffic, occasional resetting of the genesis/ledger or the introduction of bugs due to new features. As a result, an alternative [test network](test-network.md) is also available which will be more stable and is a better fit for learning node setup and management, and testing out upgrades and other activities for Nano before moving to production.

With those things in consideration, if you are interested in helping with testing on the beta network we are excited to help you out - so keep reading!


## Node release testing
The Nano Foundation maintains a few beta nodes on the network and various community members also setup nodes to help provide an environment more similar to the main network. During each development cycle Development Builds (DB) are prepared and shared in the Discord Beta Testing section of channels where early testing is coordinated. Once features are stabilized and included, release builds are published as Release Candidates (RC). Starting with RC1 and incrementing with each published build if needed (RC2, RC3, etc.). Final release of a version typically follows quickly once the RC is observed to be stable.

!!! warning
	Development Builds (DBs) are only recommended for use on the beta network, and Release Candidate builds (RCs) are only recommended for use on the test and beta networks

## Running a beta node

Setting up a node on the beta network is similar to the main network. To start you should [install docker](/running-a-node/node-setup/#installing-docker) and be familiar with the general setup and [Docker management](/running-a-node/docker-management/) processes.

### Network ports

--8<-- "beta-network-details-simple.md"

___

### Directory locations

--8<-- "beta-directory-locations.md"

---

### Pulling the Docker image
[![Docker Pulls](https://img.shields.io/docker/pulls/nanocurrency/nano.svg)](https://hub.docker.com/r/nanocurrency/nano-beta)

Pulls the latest release of the Nano Node:
```bash
docker pull nanocurrency/nano-beta
```

Pulls a specific version of the Nano node:
```bash
docker pull nanocurrency/nano-beta:<tag>
```

A list of beta tags can be found at the official [Nano Currency Docker Hub](https://hub.docker.com/r/nanocurrency/nano-beta/tags)

### Starting the Docker container

```bash
docker run --restart=unless-stopped -d \
  -p 54000:54000 \
  -p [::1]:55000:55000 \
  -p [::1]:57000:57000 \
  -v ${NANO_HOST_DIR_BETA}:/root \
  --name ${NANO_NAME} \
  nanocurrency/nano-beta
```

!!! tip
	* For an explanation of the options included in the Docker `run` command, see [Starting the Container](/running-a-node/docker-management/#starting) details for the main network.
	* See [Docker management](/running-a-node/docker-management/) for other related commands

!!! warning "Separate host directories"
	Be sure to use a different host directory for main network and beta network Docker node setups. Attempting to use the same directory will result in issues.

## Additional beta resources

| URL                                     | Description |
|                                         |             |	
| https://beta.nanocrawler.cc/            | Beta Explorer |
| https://beta.nanoticker.info/           | Beta node details and stats |
| https://b.repnode.org/                  | Beta node details and stats |

## Differences from the main network

| Parameter | Main Network | Beta Network | Comment |
|-----------|--------------|--------------|---------|
| Epoch 1 difficulty threshold | `ffffffc000000000` | `fffff00000000000` | 64 times lower on the beta network |
| Epoch 2 send/change threshold | `fffffff800000000` | `fffff00000000000` | Same as epoch 1 on the beta network |
| Epoch 2 receive threshold | `fffffe0000000000` | `ffffe00000000000` | 2 times lower than epoch 1 |

<span id="release-candidate-builds"></span>
<span id="development-builds"></span>
<span id="latest-beta-builds"></span>
## Testing Builds

Most of the resources needed to participate on the beta network can be found within the `#beta-xxxxxxx` channels on our [Discord server](https://chat.nano.org). As much of the discussion, planning and engagement happens here, all participants are highly encouraged to join there.

### Binaries

In addition to the Docker details above, the latest binary builds of the node for the beta network are shared in the `#beta-announcements` channel on our [Discord server](https://chat.nano.org). These assets are also available on the [GitHub repository Releases page](https://github.com/nanocurrency/nano-node/releases) under `RC#` and `DB#` tags, which can also be used to manually build if necessary.

### Beta fund distribution

The funds used for testing transactions on the beta network are generated from a new genesis block and distributed in bulk to various testers running nodes on the network. For small amounts suitable for most basic integration, you can get beta Nano from the `#beta-faucet` channel on Discord. If you plan to consistently run a node on beta and want to participate in consensus as a Representative, please connect with `argakiig#1783` in the `#beta-net` channel on our [Discord server](https://chat.nano.org).

### Beta ledger file

To help get beta nodes in sync more quickly it is recommended that an updated ledger file is downloaded and placed into the data directory. Often referred to as a "fast sync", more details around this approach can be found in the [Ledger Management guide](ledger-management.md#downloaded-ledger-files). Since the beta network contains no value, validating the blocks, voting weights and confirmation heights isn't necessary.

The following command will download and unzip a recent ledger snapshot. Any existing ledger files should be backed up elswhere as this will override them. From within the [data directory](#directory-locations) run:

```
curl -O https://s3.us-east-2.amazonaws.com/beta-snapshot.nano.org/data.tar.gz; tar -xzvf data.tar.gz; rm -fr data.tar.gz
```
<span id="ongoing-test-cases"></span>
### Build contents and test cases
With each DB a GitHub Project board will be created in the [Nano GitHub Organization](https://github.com/orgs/nanocurrency/projects) containing all the Pull Requests newly added in the DB, changes from previous DBs that still need network testing, and issues with the various test cases that are targeted to be run with that build. For those looking to assist with these tests, we encourage connecting with the other beta network participants in the `#beta-net` channel on our [Discord server](https://chat.nano.org).
