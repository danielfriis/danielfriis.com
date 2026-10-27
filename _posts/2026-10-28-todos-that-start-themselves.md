---
title: Todos that start themselves
description: I built a todo app I share with my AI assistant. I write the todo, and the assistant takes the first step. It’s open source now.
date: 2026-10-28
# A draft on an unmerged branch. Set the date to launch day; drop unlisted to list it.
unlisted: true
---

<!--
  DRAFT for Daniel. Written in your voice from what the code shows. Every
  [Daniel: …] is a fact only you know: fill it in or cut the sentence. Nothing
  here describes your own routine beyond what the repo proves.
-->

Most of my todos don’t stall on the doing. They stall on the first step. “Find a cheaper internet plan” sits on the list for weeks. Switching takes ten minutes. Comparing six plans first is the part nobody wants to do.

That first step is exactly what an AI agent is good at. But my agent lived in a chat window, and my todos lived in a todo app, and the two never met. [Daniel: one line on how you handled this before. Copy-pasting todos into a chat?]

So I built [Headstart](https://headstart.lab.nowadays.tech). It’s a todo app for iPhone and Mac that I share with my assistant.

When I write a todo, Headstart sends it to my assistant, and the assistant starts on it. It writes what it found into the todo’s notes, with sources and links. Under the todo it leaves one line of status, like “Cheapest: [Daniel: a real status line from your list]”. When it needs a decision from me, the status line asks.

[Daniel: which part surprised you? A guess to keep or cut: the status line turned out to matter most, because I see where everything stands without opening anything.]

Some todos are mine alone. When I write one of those, I switch the assistant off, and it never sees it.

## The assistant is the other user

I’ve [argued before]({% post_url 2026-10-18-the-next-operating-system %}) that MCP servers are the new apps. You set them up once, and every job can use them.

Headstart is built that way. The iPhone and Mac apps are one way into the list. The MCP server is the other. Claude can add it as a custom connector and sign in with OAuth, and any other agent that speaks MCP can read and write the same todos. My assistant isn’t a feature inside the app. It’s the second user of it.

It also needs an assistant that’s always on. A todo I write at 23:00 gets sent at 23:00. [Daniel: where does your webhook go? The Mac Studio from the operating-system note?]

## How it’s built

- A Cloudflare Worker with a D1 database holds the todos.
- A Durable Object pushes every change to the apps over a WebSocket, so the list updates live on every device.
- The worker sends each new todo to a webhook, and exposes an MCP server for the assistant to write back.
- The apps are SwiftUI, for iPhone and Mac. They keep a local copy, so they work offline.

## It’s open source

The code is on [GitHub](https://github.com/nowadays-tech/headstart) under the MIT license. There is no App Store version and no hosted sign-up. You deploy the worker to your own Cloudflare account and build the app in Xcode. The README walks through each step.

[Daniel: a closing line in your words: who should try it, or what you want to hear back.]
