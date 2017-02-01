# json to datadog

This tool takes a json object like this

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
`cat ~/bosh-stats-json | ./json_to_datadog --metric cloudops_tools.deployment_count --tag-prefix bosh-stats -v`


