# Datadog API Tools

Ideally this repo can hold multiple (preferably small) tools for working with
the datadog API. Cloudops has a lot of code where we use `curl` to interact
with the Datadog API, but sometimes that's not easy to reason about.

Wouldn't it be cool if we had [small, modular tools](https://en.wikipedia.org/wiki/Unix_philosophy#Do_One_Thing_and_Do_It_Well) to interact with the API?

## Tools in this repo
- [json-to-datadog](#json-to-datadog): Takes a JSON object/hash and sends each item in the hash as a metric to datadog.


# json to datadog
Send metrics to datadog from JSON.

This tool takes a json object like this from `STDIN`

```
{
  "cf-staging": 74,
  "cf-staging-diego": 24,
  "cf-staging-diego-netman": 3,
  "cf-staging-mysql-standalone": 17,
  "cf-staging-routing": 9,
  "concourse-staging-worker": 11,
  "datadog-firehose-nozzle": 5,
  "metacourse-staging-worker": 4,
  "staging-opentsdb": 6,
  "staging-opentsdb-firehose-nozzle": 6
}
```

and sends it to datadog. It assumes:

- That the key in this object (`cf-staging`, for example) will become a tag in datadog
- That the user has `$DATADOG_KEY` created

## Example Usage
For example, if you have a file in your home directory named `bosh-stats-json`, 
you can send that data to datadog with the following:

`cat ~/bosh-stats-json | ./json_to_datadog --metric cloudops_tools.deployment_count --tag-prefix bosh-stats -v`

## Arguments
```
Usage: ./json_to_datadog
Options:
  --metric           Name of the metric to store in datadog
  --tag-prefix       Namespace prefix for metric tag
  --verbose          Enable verbose output
  --api-key          Your datadog api key (can also be set as $DATADOG_KEY)
  --additional-tags  A list of additional tags you want to send, formatted like 'environment:prod,foo:bar'
```


