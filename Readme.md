<Header1>Quick test repo for Concourse
Concourse get should be able to read this repo

<Header2>Concourse Config.yml
---
resources:
- name: git-concourse-test
  type: git
  icon: github
  source:
    uri: https://github.com/JonathanMorley2/concourse-test

jobs:
- name: job
  public: true
  plan:
  - get: git-concourse-test
    trigger: true
  - task: list-files
    config:
      inputs:
        - name: git-concourse-test
      platform: linux
      image_resource:
        type: registry-image
        source: { repository: busybox }
      run:
        path: ls
        args: ["-la", "./git-concourse-test"]


