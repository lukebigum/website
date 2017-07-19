+++
title = "MCollective"
weight = 130
toc = true
+++

Configuring MCollective with Choria is generally very simple and involves just including 1 module and setting some Hiera data, it takes care of the entire process for you.

In MCollective terminology a _client_ is one you manage your network from - where you run _mco_ commands - and a _server_ is a node being managed.

{{% notice info %}}
Your mcollective config files in */etc/puppetlabs/mcollective* should be factory default before starting this, especially important if you previously tried to use another module to configure it
{{% /notice %}}

## Every node

All nodes should have the _choria-mcollective_ module on them, by default every node becomes a MCollective Server ready to be managed via MCollective:

{{% notice info %}}
The choria/mcollective_choria module has a number of [dependencies](https://forge.puppet.com/choria/mcollective_choria/dependencies), if you use R10k to manage environments please be sure to fetch all dependencies.
{{% notice %}}


```puppet
node "server1.example.net" {
  include mcollective
}
```

## Client nodes

On machines where you wish to run _mco_ commands like your Bastion nodes you have to configure them to be clients, you do this via _Hiera_:

```yaml
mcollective::client: true
```

If you wish to have Client Only machines, you can disable the server on them:

```yaml
mcollective::client: true
mcollective::server: false
```

