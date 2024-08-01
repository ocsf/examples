# OCSF Examples

This, the OCSF Examples repository, contains a collection of
supporting content for OCSF, such as:

1. example mappings (raw events to OCSF events),
2. a collection of demonstrative use-cases of OCSF transformed
   datasets,
3. notes and tooling to help develop OCSF-related technology (_e.g._,
   recommended best practices for encoding OCSF events using different
   technologies)

## Mappings

Mappings are all about transforming "native" events into OCSF events.
That is, mapping the syntax and semantics of events coming from
systems that are OCSF-unware to instances of classes within OCSF.


### Sample Mappings

A variety of sample mappings can be found in the `/mappings` directory of this repository. The mappings are organized based on the mapping DSL (Domain Specific Language) used for the transformation. Additionally, a few mappings are provided in a generic markdown file. Sample raw events and corresponding OCSF normalized events can also be found in the /samples sub-directory for each mapping submission.

### How to submit your mappings?

1. Use a directory that corresponds to the mapping DSL you are using. If a directory doesn't exist, feel free to create one. If you want to submit platform agnostic mappings, you can utilize the markdown format as described in the [submission spec](https://github.com/ocsf/examples/blob/main/mappings/markdown/submission_spec.md).
2. Within a platform/DSL dir, all the mappings are organized in a `Vendor > OCSF Version > Product > _mappings_` structure. Whenever missing, create your sub directories accordingly.
3. Each mapping example, must be accompanied by a sample input log record and it's corresponding OCSF transformed record. In your `product` dir, create a `samples` dir to store your sample input record as `*.raw` and its OCSF transformed version as `*.ocsf` files.
4. Ensure the transformed OCSF record is a valid OCSF file by utilizing the validation endpoint available [here](https://schema.ocsf.io/doc/index.html#/Tools/SchemaWeb_SchemaController_validate).
5. A reference of the structure outlined above can be found [here](https://github.com/ocsf/examples/tree/main/mappings/markdown/AWS).

## Encodings and Representation

Encodings are all about how OCSF events (instances of OCSF classes)
are serialized in order to be transported in space (_e.g._, over a
network between systems) or time (_e.g._, saved on disk), so is about
how events in an abstract OCSF schema are turned into sequences of
bytes.  For example, [JSON](https://www.json.org/json-en.html) is one
way of representing OCSF events as a sequence of bytes.  (Since OCSF
was built starting with from a JSON perspective, the recommendations
for that encoding are fairly straightforward)

More generally, representations are how OCSF events are represented
within a computing system.  Here we usually use representation to
connote how OCSF events are modeled in a process's memory, and so is
more about language-specific data structures.  For example, in
[Go](https://go.dev/) it is common practice to use `struct` types to
represent objects with named fields.

Note that these are _informative_ guidelines, designed to assist the
development of systems around OCSF by sharing experiences and giving
developers a head start; the source of truth for OCSF events is the
OCSF schema itself.  However, in pursuit of the opportunity for
exchanging events between systems built by different vendors - that
is, interoperability - consistency is important.

More details about representations and encodings can be found in the
[`encodings/`](encodings/README.md) directory.


## raw_sample_logs
This is a place to store sanitized log datasets. Text datasets will throw an error at 50MB and fail to upload at 100MB so keeps it smaller then 100MB. Please try and donate log file datasets with a high cardinality of event types. The more event types that exist in each dataset, the easer it is to conditionally map each log source. Thank you for your participation in the OCSF. The file Stucture is to be "vendor name"/"vendor product" -> file.json 