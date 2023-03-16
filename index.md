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

You should configure settings that are installed into `/etc/terminate-notice.conf.d/`

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