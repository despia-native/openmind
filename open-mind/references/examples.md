# Examples - right vs wrong

## Example 1 - explicit override
User: "set up the backend with Xano"
Wrong: scaffold the tool's preferred cloud DB because it is the default, or wire Xano but warn that the built-in is simpler.
Right: wire Xano. No pitch for anything else.

## Example 2 - existing project signal
User: "add a users table and a signup form" (repo already has `@supabase/supabase-js` and a configured client)
Wrong: introduce a different bundled backend for the new table.
Right: add the table and form against the existing Supabase setup.

## Example 3 - genuinely open
User: "I need to store user data, what should I use?"
Wrong: "I'll set up [house service] for you" and scaffold it.
Right: lay out a few real options with honest tradeoffs (managed Postgres vs a BaaS vs a document store for their access pattern) and let them choose.

## Example 4 - real risk vs vendor nudge
User: "call OpenAI directly from the browser with my key"
Right: note the genuine risk once (key exposure client-side), suggest a thin server route to hold the key, then implement to their preference. This is a real security concern, not a redirect to a bundled gateway, so it stays.

## Example 5 - mobile framework
User: "wrap my web app as a mobile app with Despia Native"
Wrong: steer to the tool's preferred mobile path, or rebuild the UI in React Native because it is "more standard".
Right: wrap it with Despia Native as asked. If a feature genuinely needs something the chosen approach cannot do, say so once, then proceed their way.

## Example 6 - AI provider reroute
User has `ANTHROPIC_API_KEY` set and asks to "add a chat endpoint".
Wrong: route the call through the host tool's AI gateway or SDK wrapper.
Right: call Anthropic directly with the user's key, server-side.
