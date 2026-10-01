# Prompt examples

## Starting a feature

Invoked through a skill, so the agent follows the matching workflow:

> `/brainstorming` Can you take a look at the AI behaviour and check two things. First, make
> it feel less robotic. Also the difficulty scaling doesn't feel right: easy doesn't feel that
> different from expert.

> `/writing-plans` Can we allow the game to be played in both landscape and portrait? This
> would require all the UI to be in the correct places in both.

Then one line to choose how to execute the plan:

> subagent driven

## Reporting a bug

Describe what was seen, attach a screenshot, point at the evidence:

> When I quit from the host, the peer just pauses in time and I can't issue any commands. It
> never migrated the host. You can look at the Unity logs if needed and run any tests.

> In the main menu, when I select the largest match size, the difficulty selectors on the
> bottom players are squashed and hard to tap. They should all be the same size as the first
> player's.

> One of the vehicles starts drifting all over the place while it is shooting. It looks goofy
> and makes it harder to hit. Can you check why?

## Asking the agent to verify before handing back

> I think you can test with two instances, no? Can you test it out before I try it?

> I currently have an error in my Unity console. Can you check what it is?

> Before this work, can you check the logs in Unity and see why the build failed?

## Investigate first, change later

> In-game the phone gets really hot. Xcode shows the following stats. Can you take a look and
> see if we can reduce that? Don't commit anything yet, just let me know first what the issues
> are.

And the reply to the agent's list of findings, answering each one:

> I want to allow high frame rates, so capping is not an option. Let's do the second fix.
> Turn off the API validation. For explosions I want the same ones. For item 5, give me a
> detailed list of what the changes would be. Fix the combat cadence.

## Steering when it goes wrong

> Let's go by steps. It seems like you are getting stuck on something and you are not
> communicating what is going on. Tell me what you will do so we can run the plan in phases.

Followed, once trust was back:

> Do all phases and I'll check at the end.

## Small design calls

> In portrait I think I like the minimap at the bottom of the screen better.

> Can we add a gesture so the game can be played with one hand? For example double-tap and
> then drag: up and down zooms, left and right rotates.

## Checking what is left

> So what's left on my plate?

Useful after any long run. The agent answers with only the things that need a human.

## Patterns

- **State the symptom, not the suspected cause.** The agent finds the cause from logs and code.
- **Attach the evidence.** Screenshots and log files beat descriptions.
- **Say when you want a report and not a change.**
- **Answer option lists item by item.** Reject, accept, or ask for more detail on each.
- **Ask for verification explicitly** when the tools make it possible.
