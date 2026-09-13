# Privacy Policy

**Effective date: September 13, 2026**

## Overview

jetson-bot is a privately operated Discord bot used for local automation, archival, search, retrieval, summarization, and agentic assistance.

The bot is not an advertising service, data broker, or public data collection service.

## Data We Process

When the bot is present in a Discord server or channel, it may process data made available to it through Discord, including:

* Message content
* Message metadata, such as timestamps and channel identifiers
* Discord user identifiers and display information
* Attachments, links, reactions, and related message information where required by the bot's functionality
* Commands and interactions sent to the bot

The bot only accesses data available to it through its authorized Discord integration.

## How Data Is Used

Discord data may be used for functionality including:

* Local backup and archival
* Search and retrieval
* Conversation context and memory
* Summarization and knowledge extraction
* Local AI and agentic assistance
* Operating and improving the bot's intended functionality

Message content obtained from Discord is **not used to train or fine-tune machine-learning or AI models**.

AI models may process message content at inference time to perform features such as retrieval, summarization, reasoning, or assistance.

## Storage

Data retained by jetson-bot is stored on infrastructure controlled by the operator, primarily on local systems.

Stored Discord data is not made publicly available merely because it was accessible to the bot.

Reasonable technical safeguards are used to protect retained data, including encryption at rest where required.

## Sharing and Sale of Data

jetson-bot does not sell, license, or commercialize Discord API data.

Discord message content and other Discord API data are not made available for unrestricted copying, redistribution, or commercial use.

Data is not shared with third parties except where:

* necessary to operate an explicitly configured service provider;
* required by law; or
* specifically requested or authorized by the applicable user.

If the bot's processing architecture changes to transmit Discord data to additional external services, this Privacy Policy will be updated accordingly.

## Data Retention

Data may be retained while it remains necessary for jetson-bot's stated functionality, including archival, memory, retrieval, and agentic assistance.

Data may be deleted when:

* it is no longer required for those purposes;
* the applicable user requests deletion;
* Discord requests deletion;
* operation of the relevant functionality ends; or
* deletion is otherwise required by applicable law or Discord's terms.

Backups and derived indexes associated with deleted data will also be removed where reasonably necessary and technically feasible.

## Data Access, Correction, and Deletion

Users may request access to, correction of, or deletion of Discord data associated with them.

Retained copies mirror what was posted on Discord, so a correction is made by editing the message on Discord; the daily reconciliation described below applies the edit to the retained copy. The operator does not rewrite retained messages by hand.

Requests can be made by contacting the operator through the contact methods provided by the jetson-bot project or directly through Discord.

Sufficient information may be requested to verify the identity of the person making the request before modifying or deleting data.

## The jlab Message Cache

This section describes one specific store: the message cache kept by jetson-ai-lab-cli (`jlab`), the component that reads, searches and backs up channel history. Where it is more specific than the general sections above, this section applies.

### What is collected

* Only channels of the configured Discord server that the server's `@everyone` role can view. Private and role-gated channels are never fetched, and a channel that later becomes private is purged (see Retention).
* For each message: the message body, the message id, the channel id, the author's Discord user id, the author's name and display name, whether the author is a bot, the time it was posted, the time it was last edited, the time the copy was stored, and a link back to the message.
* Attachments, embeds and reactions are not stored in the cache.
* The bot never posts, reacts, or edits anything; its Discord access is read-only.

### How it is stored

* The cache is a MongoDB database on infrastructure controlled by the operator, dedicated to this component.
* The message body and the author's name and display name are encrypted before they reach the database, using AES-256-GCM with a key derived from an operator-held secret. The operator's tooling measures that stored content is not readable as plaintext.
* Ids, timestamps and the message link are stored unencrypted so the cache can be queried and so deletions can run without decrypting anything.
* Encryption protects data at rest in the database. It does not protect against anyone who holds the key or can read the running process.

### Retention

* Messages are kept only while backup, search and retrieval need them, and never indefinitely: the operator runs a scheduled purge that deletes cached messages, and reports derived from them, older than a stated number of days.
* The operator runs a reconciliation pass daily. It applies edits made on Discord, removes messages deleted on Discord, and purges all cached content and reports for any channel that is no longer visible to `@everyone`, has been deleted, or is no longer reachable by the bot.
* A message deleted on Discord can remain in the cache until the next reconciliation pass.

### Deletion

* On request, the operator deletes every cached message by a given author, or every cached message from a given channel, together with every generated report that mentions that author or channel.
* To make an author's deletion permanent, the operator keeps a one-way keyed hash of that author's Discord user id. The hash cannot be read back into the id; it is used only to refuse re-caching that author's messages in later fetches and reconciliation passes. Messages written by other people that mention the author are other people's content and are not removed by this request.
* When operation of this component ends, the operator deletes the cache channel by channel, together with its reports.

### Sharing

Cache contents are not shared, sold or transmitted to third parties. Search and read results are shown only to the operator and to the operator's own local tooling.

## User Content

Users retain their rights in content they create.

This Privacy Policy does not grant jetson-bot users, the operator, or third parties any independent license to copy, publish, sell, or redistribute another user's Discord content.

## Security

Reasonable administrative and technical measures are used to protect retained data against unauthorized access, disclosure, alteration, or loss.

Developer credentials and Discord tokens are treated as confidential credentials and are not intentionally exposed publicly.

## Changes to This Policy

This Privacy Policy may be updated when jetson-bot's functionality or data-processing practices change.

The current version will be maintained in the jetson-bot repository.

## Contact

For privacy questions or requests concerning stored data, contact the operator through the jetson-bot repository or through Discord.
