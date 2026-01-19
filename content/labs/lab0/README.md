# Access Cloudera Environment

**Goals**

- [ ] Welcome
- [ ] Use Case Overview
- [ ] Connect to Cloudera on cloud control plane

## The Scenario

![Need Coffee](../../assets/images/coffee.png){ align=right }

Pager shrieked. 3:17 AM. Seriously? Who the hell is calling me at this ungodly hour? Groaning, I swatted at the bedside table, finally silencing the infernal device. 'Infamous PCI,' my phone screen mocked me. Of course, it had to be the middle of the night.  The air in the office always had that faint aroma of impending doom, a mix of stale coffee and the lingering fear of a massive data breach. I stumbled towards my desk, the keyboard lights reflecting in my bleary eyes. The dashboard indicates an increase in suspicious transactions...

Man, 3:25 AM, an unholy hour when only pizza delivery drivers and rogue algorithms were supposed to be awake, I'll have to follow our newly reviewed procedure "Operation TransactionBusters" and check some parameters before calling my manager that we got robbed...

## Establishing Access to the Cloudera on cloud Environment

Before you can start looking for frauds and other cool stuff, confirm that you can access the system.

We will be using today Cloudera on Cloud,
Connect to the Cloudera Control Plane via our [login portal](https://login.cdpworkshops.cloudera.com/auth/realms/se-workshop-2/protocol/saml/clients/cdp-sso).

Use the credentials that you selected for your group in this [spreadsheet](https://docs.google.com/spreadsheets/d/1AMRPY3MER_aFh7T3upj25M_iizkBFXEKc6M_kakemiE/edit).

![Hands on Lab Flow Overview](../../assets/images/cdp-public-cloud-diagram-vert-light.png)


<details>
- Go to the this link.

    https://raw.githubusercontent.com/22itay/hol-nifi-hbase/refs/heads/main/content/labs/lab0/fastlinks.ps1

- edit `<<<XXX>>>` in line 2 & 3 with the values from your browser.
- run in your PC Powershell cli
<summary><b>Click to expand fast links guide</b></summary></details>

### Checklist

- [ ] Are you able to connect to the Cloudera Control Plane?
- [ ] Do you see in Environments  list `cldr-gre-cdp-env` ?
- [ ] Do you see in Datahubs at least one `datahub` ?
- [ ] optional set fast links

**:rocket: We have now concluded `Welcome Lab` :rocket:**
