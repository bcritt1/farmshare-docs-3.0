---
tags:
    - software
---

Sentaurus is Synopsys TCAD software used in Electrical Engineering courses and
research. On FarmShare it's provided, licensed and supported by EE, not by
Stanford Research Computing. You run it from a Caddyshack Desktop.

## Run Sentaurus

EE packages Sentaurus with its other course software for the Caddyshack
Desktop. Start a Caddyshack Desktop in [OnDemand]({{ facts.ondemand_url }}) and
follow EE's instructions for starting Sentaurus. See [Use Caddyshack for EE
Courses](../../use/caddyshack.md).

EE's copy of the software is in `/home/classes/ee/admin/software`, on storage
that every FarmShare node can read. To run Sentaurus in a batch job, ask EE how
to set it up from there.

## Things to Know

If you used Sentaurus on the old FarmShare, you may have loaded it with a module
setup kept in AFS. That setup doesn't work in batch jobs or desktops, because
AFS is only available on the login nodes. Use EE's current installation
instead.

Sentaurus gets its license from an EE license server. If it reports
`Cannot connect to license server system.`, the EE server is usually down or
unreachable, often during a network outage. Wait and try again. If it keeps
happening, contact EE's IT support.

For questions about Sentaurus itself, contact EE's IT support. For problems with
OnDemand or FarmShare, see [OnDemand and Desktops](../../fix/ondemand.md).
