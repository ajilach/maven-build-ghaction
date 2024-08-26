# Github action "maven-build-ghaction"

## Purpose

Building maven based projects the ajila way.

## Details

This action runs `mvn clean deploy` for the currently checked out sources. It uses the java and maven versions provided for the build job. Also it sets up the ajila artifact repository (Nexus) to resolve dependencies. Once built, it uploads the artifacts to Nexus and attaches themm to the Github workflow run. Finally, it notifies about its success or failure through Slack.

## Prerequisites

Make sure to have checked out the sources before triggering this step. See `Usage` below.

## Usage

Here is how you can call this action:

```yaml
on: [workflow_call]

jobs:
  build:
    name: Build ${{ github.ref }} branch
    runs-on: [self-hosted]
    outputs:
      build_version: ${{ steps.builder.outputs.build_version }}
      artefact_id: ${{ steps.builder.outputs.artefact_id }}

    steps:
        
      - name: Checkout source code
        uses: actions/checkout@v4.1.7

      - name: Building the maven artifacts
        id: builder
        uses: ajilach/maven-build-ghaction@v1.0.0
        with:
          java_version: '8'
          maven_version: '3.6.3'
          additional_profiles: 'jboss'
          slack_channel_id: CPX5X4B0P

```
