# Pre-Read Materials

This directory is used to store files that can be provided as initial context to the multi-agent framework at the start of a new run.

## How it Works

1.  Place any files you want the agents to read (`.md`, `.txt`, `.pdf`, etc.) in this directory **before** you initiate a new `GOAL:`.
2.  When a new run starts, the framework will detect the files in this directory.
3.  It will then present you with a numbered list of the available files.
4.  You can select which files the agents should ingest for their initial analysis.

This allows you to provide a common set of contextual documents (market reports, internal memos, competitor analysis, etc.) that can be reused across multiple runs.
