---
project: Toshi
stars: 4251
description: A full-text search engine in rust
url: https://github.com/toshi-search/Toshi
---

Toshi
=====

##### A Full-Text Search Engine in Rust

> _Please note that this is far from production ready, also Toshi is still under active development, I'm just slow._

#### Description

Toshi is meant to be a full-text search engine similar to Elasticsearch. Toshi strives to be to Elasticsearch what Tantivy is to Lucene.

#### Motivations

Toshi will always target stable Rust and will try our best to never make any use of unsafe Rust. While underlying libraries may make some use of unsafe, Toshi will make a concerted effort to vet these libraries in an effort to be completely free of unsafe Rust usage. The reason I chose this was because I felt that for this to actually become an attractive option for people to consider it would have to have be safe, stable and consistent. This was why stable Rust was chosen because of the guarantees and safety it provides. I did not want to go down the rabbit hole of using nightly features to then have issues with their stability later on. Since Toshi is not meant to be a library, I'm perfectly fine with having this requirement because people who would want to use this more than likely will take it off the shelf and not modify it. My motivation was to cater to that use case when building Toshi.

#### Build Requirements

At this current time Toshi should build and work fine on Windows, Mac OS X, and Linux. From dependency requirements you are going to need 1.39.0 and Cargo installed in order to build. You can get rust easily from rustup.

#### Configuration

There is a default configuration file in config/config.toml:

host = "127.0.0.1"
port = 8080
path = "data2/"
writer\_memory = 200000000
log\_level = "info"
json\_parsing\_threads = 4
bulk\_buffer\_size = 10000
auto\_commit\_duration = 10
experimental = false

\[experimental\_features\]
master = true
nodes = \[
    "127.0.0.1:8081"
\]

\[merge\_policy\]
kind = "log"
min\_merge\_size = 8
min\_layer\_size = 10\_000
level\_log\_size = 0.75

##### Host

`host = "localhost"`

The hostname Toshi will bind to upon start.

##### Port

`port = 8080`

The port Toshi will bind to upon start.

##### Path

`path = "data/"`

The data path where Toshi will store its data and indices.

##### Writer Memory

`writer_memory = 200000000`

The amount of memory (in bytes) Toshi should allocate to commits for new documents.

##### Log Level

`log_level = "info"`

The detail level to use for Toshi's logging.

##### Json Parsing

`json_parsing_threads = 4`

When Toshi does a bulk ingest of documents it will spin up a number of threads to parse the document's json as it's received. This controls the number of threads spawned to handle this job.

##### Bulk Buffer

`bulk_buffer_size = 10000`

This will control the buffer size for parsing documents into an index. It will control the amount of memory a bulk ingest will take up by blocking when the message buffer is filled. If you want to go totally off the rails you can set this to 0 in order to make the buffer unbounded.

##### Auto Commit Duration

`auto_commit_duration = 10`

This controls how often an index will automatically commit documents if there are docs to be committed. Set this to 0 to disable this feature, but you will have to do commits yourself when you submit documents.

##### Merge Policy

\[merge\_policy\]
kind = "log"

Tantivy will merge index segments according to the configuration outlined here. There are 2 options for this. "log" which is the default segment merge behavior. Log has 3 additional values to it as well. Any of these 3 values can be omitted to use Tantivy's default value. The default values are listed below.

min\_merge\_size = 8
min\_layer\_size = 10\_000
level\_log\_size = 0.75

In addition there is the "nomerge" option, in which Tantivy will do no merging of segments.

##### Experimental Settings

experimental = false

\[experimental\_features\]
master = true
nodes = \[
    "127.0.0.1:8081"
\]

In general these settings aren't ready for usage yet as they are very unstable or flat out broken. Right now the distribution of Toshi is behind this flag, so if experimental is set to false then all these settings are ignored.

#### Building and Running

Toshi can be built using `cargo build --release`. Once Toshi is built you can run `./target/release/toshi` from the top level directory to start Toshi according to the configuration in config/config.toml

You should get a startup message like this.

  \_\_\_\_\_\_         \_\_   \_   \_\_\_\_                 \_\_
 /\_  \_\_/\_\_  \_\_\_ / /  (\_) / \_\_/\_\_ \_\_\_ \_\_\_\_\_\_\_\_\_/ /
  / / / \_ \\(\_-</ \_ \\/ / \_\\ \\/ -\_) \_ \`/ \_\_/ \_\_/ \_ \\
 /\_/  \\\_\_\_/\_\_\_/\_//\_/\_/ /\_\_\_/\\\_\_/\\\_,\_/\_/  \\\_\_/\_//\_/
 Such Relevance, Much Index, Many Search, Wow
 
 INFO  toshi::index \> Indexes: \[\]

You can verify Toshi is running with:

curl -X GET http://localhost:8080/

which should return:

{
  "name": "Toshi Search",
  "version": "0.1.1"
}

Once toshi is running it's best to check the `requests.http` file in the root of this project to see some more examples of usage.

#### Example Queries

##### Term Query

{ "query": {"term": {"test\_text": "document" } }, "limit": 10 }

##### Fuzzy Term Query

{ "query": {"fuzzy": {"test\_text": {"value": "document", "distance": 0, "transposition": false } } }, "limit": 10 }

##### Phrase Query

{ "query": {"phrase": {"test\_text": {"terms": \["test","document"\] } } }, "limit": 10 }

##### Range Query

{ "query": {"range": { "test\_i64": { "gte": 2012, "lte": 2015 } } }, "limit": 10 }

##### Regex Query

{ "query": {"regex": { "test\_text": "d\[ou\]{1}c\[k\]?ument" } }, "limit": 10 }

##### Boolean Query

{ "query": {"bool": {"must": \[ { "term": { "test\_text": "document" } } \], "must\_not": \[ {"range": {"test\_i64": { "gt": 2017 } } } \] } }, "limit": 10 }

##### Usage

To try any of the above queries you can use the above example

curl -X POST http://localhost:8080/test\_index -H 'Content-Type: application/json' -d '{ "query": {"term": {"test\_text": "document" } }, "limit": 10 }'

Also, to note, limit is optional, 10 is the default value. It's only included here for completeness.

#### Running Tests

`cargo test`

#### What is a Toshi?

Toshi is a three year old Shiba Inu. He is a very good boy and is the official mascot of this project. Toshi personally reviews all code before it is committed to this repository and is dedicated to only accepting the highest quality contributions from his human. He will, though, accept treats for easier code reviews.
