---
layout: home
title: Handle your AWS Spot Instance Actions with terminate-notice
---
You're running AWS Spot Instances, and suddenly your monitoring system notices
that the spot instances are being terminated without workloads being
effectively moved to another instance. How can we fix this?

AWS create an entry in the Metadata Service which the node can watch for. This
script polls that Metadata entry, and if it finds it, it runs any responding
scripts to cleanly move services elsewhere.

## How to Install?

### Individually

Get the latest release from [terminate-notice/terminate-notice](
https://github.com/terminate-notice/terminate-notice/releases/latest)

You will also need to install the appropriate actions, which are available from:

* [terminate-notice/terminate-notice-announce](
https://github.com/terminate-notice/terminate-notice-announce/releases/latest)
* [terminate-notice/terminate-notice-datadog](
https://github.com/terminate-notice/terminate-notice-datadog/releases/latest)
* [terminate-notice/terminate-notice-slack](
https://github.com/terminate-notice/terminate-notice-slack/releases/latest)
* [terminate-notice/terminate-notice-shutdown](
https://github.com/terminate-notice/terminate-notice-shutdown/releases/latest)

### Add a Debian Repository

Download the [public key](terminate-notice.gpg) and put it in
`/etc/apt/keyrings/terminate-notice.gpg`. You can achieve this with:

```
wget -qO- {{ site.url }}/terminate-notice.asc | sudo tee /etc/apt/keyrings/terminate-notice.asc >/dev/null
```

Next, create the source in `/etc/apt/sources.list.d/`

```
echo "deb [arch=all signed-by=/etc/apt/keyrings/terminate-notice.asc] {{ site.url }}/deb stable main" | sudo tee /etc/apt/sources.list.d/terminate-notice.list >/dev/null
```

Then run `apt update && apt install -y` followed by the names of the packages you want to install.

### Add a RPM Repository

Download the repo file `cd /etc/yum.repos.d ; curl {{ site.url }}/terminate-notice.repo -LO`

Then you can do `yum install -y` followed by the names of the packages you want to install.

### The packages you can install

Currently these are:

* terminate-notice
* terminate-notice-announce
* terminate-notice-datadog
* terminate-notice-shutdown
* terminate-notice-slack

## After installing the packages

You should configure settings that are installed into `/etc/terminate-notice.conf.d/` and then run

```
systemctl enable --now terminate-notice.service
```

## How to contribute?

Please contribute changes and bug reports in the relevant repository above.

Have a security issue? Please email [Jon](mailto:jon@sprig.gs) with details.

Have your own action? Please create a 
[pull request on this repository](https://github.com/terminate-notice/terminate-notice.github.io/pulls).

## Related

You might find [this document from AWS](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-instance-termination-notices.html) useful.

## Thanks

This script was created during my first month at [Dice.FM](https://dice.fm),
who very generously permitted me to release this code publically.