# Unified Search Engine Synonym Format

This repository holds proposals and tools for crafting a unified synonym format
to easily exchange synonyms and load them into various search engines. 

## Design goals

- human readable
- machine parsable standard format (YAML, JSON)
- single point of truth for a single query string
- importable into Query, Bmax and (partially) Solr

## Not covered here

This repository will not hold any real synonyms. It is up the query parser
used to handle the given synonyms. If the query parser is not capable of 
handling _subtopics_ or _up_ and _down_ boosts, it should ignore those.

## Format proposal

We strive for a format parsable and validatable using a standard tool. The [Querqy
synonym format](https://github.com/renekrie/querqy#input-matching) is a good starting point, 
which we push to the YAML standard. Let's start with an example:

```yaml
definitions:
  - bicylce:
    synonyms:
      - bike
    subtopics:
      - mountain bike
      - road bike
    up:
      - 105
      - chorus
      - dura ace
    down:
      - book
      - glove
``` 

In this example `bicycle` and `bike` are bidirectional synonyms to each other.
This means further more that the following concepts apply to both terms. 
Subtopics are directional synonyms expanding the recall for a given term. In
this case, you should search for `mountain bike` and `road bike` when originally
searching for `bicycle` (or `bike`).

Synonyms and subtopics expand the recall of a search query, the _up_ and _down_
entries manipulate the ranking of the search results. _Up_ terms should boost
documents containing those terms, _down_ terms should penalize documents in
search result ranking.
