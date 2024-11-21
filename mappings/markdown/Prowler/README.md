# Event Dossier: Prowler

## Prowler Finding
- **Description**: Prowler natively generates findings in the OCSF Detection Finding format using the [`py-ocsf-models`](https://github.com/prowler-cloud/py-ocsf-models) library.

- **Event References**
  - https://docs.prowler.com/projects/prowler-open-source/en/latest/tutorials/reporting/#json-ocsf
  - https://github.com/prowler-cloud/py-ocsf-models

## OCSF Version 1.2.0
 - `activity_id`: `1` (`Create`)
 - `category_uid`: `2` `(Findings)`
 - `class_uid`: `2004` `(Detection Finding)`
 - `metadata.product.name`: `Prowler`
 - `metadata.product.vendor_name`: `Prowler`

## Mapping

Prowler has an [OCSF](https://github.com/prowler-cloud/prowler/blob/70fdc2693ed4d5c64bddcdb52b0ce3a491a5220c/prowler/lib/outputs/ocsf/ocsf.py#L26) class with a [`transform()`](https://github.com/prowler-cloud/prowler/blob/70fdc2693ed4d5c64bddcdb52b0ce3a491a5220c/prowler/lib/outputs/ocsf/ocsf.py#L47) method, in charge of translating a Prowler finding into a OCSF Detection Finding object.
