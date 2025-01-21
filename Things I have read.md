### 20241009
[Automating Auditing: An ambitious concrete technical research proposal](https://www.alignmentforum.org/posts/cQwT8asti3kyA62zc/automating-auditing-an-ambitious-concrete-technical-research)
- Here, "auditing" means "figuring out what's wrong with a model", in the context of an adversarial game where a person tries to corrupt its outputs in some desirable way
- Basically this is an ambitiously high standard to have for interpretability/safety generally; given a model that has been messed with in some way by an attacker
- Correctly points out that most interpretability work/workflows do interpretability in average or even best-case situations, where worst-case is really what we need for safety, particularly deceptive behavior
- Standard caveats about the fact that the desired distribution of output isn't perfectly clear apply; Evan acknowledges these things and you can still move forward to a good extent despite these.
- Similarly, in mentioning the solution of "training for transparency", standard caveats about the fact that specifying exactly what transparency is is also hard and prone to being Goodharted.
- An aside: was reminded by this about Evan's interest in myopia as a property of safe AI systems. In the modern paradigm, LLMs are kind of myopic, aren't they (caveats apply)? Chain of thought prompted ones mildly less so.
[Two Cultures In Mathematics](https://www.dpmms.cam.ac.uk/~wtg10/2cultures.pdf)
### Before 202410
- [[CLIP]]
- [Are Emergent Abilities of Large Language Models a Mirage?](https://arxiv.org/abs/2304.15004) 
	- I didn't like this one. I think the very premise-question of this thing is really ill-formed, and depends on a cherry-picked conception of "emergence". I don't know if anyone ever thought that with respect to the correct metric performance wasn't continuous, but the bottom line, "practical" observation is that the *effective/useful* abilities of a given model grow discontinuously.
	- [[Hidden Progress in Deep Learning- SGD Learns Parities Near the Computational Limit]] is a paper whose approach and framing I appreciate a lot more.
- [Against Almost Every Theory of Impact of Interpretability](https://www.lesswrong.com/posts/LNA8mubrByG7SFacm/against-almost-every-theory-of-impact-of-interpretability-1#7fNRMke9Gc4QghYyf)
	- I really struggled to engage with this completely, possibly because it was too sprawling and I couldn't keep all the author's points in my head or because I don't have enough prior engagement with this and related fields to really judge this person's arguments myself.
	- With that said, bottom line it's refreshing to see certain things I've thought about addressed by other people, and in particular I do agree with several of the things he said, such as:
		- Enumerative safety/reverse engineering is not a likely or practical outcome.
			- `Graphs like the ones just below can be overwhelming and remain very limited.`
		- Microscope AI is not a reasonable goal due to economic incentives.
		- Political coordination is necessary and a precursor to most work being useful, and in particular interpretability can be harmful due to "safety washing", and the obvious fact that interpretability helps capabilities
		- For various reasons, mechanistic interpretability work seems fundamentally incapable of providing guarantees or insight into "deceptive agents".
	- However, on the flip-side, many of the critiques do boil down to "the results aren't that impressive yet".
	- It was a good source of links to the unreliability of some interpretations, such as the [[But is it really in Rome? An investigation of the ROME model editing technique||Rome critique]].
