OCSF Examples repository contains a collection of sample mappings (raw events to OCSF events), and a collection of demonstrative use-cases of OCSF transformed datasets. 

### Sample Mappings
A variety of sample mappings can be found in the `/mappings` directory of this repository. The mappings are organized based on the mapping DSL (Domain Specific Language) used for the transformation. Additionally, a few mappings are provided in a generic markdown file. Sample raw events and corresponding OCSF normalized events can also be found in the /samples sub-directory for each mapping submission.


### How to submit your mappings?

1. Use a directory that corresponds to the mapping DSL you are using. If a directory doesn't exist, feel free to create one. If you want to submit platform agnostic mappings, you can utilize the markdown format as described in the [submission spec](https://github.com/ocsf/examples/blob/main/mappings/markdown/submission_spec.md).
2. Within a platform/DSL dir, all the mappings are organized in a `Vendor > OCSF Version > Product > _mappings_` structure. Whenever missing, create your sub directories accordingly.
3. Each mapping example, must be accompanied by a sample input log record and it's corresponding OCSF transformed record. In your `product` dir, create a `samples` dir to store your sample input record as `*.raw` and its OCSF transformed version as `*.ocsf` files.
4. Ensure the transformed OCSF record is a valid OCSF file by utilizing the validation endpoint available [here](https://schema.ocsf.io/doc/index.html#/Tools/SchemaWeb_SchemaController_validate).
