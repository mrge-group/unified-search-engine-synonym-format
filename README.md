# Unified Synonym Format for search engines 

This repository holds proposals and tools for crafting a unified synonym format
to load and exchange synonyms into search engines. 

## Motivation

- human readable
- machine parsable
- single point of truth for a query string
- importable into query, bmax and solr

## Format proposal

We strive for a format parsable and validatable using a standard tool. The Querqy
synonym format is a good starting point, which we push to the YAML standard. Let's
start with an example:

```yaml
definitions:
  - personal computer:
    synonyms:
      - pc
      - desktop computer
    subtopics:
      - laptop
      - notebook
    up:
      - ibm
    down:
      - software
``` 