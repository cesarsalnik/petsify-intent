# Case: moving the knowledge base from Notion to Fibery

*October 2026. One real task delegated to an AI agent (Claude, connected to Notion and Fibery through MCP), shown step by step.*

## The task

Move our team workspace from Notion into Fibery and organise it well: documents, meeting notes, product features, decisions, roadmap and calendar views.

## First result, and why I rejected it

The agent built a clean structure in Fibery, but many items kept a link back to the original Notion page instead of carrying the content itself. It looked finished. It wasn't, because we were leaving Notion.

My feedback, translated from Polish:

> "We won't use Notion at all. Fibery has to be the only knowledge base. You can't put documents in as links to Notion. Actually move them in."

That changed the definition of done: **zero dependency on Notion**, including images.

## What the agent did after the feedback

- Rebuilt the content inside Fibery: 71 documents, 24 meetings, 11 features and 6 decisions.
- Moved images into the documents themselves, not as links. The agent's environment couldn't download Notion's image files, so it switched to letting Fibery fetch them on the server side. One showcase document alone needed 30 images.
- Deleted the "Notion URL" fields and added a files field for attachments.
- Rebuilt the views: roadmap board, feature status, decisions grid, meetings, calendar, wiki, hypotheses and a start page.

## Problems caught along the way

- **Duplicated content.** The showcase document ended up with old and new blocks side by side. The agent removed the old blocks.
- **Wrong place.** The start page view was first created in a private space instead of the team space. It was deleted and recreated where the team can see it.

## How "done" was proven

I didn't accept a "migration complete" message. The final check was a scan of all content and fields for any remaining Notion links. It found none, apart from historical mentions inside meeting notes ("we discussed this in Notion"), which we kept on purpose because they're part of the record.

What this check proves, and what it doesn't: it proves nothing in Fibery depends on Notion any more. It doesn't prove that every document is complete, that every image displays, or that permissions are right. Those weren't checked systematically.

## What I take from it

- The agent was fast at the repetitive work: over a hundred items moved and formatted.
- The first output was plausible but wrong for our real goal. My part was defining the goal precisely ("no Notion dependency at all"), rejecting a result that only looked finished, and choosing a check that proves it.
